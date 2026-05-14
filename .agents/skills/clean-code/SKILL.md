# Clean Code

## Core Idea

Clean code is code that reads like well-written prose. It does one thing, says what it means, and makes the next developer's job easier — including your future self three months from now. The measure isn't cleverness; it's how quickly a competent reader can understand, change, and trust it.

In a TypeScript/React codebase, clean code compounds. A well-named hook is reused confidently. A muddled one gets duplicated. The mess accretes until every change is a risk.

---

## Naming

Names are the primary documentation of code. If a name requires a comment to explain it, the name is wrong.

**Functions:** name them as verbs that describe what they do, not how.
```ts
// Bad
function process(s: Student) { ... }

// Good
function flagAtRiskStudent(student: Student) { ... }
```

**Booleans:** use `is`, `has`, `can`, `should` prefixes.
```ts
const isEligibleForPromotion = beltTestsDue(student)
const hasOutstandingBalance = student.balance > 0
```

**React components:** noun or noun-phrase; name what they represent, not what they render.
```ts
// Bad
function RenderStudentRow(...) { ... }

// Good
function StudentRow(...) { ... }
```

**Avoid encodings and noise:** no `IStudent`, no `studentData`, no `temp`, no `obj`. Say what the thing is.

**Consistency over cleverness:** if existing code uses `student` not `member`, use `student`. Surprise has a cost.

---

## Functions

**Do one thing.** A function that does one thing can be named cleanly, tested simply, and read in one pass. If you need "and" to describe it, split it.

**Keep them short.** Target under 20 lines. If a function scrolls, it's doing too much.

**Arguments:** 0 is ideal. 1 is fine. 2 is acceptable. 3+ is a smell — consider an options object.
```ts
// Bad
function sendMessage(studentId: string, templateId: string, channel: string, urgent: boolean) { ... }

// Good
function sendMessage(options: SendMessageOptions) { ... }
```

**No side effects in query functions.** A function named `getStudent` should not update state. Command/Query Separation: a function either answers a question or causes a change, not both.

**Prefer returning early** over nested conditions:
```ts
// Bad
function getPromoStatus(student: Student) {
  if (student.active) {
    if (student.attendanceRate > 0.8) {
      return 'eligible'
    }
  }
  return 'ineligible'
}

// Good
function getPromoStatus(student: Student) {
  if (!student.active) return 'ineligible'
  if (student.attendanceRate <= 0.8) return 'ineligible'
  return 'eligible'
}
```

---

## Comments

**Don't comment what the code says — comment why it does what it does.**
```ts
// Bad: restates the obvious
// Check if student is active
if (student.active) { ... }

// Good: explains non-obvious reasoning
// White Crane pilot: instructors consider 14-day absence the point of no return
const AT_RISK_THRESHOLD_DAYS = 14
```

**Delete dead code.** Don't comment it out — git has the history. Commented-out code is noise that erodes trust in the surrounding code.

**TODO comments are fine temporarily.** They become technical debt if they outlive the sprint. Attach a ticket reference if it matters.

---

## Formatting

Formatting is communication. Inconsistent formatting makes readers think there's a reason for the difference.

**Use a formatter and commit the config.** In this project: Prettier + ESLint. Never debate formatting in code review — automate the opinion.

**Vertical proximity:** things that are related should be close together. Functions that call each other should be near each other. The reader should not have to scroll to follow the logic.

**One concept per line.** Avoid horizontal density:
```ts
// Bad
const result = students.filter(s => s.active).map(s => ({ ...s, risk: calcRisk(s) })).sort((a,b) => b.risk - a.risk)

// Good
const activeStudents = students.filter(s => s.active)
const withRisk = activeStudents.map(s => ({ ...s, risk: calcRisk(s) }))
const ranked = withRisk.sort((a, b) => b.risk - a.risk)
```

---

## The Boy Scout Rule

**Leave the code cleaner than you found it.** Not a full refactor — a small improvement: rename a confusing variable, extract a nested condition, delete a stale comment. Compounded across every PR, this prevents rot.

This rule does not mean refactor everything you touch. It means make one small thing better every time you pass through. Don't let perfect be the enemy of slightly better.

---

## Common Failure Modes

- **Abbreviations as names** — `stud`, `mgr`, `cfg` save three keystrokes and cost hours of comprehension
- **Function length creep** — functions grow one `if` at a time until nobody understands the whole thing
- **Comment drift** — a comment that described what the code used to do is worse than no comment (it actively misleads)
- **Inconsistent abstractions** — mixing raw Supabase queries with service-layer calls in the same component
- **Magic numbers** — `if (days > 14)` scattered through the codebase; change the threshold and hunt for every instance

---

## Applied to DojoFlow

The codebase is small now but will grow. Clean code habits established early prevent the rewrite conversation later.

Specific patterns to enforce:
1. **Constants for domain thresholds** — `AT_RISK_DAYS`, `BELT_ELIGIBILITY_RATE` in a shared `constants.ts`
2. **One responsibility per hook** — `useAtRiskStudents` does not also handle sending messages
3. **Service layer for Supabase** — components call `studentService.getAtRisk()` not raw `supabase.from('students').select(...)`
4. **Early returns in components** — loading/error states at the top, happy path at the bottom
5. **Named booleans for readability** — `const showRiskBadge = daysSinceLastAttendance > AT_RISK_DAYS` reads like a sentence
