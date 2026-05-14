# Refactoring

## Core Idea

*Refactoring* by Martin Fowler is the practice of improving the internal structure of existing code without changing its observable behaviour. The key word is *without* — a refactoring that changes what the code does is not a refactoring, it is a bug fix or a feature. Keeping these activities separate is what makes refactoring safe.

Refactoring answers a question that most developers never ask: *why does this code feel hard to change?* The answer is almost always one of a small set of recurring patterns — code smells — that have known remedies.

---

## The Two Hats

Fowler's most important practical rule: never wear both hats at once.

- **Adding functionality hat:** add new code; don't restructure existing code; tests turn green on new behaviour
- **Refactoring hat:** restructure existing code; don't add new behaviour; tests stay green throughout

Switching between hats is fine. Wearing both simultaneously is how bugs are introduced in code that was "just being cleaned up."

**In practice:** before starting a refactoring, run the tests and confirm they pass. Run them again after every mechanical step. If they break, you changed behaviour — undo immediately, don't debug.

---

## Code Smells

Smells are surface indicators of deeper design problems. They don't require immediate action, but they signal that refactoring is likely to pay off.

### Long Method
A method that does more than one thing. The fix is always Extract Function. If a function requires a comment to explain a section, that section wants to be a named function.

```ts
// Smell: one function doing three things
async function handleSaveStudent() {
  // validate fields
  if (!firstName.trim()) { ... }
  // build payload
  const payload = { first_name: firstName, ... }
  // insert to Supabase
  const { error } = await supabase.from('students').insert(payload)
}

// Refactored: each concern named
function validateStudentFields(): string | null { ... }
function buildStudentPayload(): StudentInsert { ... }
async function insertStudent(payload: StudentInsert) { ... }
```

### Long Parameter List
More than three parameters is a smell. Pass an options object instead — it names the parameters at the call site and doesn't break callers when you add a new option.

```ts
// Smell
function sendMessage(studentId, templateId, channel, urgent, familyId) { ... }

// Refactored
function sendMessage(options: SendMessageOptions) { ... }
```

### Duplicate Code
The same or very similar code in two or more places. Violates DRY. The fix depends on where the duplication lives: Extract Function (same class), Pull Up Method (sibling classes), or Form Template Method (parallel algorithms).

**In DojoFlow context:** the contact resolution logic (`parent_email` vs `family.primary_contact_email` vs `student.email`) appears in at least three places. Each copy is a future divergence point.

### Feature Envy
A function that seems more interested in data from another class than its own. It's reaching across a boundary it shouldn't cross.

```ts
// Smell: this function in a component knows too much about the student domain
function getDisplayName(student) {
  return student.first_name || student.legal_first_name || 'Unknown'
}
// Fix: move to a student utility or the Student domain object
```

### Data Clumps
Groups of data that travel together everywhere — if you see three variables always passed together, they want to be a single object.

```ts
// Smell: these four always travel together
function createFamily(name, contactFirst, contactLast, contactEmail) { ... }

// Refactored
interface FamilyContact { firstName: string; lastName: string; email: string }
function createFamily(name: string, contact: FamilyContact) { ... }
```

### Primitive Obsession
Using primitive types (strings, numbers) for domain concepts that have their own rules. A belt level is not just a string — it has an ordering, valid values, and display rules. An email address is not just a string — it has a format constraint.

```ts
// Smell: string used everywhere for belt
function isEligible(beltLevel: string, classCount: number): boolean { ... }

// Better: newtype or enum captures the domain constraint
type BeltLevel = typeof BELT_OPTIONS[number]['value']
function isEligible(beltLevel: BeltLevel, classCount: number): boolean { ... }
```

### Switch Statements / Long Conditionals
A conditional that switches on type is usually a missing polymorphism opportunity. When you see the same `if/switch` pattern in multiple places, Extract Function at minimum; consider Replace Conditional with Strategy if the same switch appears more than twice.

### Comments
Not all comments are smells — comments explaining *why* are valuable. But comments explaining *what* the code does are a smell: extract the code into a function and name it so the comment is unnecessary.

---

## The Refactoring Catalog

