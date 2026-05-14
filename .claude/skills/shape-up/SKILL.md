# Shape Up

## Core Idea

*Shape Up* by Ryan Singer (Basecamp) is a product development methodology built around one insight: projects don't fail because developers are slow. They fail because the work was never properly defined before building started. Vague ideas handed to builders produce vague results — or no results, because the problem turns out to be larger than anyone imagined.

Shape Up separates the work of figuring out what to build (shaping) from the work of building it. Shaping is done by senior people before a cycle starts. Building is done by small teams with full autonomy during a fixed time window. The time window is non-negotiable.

---

## Appetite vs Estimate

The most important reframe in Shape Up: replace estimates with appetite.

**Estimate:** "How long will this take?" — answered by the team doing the work, usually wrong, creates pressure to hit a number.

**Appetite:** "How much time is this worth?" — decided by the person setting priorities, based on the value of the outcome.

An appetite is a budget, not a prediction. "This problem is worth two weeks of one developer's time." If the solution doesn't fit in that budget, you either narrow the scope or don't do it. You don't extend the budget.

**Why this matters:** estimates create the illusion of commitment on a number that was always uncertain. Appetite creates real commitment — to a time box, not a scope. The scope flexes; the time does not.

**For DojoFlow:** before starting any feature, ask "how much is this worth?" not "how long will this take?" Contact completeness (Priority 1) is worth a full focused week. A billing nudge toast is worth two hours. If either takes longer than its appetite, the scope was wrong — not the estimate.

---

## Shaping

Shaping is the work of defining a problem well enough that a builder can make autonomous decisions without constant clarification. A shaped piece of work has:

1. **A problem statement** — what job is currently done poorly, and why does it matter now?
2. **Appetite** — how much time is this worth?
3. **A solution sketch** — rough enough to leave room for builder judgment; specific enough to prevent wasted exploration
4. **Boundaries** — what is explicitly out of scope?

### Fat Marker Sketches
Shaped work is drawn with a fat marker, not a fine-tipped pen. The sketch should communicate the concept without over-specifying layout, copy, or interaction details. Builders fill in those details — that's their creative contribution.

A fat marker sketch of the contact completeness feature would show:
- A warning indicator on the Students list card
- The concept "missing email = amber badge"
- No pixel-perfect wireframe, no exact badge text, no specific icon

Over-specification kills builder ownership and produces resentment. Under-specification (no sketch at all) produces scope creep and rabbit holes.

### Shaped vs Unshaped Work — DojoFlow Examples

**Shaped:**
> "Attendance page: add a Walk-in Trial button that opens a minimal capture form (first name, age group, parent email). Student is created with status=trial. No family linkage at creation time. Two weeks appetite."

**Unshaped:**
> "We should improve the student add flow to support trials better and maybe families too."

The shaped version has a specific solution concept, explicit boundaries (no family linkage), and a time box. The unshaped version will expand to fill any time given to it.

**Shaped:**
> "Contact completeness: add an amber badge to the Students list card for students with no resolvable email. Badge shows 'No email' with a MailX icon. No dashboard tile yet — list only. One week appetite."

**Unshaped:**
> "Surface missing contact info as actionable warnings."

---

## Cycles and Cooldown

Shape Up uses **6-week cycles** followed by **2 weeks of cooldown**.

- **During the cycle:** builders work on shaped projects with no interruptions
- **During cooldown:** no scheduled work; developers fix bugs, explore ideas, write tests, handle small requests; this is where technical debt gets addressed

**Why cooldown matters:** without explicit breathing room, debt accumulates and morale degrades. The cooldown is not slack — it is structural maintenance.

**For a solo founder:** the cycle/cooldown rhythm still applies. Six weeks of focused build on one shaped project. Two weeks of cleanup, exploration, and shaping the next cycle. Don't treat cooldown as more feature time — it will cost you more than it saves.

---

## Circuit Breaker

At the end of a cycle, a project either ships or it doesn't. There is no automatic extension. This is the circuit breaker.

**Why no extensions:** teams that know a deadline will be extended learn to let deadlines slip. Teams that know the deadline is real make hard scope decisions during the cycle, not after it ends.

