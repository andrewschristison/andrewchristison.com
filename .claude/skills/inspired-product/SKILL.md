# Inspired Product

## Core Idea

Most product teams are feature factories — they take requirements from stakeholders, build them, ship them, and wonder why growth is flat. *Inspired* by Marty Cagan argues that the best products are discovered, not specified. The team's job is to find the right thing to build before committing to building it.

Discovery and delivery are separate activities. Conflating them — jumping straight from idea to sprint — is the root cause of most wasted engineering effort.

---

## Product Discovery vs. Delivery

| Discovery | Delivery |
|-----------|----------|
| Are we solving the right problem? | Are we building it correctly? |
| Cheap to run — prototypes, conversations | Expensive — engineered, tested, deployed |
| High uncertainty → reduce risk first | Low uncertainty → execute well |
| Happens continuously | Happens in sprints/releases |

**The goal of discovery is to validate ideas at 1/10th the cost of building them.**

A two-hour user session with a prototype can kill a two-week feature before it's written. That's the trade to make.

---

## The Four Big Risks

Before committing to any feature, validate against all four risks:

### 1. Value Risk — Will customers actually use it?
The most common failure. Teams build what customers *say* they want, not what they'll *actually use*. Validated by: prototype testing, usage data, genuine enthusiasm (not polite interest).

### 2. Usability Risk — Can customers figure out how to use it?
Especially critical in B2B tools used by non-technical users. A sensei managing a dojo is not a product manager. If it takes training to use, usability failed. Validated by: watched usability sessions, not survey responses.

### 3. Feasibility Risk — Can we actually build this?
Engineers should be involved in discovery, not just delivery. A brilliant idea that requires three months of infrastructure work is not a near-term opportunity. Validated by: engineers in the room during discovery, not handed specs.

### 4. Viability Risk — Does this work for the business?
Legal, financial, support, and go-to-market constraints are real. A feature that creates a support burden larger than its revenue is not viable. Validated by: talking to the people who'll operate the business, not just the people who'll use the product.

**All four risks must be addressed before a feature enters delivery.** If you're not sure which risk killed a feature in hindsight, it was probably value risk.

---

## Outcome Over Output

Output is features shipped. Outcome is behaviour changed.

- **Output:** "We shipped bulk email."
- **Outcome:** "Senseis now reach out to at-risk students before they leave, reducing churn by 20%."

Teams measured on output ship things. Teams measured on outcomes build things that matter.

**For every feature, define the outcome before the output:**
- What user behaviour changes?
- How will we measure it?
- What does success look like in 30 days?

If you can't answer these, you're optimising for output.

---

## Continuous Customer Contact

Product managers (and in early-stage products, founders) should be talking to customers every week. Not quarterly discovery sprints — continuous contact.

**The minimum:** one substantive customer conversation per week. Not a support call. A conversation where you learn something about their world.

What to listen for:
- The narrative around when they started looking for a solution
- Frustration with current behaviour (not feature requests — frustration)
- Workarounds they've invented (every workaround is an unmet job)
- What they *don't* mention (often as important as what they do)

Cagan's warning: **customers don't know what's possible.** Their requests are constrained by their imagination of existing solutions. Your job is to understand the problem deeply enough to invent a better solution than the one they described.

---

## The Product Team Structure That Works

The empowered product team:
- **Product manager** — owns the problem, defines outcomes, talks to customers
- **Designer** — owns the experience, prototypes solutions, runs usability tests
- **Engineer(s)** — own the feasibility and architecture, involved in discovery

Each owns their domain; none are order-takers. The PM does not hand designs to engineers. The designer does not hand specs to the PM.

In a solo/early-stage context (like DojoFlow now): the founder plays all three roles simultaneously. The risk is skipping discovery because it feels like overhead. It isn't — it's the only thing that prevents building the wrong product.

---

## Common Failure Modes

- **Stakeholder-driven roadmaps** — building what was asked for, not what was discovered
- **Discovery theater** — running user interviews but not changing what you build based on them
- **Big-bang delivery** — waiting until fully built to validate; by then the feedback is expensive to act on
- **Usability optimism** — "users will figure it out" is not a usability strategy
- **Ignoring viability** — the feature that marketing loves but support can't sustain
- **Output metrics** — measuring velocity instead of outcomes; the team learns to ship faster, not better

---

## Applied to DojoFlow

DojoFlow is in discovery for most of its feature set. The White Crane pilot is the primary discovery vehicle.

Current validation status (Mar 2026):
- **Value risk resolved:** "reduce silent churn" is confirmed as the core job; pilot sensei engaged
- **Usability risk open:** no watched usability sessions yet; sensei hasn't used it solo without help
- **Feasibility risk mostly resolved:** core stack is working
- **Viability risk partially open:** pricing and support model TBD

Discovery priorities:
1. Watch White Crane sensei use contact completeness and Magic Text without assistance
2. Validate that "suggested sends queue" feels like help, not homework
3. Understand how belt test prep currently works before building analytics around it

The temptation will be to ship features faster as the pilot progresses. Resist it. One well-validated feature used daily beats five speculative features used never.