### Extract Function
Pull a block of code into a named function. The most common refactoring. Use it whenever:
- A section of code could have a descriptive name
- A comment explains what a block does
- A function is longer than ~15 lines

### Inline Function
The inverse: when a function's body is as clear as the function's name, inline it. Don't extract for its own sake — only when the name adds clarity.

### Extract Variable
Pull a complex expression into a named variable. Makes the expression readable and allows reuse without re-evaluation.

```ts
// Before
if (student.last_attendance && differenceInDays(new Date(), parseISO(student.last_attendance)) >= 14) { ... }

// After
const daysSinceAttendance = differenceInDays(new Date(), parseISO(student.last_attendance))
const isAtRisk = daysSinceAttendance >= AT_RISK_THRESHOLD_DAYS
if (isAtRisk) { ... }
```

### Move Function / Move Field
When a function or field is more about the data in another module than its current home, move it. The test: does this function use more data from module A than module B? It belongs in A.

### Replace Temp with Query
A temp variable that's computed from other data can often be replaced with a function call. Makes the computation reusable and keeps the code declarative.

### Introduce Parameter Object
When a group of parameters always travel together, replace them with a single object. Documents the relationship and makes adding new parameters non-breaking.

### Replace Conditional with Polymorphism
When the same conditional logic appears in multiple places to handle different types, replace with a strategy pattern or discriminated union. The conditional moves into the type system.

### Separate Query from Modifier
Functions that both return a value and have a side effect (Command/Query Separation). Split them: the query returns a value with no side effects; the command changes state and returns nothing.

---

## When to Refactor

### The Rule of Three
First time: do it. Second time: note the duplication. Third time: refactor.

### Preparatory Refactoring
Before adding a feature, refactor to make the feature easy to add. "It's like I want to go 100 miles east but instead of just driving east, I take the time to turn the car so it's pointing east." — Fowler.

### Comprehension Refactoring
When reading code, refactor as you understand it. Rename a confusing variable; extract a nested condition. The code is clearer for the next reader (including yourself in six months).

### Opportunistic Refactoring (Boy Scout Rule)
Leave the code cleaner than you found it. Not a dedicated sprint — a small improvement every time you pass through. Compounded across every PR, this prevents rot.

---

## Common Failure Modes

- **Refactoring without tests** — no safety net; you can't know if you changed behaviour; don't refactor code that has no tests without adding tests first
- **Big-bang refactor** — rewriting everything at once; no incremental path; high risk of regression; always refactor in small, reversible steps
- **Renaming as refactoring** — renaming everything without fixing design; changes the surface without changing the structure; still smells the same
- **Refactoring during a feature** — wearing both hats; the change "just to clean up" becomes the source of a regression that's hard to attribute
- **Over-extraction** — extracting every two-line block into a function; adds indirection without adding clarity; extraction is only valuable when the name is clearer than the code
- **Ignoring the smell** — noticing duplication and moving on; the third time you touch duplicated code you will regret not fixing it the second time

---

## Applied to DojoFlow

High-value refactoring targets (in priority order):

1. **Contact resolution logic** — the adult/minor/linked/unlinked email resolution appears in multiple places; Extract Function into `resolveContactEmail(student, family)` in `src/lib/contacts.ts`; one change point for a critical domain rule

2. **`handleSave` in `StudentSheet`** — currently ~80 lines covering validation, payload construction, Supabase insert, error handling, and sync prompt; Extract Function for `validateStudentFields`, `buildStudentPayload`, and `insertStudent`; each becomes independently testable

3. **Segment filter logic in `useBroadcast`** — the per-segment filtering conditions are long conditionals that duplicate threshold values; Extract the threshold constants and the filter functions; Replace the inline conditions with named predicates (`isAbsent2Weeks`, `isTrialWithoutFollowup`)

4. **Belt eligibility computation** — the stripe/eligibility logic appears inline in the belt management view; Extract into `getBeltReadiness(student, promotionHistory)` returning a typed result; components become dumb renderers of domain state

**Refactoring rule for DojoFlow:** never refactor a file you haven't just read. Never refactor and add a feature in the same commit. Always confirm tests are green before and after.
