# Clean Architecture

## Core Idea

Dependencies should point inward. Business rules don't know about the database, the UI, or the framework. If you can swap your database from Postgres to SQLite without touching your domain logic, you're doing it right. If changing a UI field requires touching business logic, something is inverted.

The architecture is named for what it protects: your core domain from the churn of infrastructure decisions.

---

## The Dependency Rule

> Source code dependencies must point only inward — toward higher-level policies.

Layers (outermost to innermost):
1. **Frameworks & Drivers** — React, Supabase client, Postmark, browser APIs
2. **Interface Adapters** — hooks, query functions, form handlers (translate between domain and infrastructure)
3. **Application Use Cases** — what the user actually does (enroll a student, send a follow-up)
4. **Domain Entities** — core business rules (a student can't test until `next_test_eligible_date`, a lapsed student is one with no attendance in 30 days)

Layer 1 can import from Layer 2. Layer 2 can import from Layer 3. Layer 3 can import from Layer 4. **Nothing goes the other way.**

---

## In a React + Supabase SPA

You won't have formal Use Case classes, but the same principle applies:

- **Hooks** (`usePrograms`, `useEnrollStudent`) are your interface adapters — they know about Supabase but return typed domain objects
- **Components** consume hooks; they don't know SQL exists
- **Business logic** (is a student lapsed? is a payment expiring?) lives in hooks or pure utility functions, not in JSX
- **Supabase client** is a detail — it lives in `src/integrations/`, not scattered across components

**Red flags:**
- `supabase.from(...)` inside a component
- SQL-shaped data structures leaked into component props (`student_class_enrollments` vs `enrolledClasses`)
- Business rule hard-coded in a render function (`{attendance < 3 ? 'at risk' : 'ok'}`)

---

## Practical Application

**Naming the boundary:** The boundary between "what the app does" and "how it stores/sends data" is the most important boundary to maintain. In DojoFlow, "enroll a student in a program" is a use case — it should read like a business operation, not a SQL statement. `useEnrollStudent` is right; having a component call two `supabase.from()` queries in sequence is wrong.

**Testing implication:** Domain logic that doesn't touch Supabase is trivially testable. If your lapsed-student filter function takes a list of students and a date, you can test it with raw objects. If it calls the database, you can't test it without a real DB.

**The adapter pattern for mutations:** Mutations should validate and transform input at the boundary, then pass clean domain types inward. The component shouldn't know whether a student is enrolled via `program_enrollments` + `student_class_enrollments` or some future unified table.

---

## Common Failure Modes

- **Fat components** — JSX that contains business logic, data fetching, and presentation all at once
- **Anemic hooks** — hooks that just proxy Supabase with no abstraction; a component still needs to know the DB schema
- **Leaky abstractions** — returning Supabase row types directly instead of mapping to domain types
- **Circular dependencies** — a hook that imports from a component, or a component that imports from a page
- **Over-engineering** — adding formal Use Case classes and Repository interfaces to a 2-person SPA; the principle matters more than the ceremony

---

## Applied to DojoFlow

Current architecture is mostly correct:
- Hooks in `src/hooks/` handle all Supabase queries and mutations
- Components consume hooks; they don't import `supabase` directly (or shouldn't)
- Domain types (`ProgramWithStats`, `BroadcastRecipient`) are defined at the hook layer

Watch for:
- Business rules creeping into components (e.g., computing "is lapsed" inline in JSX)
- `useClasses` returning raw `ClassRow[]` and leaving components to figure out display logic
- Broadcast segment logic (`getSegmentRecipients`) — keep this as a pure function, not tied to the Supabase query shape
