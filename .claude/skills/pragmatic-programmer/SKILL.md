# Pragmatic Programmer

## Core Idea

The Pragmatic Programmer by Andrew Hunt and David Thomas is not a book about a specific technology. It is a book about the craft of programming — the habits, instincts, and philosophies that separate developers who produce reliable, maintainable software from those who produce technical debt.

The central theme: **take responsibility for your code and your career**. Don't be passive. Don't accept broken windows. Don't ship things you don't understand. Think about what you're building and why.

---

## DRY — Don't Repeat Yourself

Every piece of knowledge should have a single, authoritative representation in the system. Duplication is not just copy-pasted code — it is any situation where the same fact is expressed in two places.

**Types of duplication:**
- **Imposed duplication** — two places that must stay in sync (a TypeScript type and a Supabase column definition that diverge)
- **Inadvertent duplication** — two developers solving the same problem independently
- **Impatient duplication** — copying something because it seems faster than abstracting

**DRY in the DojoFlow context:**
- `AT_RISK_THRESHOLD_DAYS = 14` must exist in one place; if it's in a hook and also in a SQL query and also in a component, you have three representations of one fact — and they will diverge
- Belt stripe logic (12 and 24 classes) must live in a single function; not duplicated across the promotion form, the belt management view, and the readiness badge computation
- Contact resolution rules (adult vs minor, family-linked vs unlinked) are complex enough to be implemented once in a utility and tested there

**The DRY test:** If you change this fact, how many files do you have to touch? If the answer is more than one, you have a DRY violation.

---

## Orthogonality

Two components are orthogonal when changing one does not affect the other. Orthogonal systems are easier to test, easier to debug, and easier to extend.

**The helicopter test:** If you change something in one component, which other components need to change? Orthogonality means: as few as possible.

**In React/TypeScript:**
- A hook that fetches data should not also transform it for display — those are two concerns
- A component that renders a StudentRow should not also contain the logic for deciding whether that student is at risk
- A Supabase Edge Function that drafts a message should not also write to `communications_log` — those are separate responsibilities

**Applied to DojoFlow:**
- `useAtRiskStudents` should return a list of at-risk students and nothing else; it should not trigger side effects, update state, or format output for display
- The contact resolution logic (which email to use for a minor vs adult) is used in multiple places; it should be a pure utility function with no database dependency

---

## Tracer Bullets

When starting a feature, build the thinnest possible end-to-end slice first — something real that touches all layers of the system (UI → hook → Supabase → database) — before adding breadth.

**Why tracer bullets beat big design up front:**
- You discover integration problems early, when they're cheap to fix
- You have something to demonstrate and get feedback on
- You build confidence that the architecture holds before investing in it

**Tracer bullet vs prototype:** A prototype is thrown away. A tracer bullet is production code — the first, thinnest version of the real feature.

**DojoFlow example — Bulk Email feature:**
- Tracer bullet: one compose field, one hardcoded segment ("all active students"), one send — end to end, real Postmark call
- Only after tracer is working: add segment picker, Magic Text assist, sent log, preview step
- The tracer reveals whether Postmark delivery, the Edge Function, and the `communications_log` write all work together before you've built the whole UI

---

## Broken Windows Theory

Don't leave broken windows. A broken window — a bad design decision, a quick hack, a known bug left unfixed — signals that no one cares. That signal spreads. The codebase degrades faster than any single bad decision would explain.

**Broken windows in a TypeScript/React codebase:**
- `any` types that were "temporary" and became permanent
- A console.log left in production code
- A component that handles three concerns because "we'll refactor it later"
- A TODO comment from six months ago that no one remembers
- A test that's been skipped because it's flaky

**The fix:** Fix broken windows when you see them. Not a full refactor — the specific window. Rename the confusing variable. Remove the dead comment. Fix the flaky test. This is the Boy Scout Rule in another form.

**Practical rule:** If a PR review reveals a broken window that can be fixed in under 10 minutes, fix it in the same PR. Don't create a ticket for a 5-minute fix.

---

## Programming by Coincidence

Don't rely on things that work for reasons you don't understand. If code works, know why. If it stops working, know why.

**Signs you're programming by coincidence:**
- You try something, it works, and you ship it without understanding why
- You fix a bug by changing something adjacent to the real problem
- You're not sure what would break if you changed this code

**In a Supabase context:**
- If an RLS policy seems to be working, verify it explicitly — don't assume it's correct because the UI renders
- If a Supabase join returns the expected shape, understand the query — don't copy it from a previous query and assume it will work in this context
- If an Edge Function succeeds, trace exactly what happened — the Postmark response, the database write, the error handling

**Defensive practices:**
- Write the test that would catch the bug you just fixed
- Document the non-obvious constraint next to the code that depends on it
- If you're not sure a thing is safe to change, find out — don't leave it as a black box

---

## Common Failure Modes

- **Passive acceptance** — noticing a broken window and deciding it's someone else's problem
- **Copy-paste programming** — duplicating solutions without understanding them; creates DRY violations and spreads bugs
- **Coincidence in production** — "it works on my machine" shipped because the developer doesn't understand why it works
- **Big-bang integration** — building all layers separately, integrating at the end, discovering incompatibilities when they're expensive to fix
- **Orthogonality ignored** — a change to the billing logic requires touching five components because nothing is separated

---

## Applied to DojoFlow

Current DRY risks to watch:
- `AT_RISK_THRESHOLD_DAYS` (14 days) and `LAPSED_THRESHOLD_DAYS` (30 days) — should be defined once in `src/constants.ts`
- Belt stripe thresholds (12 and 24 classes) — must be the same value in every context that references them
- Contact resolution logic — complex enough to centralize; currently risk of multiple independent implementations

Tracer bullet approach for upcoming features:
- **Contact completeness (Priority 1):** tracer = one warning badge on the Students list for a student with no email; then expand to Families, Dashboard banner, bulk view
- **Bulk email (Priority 2):** tracer = send one email to one hardcoded address end-to-end; then add segment picker, Magic Text, preview

Broken windows to fix:
- Any `any` types in hooks that interact with Supabase join shapes — address at the point of modification, not in a dedicated refactor sprint
- Known RLS policies that haven't been explicitly verified — audit before enabling parent/student role access
