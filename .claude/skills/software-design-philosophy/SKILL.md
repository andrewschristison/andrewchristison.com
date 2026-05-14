# Software Design Philosophy

## Core Idea

*A Philosophy of Software Design* by John Ousterhout argues that the primary goal of software design is to reduce complexity. Not to add features faster, not to optimize performance, not to follow patterns — to reduce the complexity that makes software hard to understand and change.

Complexity is the root cause of almost every software problem. It makes modification risky, bugs hard to find, and onboarding slow. The designer's job is to fight it at every decision point, knowing it accumulates faster than it is removed.

Complexity has two forms: **cognitive load** (how much you need to understand to work with this) and **change amplification** (how many places you must touch to make a single change). Both are enemies.

---

## Deep vs Shallow Modules

The most useful modules are **deep**: a small, simple interface that hides a large amount of implementation complexity. The worst modules are **shallow**: a complex interface that provides almost no abstraction over the implementation.

**Deep module:** hides complexity behind a simple API
```ts
// Deep: caller needs to know nothing about contact resolution logic
const email = resolveContactEmail(student, family)

// The implementation handles adult/minor, family-linked/unlinked,
// null date_of_birth, and the priority order — none of this leaks
```

**Shallow module:** the abstraction buys nothing
```ts
// Shallow: this is just a rename of supabase.from(...)
const getStudents = () => supabase.from('students').select('*')
// Caller still needs to know the table name, shape, and RLS behaviour
```

**The interface/implementation ratio:** A deep module has a large ratio of implementation complexity to interface complexity. A shallow module has a ratio close to 1 — no abstraction is happening.

**Applied to DojoFlow:**
- A `resolveContactEmail(student, family)` utility is deep: it hides the complex contact resolution rules from every caller
- A `studentService.getAtRiskStudents()` is deep: it hides the 14-day threshold, the all-class attendance check, and the Supabase query from every component that needs the list
- A hook that wraps a single Supabase query without adding any logic is shallow — consider whether it's worth the indirection

---

## Tactical vs Strategic Programming

**Tactical programming:** get it working, as fast as possible, deal with design later. This is the dominant mode in fast-moving products. It produces working software and accumulating complexity.

**Strategic programming:** invest a small amount of extra time in every change to keep the design clean. This is slower in any individual change and faster across all subsequent changes.

The tactical approach feels like it's saving time because each individual shortcut is small. The cost compounds across hundreds of small decisions until the codebase resists change.

**The investment mindset:** Ousterhout suggests spending 10–15% of development time on design investment — not refactoring sprints, but a small premium on every feature: naming things well, writing the module's interface before its implementation, simplifying before shipping.

**For DojoFlow at the current stage:** the codebase is small enough that strategic investments are cheap. The patterns established now persist through scale. A shallow abstraction written today becomes a component that every future developer copies.

---

## Information Hiding

The most important design principle: hide information that isn't necessary for callers to know. Every piece of information exposed in an interface is a dependency that callers can take on.

**What to hide:**
- Implementation details (how the query is constructed, which table is involved)
- Configuration (threshold values, business rules)
- Data representation (database column names, raw Supabase types)

**What to expose:**
- The result the caller needs
- The errors that the caller must handle
- The inputs that genuinely vary by caller

**Applied to DojoFlow:**
- Components should not know that `AT_RISK_THRESHOLD_DAYS = 14`; they should call `isAtRisk(student)` and get a boolean
- API routes and Edge Functions should not expose raw database errors to the client; map them to typed error responses
- The belt stripe logic (12/24 classes) should not be scattered across components; it belongs in a single utility that is called everywhere

**The test:** if you change the implementation, how many files break? If the answer is more than the number of files you expected to change, information is leaking.

---

## The Importance of Naming

Names are the primary interface between the developer and the code. A good name eliminates the need to look at the implementation. A bad name forces the reader to read the code to understand what the name meant to say.

**Ousterhout's standard:** a name should be precise enough that you could reconstruct the implementation's purpose without reading it.

**Naming levels:**
1. **Variables:** describe the value they hold, not the type (`atRiskStudents`, not `filteredList`)
2. **Functions:** describe the result returned or the effect produced (`resolveContactEmail`, not `getEmail`)
3. **Modules/hooks:** describe the single responsibility (`useAtRiskStudents`, not `useStudentData`)
4. **Files:** match the primary export exactly; no ambiguity about what's inside

**Naming as a design signal:** If you struggle to name a function, the function is probably doing more than one thing. The difficulty of naming is a symptom of design complexity, not a problem with language.

**DojoFlow examples:**
- `useStudentData` is too broad — what data? all students? one student? with what fields?
- `useAtRiskStudents` is precise — it returns the at-risk students list and nothing else
- `resolveContactEmail(student, family)` names the result (a resolved email) and the inputs (the two things needed to resolve it)

---

## Consistency

Consistency is a form of complexity reduction. When things that are similar look similar, the reader builds a mental model and applies it confidently. When similar things look different, the reader must read each instance carefully.

**What consistency means in practice:**
- If two hooks return data in the same shape, they should use the same naming convention (`{ data, loading, error }`)
- If the codebase uses `camelCase` for function names, every function uses it
- If error handling follows a pattern in one Edge Function, it follows the same pattern in all of them
- If one component uses early returns for loading/error states, all similar components do

**The cost of inconsistency:** a developer who has learned the pattern encounters an exception and must slow down to understand whether the exception is intentional (a real difference in behaviour) or accidental (a different developer who didn't know the convention).

---

## Common Failure Modes

- **Classitis** — creating a class or module for every small operation; shallow modules everywhere; more interfaces than abstraction
- **Premature decomposition** — breaking things into modules before the design is stable; you end up with many small modules that are coupled to each other
- **Temporal coupling hidden in plain sight** — two functions that must be called in order, with nothing in the interface indicating this
- **Leaky abstractions** — callers who need to know implementation details to use a module correctly; the abstraction is lying about what it hides
- **Consistency violations that look like choices** — inconsistent naming or structure that a reader interprets as meaning something when it means nothing

---

## Applied to DojoFlow

Deep module opportunities (currently shallow or nonexistent):
1. **Contact resolution** — `resolveContactEmail(student, family)` encapsulating adult/minor/linked/unlinked logic
2. **At-risk detection** — `isAtRisk(student, attendanceRecords)` returning a boolean; callers don't know the threshold
3. **Belt eligibility** — `getBeltReadiness(student, promotionHistory)` returning a typed readiness object; callers don't know the stripe math

Strategic investments worth making now (before the codebase grows):
- Standardize hook return shapes: every data hook returns `{ data, isLoading, error }`
- Centralize domain constants in `src/constants.ts` before they proliferate into component props and query literals
- Write Edge Function error responses in a consistent typed format before adding more Edge Functions

Design smell to watch: if adding a new page requires changes to more than 2–3 files beyond the page component itself, there is a design coupling problem worth addressing.
