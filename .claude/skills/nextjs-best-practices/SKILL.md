---
name: nextjs-best-practices
description: 'Apply Next.js App Router best practices for this project. Use when building pages, layouts, data fetching, caching, or API routes. Covers RSC vs Client Components, server actions, route handlers, and Vercel deployment patterns.'
license: MIT
metadata:
  author: dojo-admin
  version: "1.0.0"
---

# Next.js Best Practices — Dojo Admin

Opinionated guide for building with Next.js App Router in this project. Every pattern here is chosen to maximise performance on Vercel and correctness with Supabase.

## Core Principle

**Server Components by default. Client Components only when you need them.** The App Router makes RSC the default — resist the urge to `"use client"` everything. The browser should receive as little JavaScript as possible.

## Scoring

**Goal: 10/10.** When writing or reviewing Next.js code, rate it 0-10 based on adherence to these principles. Always provide the current score and specific improvements needed to reach 10/10.

---

## 1. Component Architecture

### Server vs Client Components

| Use Server Component when | Use Client Component when |
|--------------------------|--------------------------|
| Fetching data | Using `useState` or `useEffect` |
| Accessing backend resources | Event listeners (onClick, onChange) |
| Keeping secrets server-side | Browser-only APIs |
| Reducing client JS bundle | Real-time subscriptions |
| Static rendering | Shadcn components with interactions |

**Pattern — Push `"use client"` to leaf nodes:**

```tsx
// ✅ Good — only the interactive part is a Client Component
// app/students/page.tsx (Server Component)
import { StudentTable } from './student-table'
import { getStudents } from '@/lib/data'

export default async function StudentsPage() {
  const students = await getStudents()
  return <StudentTable students={students} />
}

// components/student-table.tsx
'use client'
export function StudentTable({ students }) { ... }
```

### Layouts

- Use `layout.tsx` for UI that persists across routes (sidebar, nav)
- Use `template.tsx` only when you need fresh state on navigation
- Keep layouts as Server Components — fetch shared data there

---

## 2. Data Fetching

### Fetch in Server Components

```tsx
// ✅ Fetch directly in the component — no useEffect needed
export default async function DashboardPage() {
  const { data: students } = await supabase
    .from('students')
    .select('*')
    .eq('active', true)

  return <StudentList students={students} />
}
```

### Parallel Data Fetching

```tsx
// ✅ Fetch in parallel to avoid waterfalls
export default async function DashboardPage() {
  const [studentsResult, paymentsResult] = await Promise.all([
    supabase.from('students').select('count'),
    supabase.from('payments').select('sum(amount)'),
  ])
}
```

### Server Actions for Mutations

```tsx
// app/students/actions.ts
'use server'
import { revalidatePath } from 'next/cache'

export async function createStudent(formData: FormData) {
  const name = formData.get('name') as string

  const { error } = await supabase
    .from('students')
    .insert({ name, dojo_id: await getDojoId() })

  if (error) throw new Error(error.message)
  revalidatePath('/students')
}
```

---

## 3. Caching Strategy

Next.js caches aggressively. Know what each mechanism caches:

| Mechanism | What | Duration |
|-----------|------|----------|
| Request memoization | `fetch()` within a request | Per request |
| Data Cache | `fetch()` responses | Until revalidated |
| Full Route Cache | Static page HTML | Until revalidated |
| Router Cache | Client-side page segments | 30s (dynamic) / 5min (static) |

**Rules for this project:**
- Supabase queries via the JS client bypass Next.js Data Cache — use `revalidatePath()` or `revalidateTag()` after mutations
- Use `{ next: { revalidate: 60 } }` on `fetch()` calls that can be stale
- Use `export const dynamic = 'force-dynamic'` on routes with user-specific data
- Prefer `generateStaticParams` for content that rarely changes

---

## 4. Route Organisation

```
app/
├── (auth)/                    # Auth group (sign-in, sign-up)
│   ├── login/page.tsx
│   └── signup/page.tsx
├── (dashboard)/               # Protected admin routes
│   ├── layout.tsx             # Auth guard + sidebar
│   ├── page.tsx               # Dashboard home
│   ├── students/
│   │   ├── page.tsx           # Student list
│   │   ├── [id]/page.tsx      # Student detail
│   │   └── actions.ts         # Server actions
│   ├── payments/
│   └── settings/
├── api/                       # Route handlers (webhooks, etc.)
│   └── webhooks/
│       └── stripe/route.ts
└── layout.tsx                 # Root layout
```

- Group routes with `(folder)` to apply layouts without affecting URL
- Co-locate `actions.ts` with the routes that use them
- Use `loading.tsx` and `error.tsx` at each route level

---

## 5. Loading and Error States

```tsx
// app/(dashboard)/students/loading.tsx
import { Skeleton } from '@/components/ui/skeleton'

export default function StudentsLoading() {
  return <Skeleton className="h-96 w-full" />
}

// app/(dashboard)/students/error.tsx
'use client'
export default function StudentsError({ error, reset }) {
  return (
    <div>
      <p>Failed to load students: {error.message}</p>
      <button onClick={reset}>Try again</button>
    </div>
  )
}
```

---

## 6. TypeScript

- Enable strict mode in `tsconfig.json`
- Type all Server Action params and return values
- Use `z` (Zod) for runtime validation of form data and API inputs
- Never use `any` — use `unknown` and narrow it

```tsx
import { z } from 'zod'

const createStudentSchema = z.object({
  name: z.string().min(2).max(100),
  email: z.string().email(),
  belt_level: z.enum(['white', 'yellow', 'orange', 'green', 'blue', 'brown', 'black']),
})

export async function createStudent(formData: FormData) {
  'use server'
  const raw = Object.fromEntries(formData)
  const validated = createStudentSchema.parse(raw) // throws ZodError on invalid input
  // ...
}
```

---

## 7. Vercel Deployment

- Use Edge Runtime for middleware (auth guards)
- Use Node.js Runtime for route handlers that need Supabase admin client
- Set `NEXT_PUBLIC_` prefix only for values safe to expose to the browser
- Use Vercel environment variables — never `.env` files in production
- Enable Vercel Analytics and Speed Insights on the dashboard

**`middleware.ts` pattern:**

```ts
import { createMiddlewareClient } from '@supabase/auth-helpers-nextjs'
import { NextResponse } from 'next/server'
import type { NextRequest } from 'next/server'

export async function middleware(req: NextRequest) {
  const res = NextResponse.next()
  const supabase = createMiddlewareClient({ req, res })
  const { data: { session } } = await supabase.auth.getSession()

  if (!session && req.nextUrl.pathname.startsWith('/dashboard')) {
    return NextResponse.redirect(new URL('/login', req.url))
  }

  return res
}

export const config = {
  matcher: ['/((?!_next/static|_next/image|favicon.ico).*)'],
}
```

---

## Red Flags

- `"use client"` at the top of a page or layout
- `useEffect` for data fetching (use Server Components instead)
- Secrets in `NEXT_PUBLIC_` variables
- `fetch()` inside a loop (causes waterfall — use `Promise.all`)
- Missing `revalidatePath` after a mutation
- Route handlers doing what Server Actions could do
