---
name: nextjs-security
description: 'Secure Next.js applications on Vercel. Use when implementing auth, configuring headers, handling secrets, rate limiting, or preventing common web vulnerabilities. Covers OWASP top 10 for Next.js, Supabase Auth integration, and Vercel-specific security patterns.'
license: MIT
metadata:
  author: dojo-admin
  version: "1.0.0"
---

# Next.js Security — Dojo Admin

Security-first patterns for building with Next.js on Vercel with Supabase. This is a multi-tenant SaaS with payment data — security is non-negotiable.

## Core Principle

**Every request is untrusted until proven otherwise.** Validate on the server. Authorise at the database (RLS). Authenticate at the middleware. Never trust the client.

## Scoring

**Goal: 10/10.** When reviewing code for security, rate it 0-10. A 10/10 means all auth is server-side, all data access goes through RLS, no secrets leak to the client, and all inputs are validated. Always provide the current score and specific improvements needed to reach 10/10.

---

## 1. Authentication

**Pattern:** Supabase Auth + middleware guard + server-side session validation

```ts
// middleware.ts — guards all dashboard routes
import { createMiddlewareClient } from '@supabase/auth-helpers-nextjs'
import { NextResponse } from 'next/server'

export async function middleware(req) {
  const res = NextResponse.next()
  const supabase = createMiddlewareClient({ req, res })

  // Refresh session if expired
  const { data: { session } } = await supabase.auth.getSession()

  if (!session && req.nextUrl.pathname.startsWith('/dashboard')) {
    const loginUrl = new URL('/login', req.url)
    loginUrl.searchParams.set('next', req.nextUrl.pathname)
    return NextResponse.redirect(loginUrl)
  }

  return res
}
```

**Server Component session check (belt-and-suspenders):**

```tsx
// In any server component that handles sensitive data
import { createServerComponentClient } from '@supabase/auth-helpers-nextjs'
import { cookies } from 'next/headers'
import { redirect } from 'next/navigation'

export default async function ProtectedPage() {
  const supabase = createServerComponentClient({ cookies })
  const { data: { session } } = await supabase.auth.getSession()

  if (!session) redirect('/login')

  // Fetch user-scoped data — RLS enforces ownership at DB level
  const { data } = await supabase.from('students').select('*')
  // ...
}
```

**Never:**
- Store JWTs in `localStorage` (use httpOnly cookies via Supabase helpers)
- Trust user-provided `user_id` in request body — derive it from the session
- Skip the middleware guard and rely solely on RLS (defence in depth)

---

## 2. HTTP Security Headers

Add these in `next.config.js`:

```js
// next.config.js
const securityHeaders = [
  {
    key: 'X-DNS-Prefetch-Control',
    value: 'on',
  },
  {
    key: 'Strict-Transport-Security',
    value: 'max-age=63072000; includeSubDomains; preload',
  },
  {
    key: 'X-Frame-Options',
    value: 'SAMEORIGIN',
  },
  {
    key: 'X-Content-Type-Options',
    value: 'nosniff',
  },
  {
    key: 'Referrer-Policy',
    value: 'origin-when-cross-origin',
  },
  {
    key: 'Permissions-Policy',
    value: 'camera=(), microphone=(), geolocation=()',
  },
  {
    key: 'Content-Security-Policy',
    value: [
      "default-src 'self'",
      "script-src 'self' 'unsafe-eval' 'unsafe-inline'", // tighten in production
      "style-src 'self' 'unsafe-inline'",
      `connect-src 'self' ${process.env.NEXT_PUBLIC_SUPABASE_URL}`,
      "img-src 'self' data: blob:",
      "font-src 'self'",
    ].join('; '),
  },
]

module.exports = {
  async headers() {
    return [
      {
        source: '/(.*)',
        headers: securityHeaders,
      },
    ]
  },
}
```

---

## 3. Input Validation

**All server action inputs must be validated with Zod:**

```ts
'use server'
import { z } from 'zod'
import { createServerActionClient } from '@supabase/auth-helpers-nextjs'
import { cookies } from 'next/headers'

const schema = z.object({
  name: z.string().min(1).max(100).trim(),
  email: z.string().email().toLowerCase(),
  phone: z.string().regex(/^\+?[\d\s-]{7,15}$/).optional(),
})

export async function updateStudent(id: string, formData: FormData) {
  // 1. Validate input
  const parsed = schema.safeParse(Object.fromEntries(formData))
  if (!parsed.success) {
    return { error: parsed.error.flatten() }
  }

  // 2. Verify session (never trust client-provided user_id)
  const supabase = createServerActionClient({ cookies })
  const { data: { session } } = await supabase.auth.getSession()
  if (!session) return { error: 'Unauthenticated' }

  // 3. Update — RLS enforces that this user owns the record
  const { error } = await supabase
    .from('students')
    .update(parsed.data)
    .eq('id', id)

  if (error) return { error: error.message }
  return { success: true }
}
```

