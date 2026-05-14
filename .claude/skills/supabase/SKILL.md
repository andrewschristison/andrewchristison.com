---
name: supabase
description: 'Supabase best practices for this project. Use when designing tables, writing RLS policies, implementing auth, creating edge functions, or setting up realtime. Covers row-level security, multi-tenancy patterns, and Supabase + Next.js integration.'
license: MIT
metadata:
  author: dojo-admin
  version: "1.0.0"
---

# Supabase Best Practices — Dojo Admin

Supabase is the data layer for Dojo Admin. Every pattern here prioritises security, correctness, and multi-tenant isolation.

## Core Principle

**RLS is not optional.** Every table that contains user data must have Row Level Security enabled with policies that scope reads and writes to the authenticated user's dojo. No table should ever be accessible without auth.

## Scoring

**Goal: 10/10.** When designing database schemas, RLS policies, or Supabase integrations, rate it 0-10. A 10/10 means all tables have RLS, auth is handled via Supabase helpers (not custom JWTs), and no service role key is exposed to clients.

---

## 1. Database Schema Conventions

### Naming
- Tables: `snake_case` plural nouns (`students`, `payments`, `attendance_records`)
- Columns: `snake_case` (`created_at`, `dojo_id`, `belt_level`)
- Primary keys: `id UUID DEFAULT gen_random_uuid()`
- Timestamps: always include `created_at TIMESTAMPTZ DEFAULT NOW()` and `updated_at TIMESTAMPTZ DEFAULT NOW()`
- Foreign keys: `<table_singular>_id` (e.g., `student_id`, `dojo_id`)

### Core Tables

```sql
-- Dojos (tenant root)
CREATE TABLE dojos (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  owner_id UUID NOT NULL REFERENCES auth.users(id),
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Profiles (extends auth.users)
CREATE TABLE profiles (
  id UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
  dojo_id UUID REFERENCES dojos(id),
  full_name TEXT,
  role TEXT CHECK (role IN ('owner', 'instructor', 'admin')),
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Students
CREATE TABLE students (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  dojo_id UUID NOT NULL REFERENCES dojos(id) ON DELETE CASCADE,
  full_name TEXT NOT NULL,
  email TEXT,
  phone TEXT,
  belt_level TEXT CHECK (belt_level IN ('white','yellow','orange','green','blue','brown','black')),
  active BOOLEAN DEFAULT TRUE,
  joined_at DATE DEFAULT CURRENT_DATE,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Updated at trigger (apply to all tables)
CREATE OR REPLACE FUNCTION update_updated_at()
RETURNS TRIGGER AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER students_updated_at
BEFORE UPDATE ON students
FOR EACH ROW EXECUTE FUNCTION update_updated_at();
```

---

## 2. Row Level Security

Enable RLS on every table. Write policies that are as restrictive as possible.

```sql
-- Enable RLS
ALTER TABLE students ENABLE ROW LEVEL SECURITY;
ALTER TABLE dojos ENABLE ROW LEVEL SECURITY;
ALTER TABLE payments ENABLE ROW LEVEL SECURITY;

-- Helper function to get the authenticated user's dojo_id
CREATE OR REPLACE FUNCTION auth_dojo_id()
RETURNS UUID AS $$
  SELECT dojo_id FROM profiles WHERE id = auth.uid()
$$ LANGUAGE SQL SECURITY DEFINER STABLE;

-- Students: dojo-scoped
CREATE POLICY "dojo members can read their students"
ON students FOR SELECT
USING (dojo_id = auth_dojo_id());

CREATE POLICY "dojo owners and admins can insert students"
ON students FOR INSERT
WITH CHECK (
  dojo_id = auth_dojo_id()
  AND EXISTS (
    SELECT 1 FROM profiles
    WHERE id = auth.uid()
    AND role IN ('owner', 'admin')
  )
);

CREATE POLICY "dojo owners and admins can update students"
ON students FOR UPDATE
USING (dojo_id = auth_dojo_id())
WITH CHECK (
  EXISTS (
    SELECT 1 FROM profiles
    WHERE id = auth.uid()
    AND role IN ('owner', 'admin')
  )
);
```