**What happens when the circuit breaks:**
- The project does not ship
- The time is not refunded or rescheduled
- The team evaluates: was the problem worth solving? Was the solution well-shaped? Should we re-shape it for a future cycle?
- Sometimes the answer is: this problem wasn't as important as we thought

**The circuit breaker prevents:** the half-built feature that lives in production forever, the project that takes 6 weeks and then 6 more, the "almost done" that drains every cycle.

---

## The Hill Chart

Progress is not linear. Work has two distinct phases:

1. **Uphill:** figuring out the approach — solving unknowns, making decisions, eliminating uncertainty
2. **Downhill:** executing on a known plan — straightforward work, known steps

The hill chart visualises this. A task on the left side of the hill has unsolved unknowns. A task on the right side is execution. A task at the top has clarity but no completed work.

**The insight:** most projects stall on the uphill slope — not because of execution problems, but because of unsolved design questions. If a task hasn't moved uphill in a few days, something is stuck. The intervention is not to push harder — it is to identify the unknown and make a decision.

**For DojoFlow:** the hill chart clarifies what "in progress" actually means. "Working on contact completeness" could mean "still figuring out how to handle family-linked minors" (uphill) or "implementing the badge on StudentCard" (downhill). These require different interventions.

---

## Scope Hammering

During a build cycle, the goal is not to implement everything in the shaped pitch. It is to ship something valuable. When time runs short, the builder hammers the scope — cuts nice-to-haves, simplifies edge cases, defers non-essential work.

**The scope hammer questions:**
- Is this part of the core value, or a nice-to-have?
- What's the simplest version that still does the job?
- What can we defer to a later cycle without breaking the current feature?

**Not scope hammering** is how projects become "90% done" and stall. The last 10% is always scope that wasn't hammered.

**DojoFlow scope hammer examples:**
- Contact completeness: ship the Students list badge first; defer the Dashboard tile and Families page banner to the next cycle
- Suggested sends: ship absence_followup and trial_followup; defer belt_test_invitation and event_reminder
- Billing profiles: ship manual profiles; defer Stripe integration indefinitely (already done by pilot feedback)

---

## Common Failure Modes

- **Building unshaped work** — developers start on vague ideas; scope expands; delivery slips; everyone is frustrated
- **Over-shaping** — detailed wireframes and specs that leave no room for builder judgment; the builder becomes an implementer, not a problem-solver
- **Treating appetite as estimate** — "the appetite is two weeks" → "why isn't it done in two weeks?" — the appetite is a budget decision, not a delivery promise
- **Extending the circuit** — "we're almost done, just give us one more week" → repeat indefinitely
- **No cooldown** — jumping from cycle to cycle without cleanup; technical debt and burnout accumulate; the next cycle starts slower than the last one
- **Hill chart theater** — marking everything "downhill" without actually resolving the unknowns; the chart lies; the project stalls

---

## Applied to DojoFlow

Current roadmap (from `CLAUDE.md`) maps well to Shape Up cycles:

**Cycle 1 (shaped, ready to build):**
> Contact completeness — amber badges on Students list and Families list for missing email. Dashboard alert tile "X students have no email." Appetite: 1 week.

**Cycle 2 (needs shaping before building):**
> Bulk segmented email — compose screen with segment picker, subject, body, Magic Text assist, Postmark send. Appetite: 2 weeks. Needs a shaped pitch defining which segments are in scope for v1 and what the send confirmation looks like.

**Unshaped (do not start):**
> Suggested sends queue, attendance analytics, Stripe payments — problems worth solving, but the solution concepts are not specific enough to build from. Shape before scheduling.

**Solo founder Shape Up adaptation:**
- Shaping happens in writing (CLAUDE.md, a brief doc, a rough sketch) before any code opens
- Appetite is set before shaping begins — "this is worth 3 days" constrains the solution
- Cooldown happens: one week in every six is cleanup, not features
- Circuit breaker is personal discipline: if a feature isn't shippable at the appetite boundary, cut scope or stop