---

## 4. Environment Variables

| Type | Prefix | Example | Accessible in |
|------|--------|---------|---------------|
| Public (safe to expose) | `NEXT_PUBLIC_` | `NEXT_PUBLIC_SUPABASE_URL` | Browser + Server |
| Private (secrets) | (none) | `SUPABASE_SERVICE_ROLE_KEY` | Server only |
| Stripe | (none) | `STRIPE_SECRET_KEY` | Server only |

**Rules:**
- `SUPABASE_SERVICE_ROLE_KEY` MUST only be used in Route Handlers and Edge Functions — never in Client Components or Server Components that run on user request
- `STRIPE_SECRET_KEY` only in webhook route handlers and Edge Functions
- Never log secrets — use `[REDACTED]` in error messages
- Rotate keys if they ever appear in client bundles (check with `NEXT_PUBLIC_` grep)

**Check for leaks:**
```bash
# Find any private keys mistakenly prefixed as public
grep -r "NEXT_PUBLIC_SUPABASE_SERVICE" .
grep -r "NEXT_PUBLIC_STRIPE_SECRET" .
```

---

## 5. CSRF Protection

Next.js Server Actions have built-in CSRF protection (origin checking). Route Handlers do not.

For Route Handlers that accept mutations (e.g. Stripe webhooks):

```ts
// app/api/webhooks/stripe/route.ts
import { headers } from 'next/headers'
import Stripe from 'stripe'

export async function POST(req: Request) {
  const body = await req.text()
  const signature = headers().get('stripe-signature')!

  let event: Stripe.Event
  try {
    // Stripe signature verification IS the CSRF protection for webhooks
    event = stripe.webhooks.constructEvent(
      body,
      signature,
      process.env.STRIPE_WEBHOOK_SECRET!
    )
  } catch {
    return new Response('Invalid signature', { status: 400 })
  }

  // Handle event...
}
```

---

## 6. Rate Limiting

Use Vercel's Edge Middleware with a simple in-memory store, or Upstash Redis for distributed rate limiting:

```ts
// middleware.ts (add rate limiting to auth routes)
import { Ratelimit } from '@upstash/ratelimit'
import { Redis } from '@upstash/redis'

const ratelimit = new Ratelimit({
  redis: Redis.fromEnv(),
  limiter: Ratelimit.slidingWindow(10, '10 s'), // 10 requests per 10 seconds
})

export async function middleware(req) {
  if (req.nextUrl.pathname.startsWith('/api/auth')) {
    const ip = req.ip ?? '127.0.0.1'
    const { success } = await ratelimit.limit(ip)
    if (!success) {
      return new Response('Too many requests', { status: 429 })
    }
  }
  // ...
}
```

---

## 7. SQL Injection

Supabase JS client uses parameterised queries — you cannot directly write raw SQL from the client. However:

- Never use `.rpc()` with user-constructed SQL strings
- Never interpolate user input into filter values without validation
- Use Zod to validate IDs are valid UUIDs before using them in queries:

```ts
const idSchema = z.string().uuid()
const safeId = idSchema.parse(params.id) // throws if not a UUID
```

---

## 8. Multi-Tenancy Data Isolation

Every query must be scoped to the authenticated user's dojo. RLS handles this at the database level — but server-side checks add defence in depth:

```sql
-- Supabase RLS policy (set this up in Supabase dashboard)
CREATE POLICY "Users can only see their own dojo's students"
ON students
FOR ALL
USING (dojo_id = (
  SELECT dojo_id FROM profiles WHERE id = auth.uid()
));
```

---

## Security Checklist (run before every PR)

- [ ] All Server Actions validate inputs with Zod
- [ ] No user-provided IDs used in queries without UUID validation
- [ ] Session checked in all protected server components
- [ ] No secrets in `NEXT_PUBLIC_` variables
- [ ] Stripe webhooks verify signature before processing
- [ ] Rate limiting on auth routes
- [ ] Security headers configured in `next.config.js`
- [ ] RLS policies exist on all tables with user data
- [ ] No `console.log` statements that could leak sensitive data