**Rules:**
- Never use `USING (TRUE)` or `WITH CHECK (TRUE)` — these disable filtering
- Always test policies as a non-admin user in the Supabase dashboard
- Write separate SELECT, INSERT, UPDATE, DELETE policies — don't use FOR ALL unless intentional
- Use `SECURITY DEFINER` functions sparingly and only for safe helper queries

---

## 3. Auth Integration with Next.js

Always use the official Supabase auth helpers for Next.js:

```bash
npm install @supabase/auth-helpers-nextjs @supabase/supabase-js
```

**Client hierarchy:**

| Context | Client | Use for |
|---------|--------|---------|
| Server Component | `createServerComponentClient` | Data fetching in RSC |
| Server Action | `createServerActionClient` | Mutations in server actions |
| Route Handler | `createRouteHandlerClient` | API routes, webhooks |
| Client Component | `createClientComponentClient` | Realtime, auth state |
| Middleware | `createMiddlewareClient` | Auth guards |

**Never:**
- Share a single Supabase client instance across requests
- Use the service role key in Client Components
- Manually set cookies for auth — let the helpers handle it

---

## 4. Edge Functions

Use Edge Functions for:
- Stripe webhook processing
- Email sending (Resend, Postmark)
- Complex server-side computations that need isolation
- Scheduled jobs (via `pg_cron` or external cron)

```ts
// supabase/functions/process-payment/index.ts
import { serve } from 'https://deno.land/std@0.177.0/http/server.ts'
import { createClient } from 'https://esm.sh/@supabase/supabase-js@2'
import Stripe from 'https://esm.sh/stripe@12'

serve(async (req) => {
  const stripe = new Stripe(Deno.env.get('STRIPE_SECRET_KEY')!, {
    apiVersion: '2023-10-16',
  })

  const signature = req.headers.get('stripe-signature')!
  const body = await req.text()

  const event = stripe.webhooks.constructEvent(
    body,
    signature,
    Deno.env.get('STRIPE_WEBHOOK_SECRET')!
  )

  const supabase = createClient(
    Deno.env.get('SUPABASE_URL')!,
    Deno.env.get('SUPABASE_SERVICE_ROLE_KEY')!
  )

  // Handle event...

  return new Response(JSON.stringify({ received: true }), {
    headers: { 'Content-Type': 'application/json' },
  })
})
```

---

## 5. Realtime

Use Supabase Realtime for live updates to the dashboard:

```tsx
'use client'
import { createClientComponentClient } from '@supabase/auth-helpers-nextjs'
import { useEffect, useState } from 'react'

export function LiveStudentCount({ initial }: { initial: number }) {
  const [count, setCount] = useState(initial)
  const supabase = createClientComponentClient()

  useEffect(() => {
    const channel = supabase
      .channel('student-changes')
      .on(
        'postgres_changes',
        { event: '*', schema: 'public', table: 'students' },
        () => {
          // Refetch count on any change
          supabase
            .from('students')
            .select('count', { count: 'exact', head: true })
            .then(({ count }) => setCount(count ?? 0))
        }
      )
      .subscribe()

    return () => { supabase.removeChannel(channel) }
  }, [supabase])

  return <span>{count}</span>
}
```

---

## 6. Performance

- Use `select('specific, columns')` — never `select('*')` in production
- Add indexes on frequently queried columns: `dojo_id`, `active`, `created_at`
- Use `{ count: 'exact', head: true }` for count queries — no data transfer
- Cache static/infrequent queries at the application layer with `unstable_cache`
- Use `abortSignal` for cancellable fetches

```sql
-- Recommended indexes
CREATE INDEX students_dojo_id_idx ON students(dojo_id);
CREATE INDEX students_active_idx ON students(active) WHERE active = TRUE;
CREATE INDEX payments_student_id_idx ON payments(student_id);
CREATE INDEX payments_created_at_idx ON payments(created_at DESC);
```

---

## 7. Local Development

```bash
# Install Supabase CLI
brew install supabase/tap/supabase

# Start local Supabase
supabase start

# Apply migrations
supabase db push

# Open Studio
supabase studio

# Stop
supabase stop
```

Use `supabase/migrations/` for all schema changes — never edit the database directly in production. Every schema change is a migration file.
