# Continuous Discovery

## Core Idea

Product discovery is not a phase — it's a rhythm. Teams that do a big discovery sprint at the start and then build for 6 months are building on stale assumptions. The best teams maintain a weekly cadence of customer conversations, treat every conversation as an opportunity to test assumptions, and connect insights directly to build decisions.

Teresa Torres's framework: opportunity solution trees + weekly customer interviews + small assumption tests run in parallel with delivery.

---

## The Opportunity Solution Tree

A structured way to connect the product outcome → opportunities → solutions → experiments.

```
Outcome: Reduce student churn (keep every student progressing)
├── Opportunity: Instructor doesn't know a student is at risk until they're already gone
│   ├── Solution: Absence risk indicator on Programs page
│   ├── Solution: Dashboard KPI tile "students at risk"
│   └── Solution: Automated weekly at-risk email digest to instructors
├── Opportunity: Follow-up is too much friction (composing an email takes 10 min)
│   ├── Solution: Magic Text draft-on-click for absent students
│   └── Solution: One-click re-engagement template
└── Opportunity: Student doesn't feel seen/progressing
    ├── Solution: Progress milestone messages
    └── Solution: Belt test reminder to student and family
```

The tree prevents "solution tourism" — jumping to solutions without mapping them to real opportunities. It also prevents local optimization: solving small problems while the big opportunity (instructor doesn't know who's at risk) goes unaddressed.

---

## The Weekly Interview Cadence

Goal: one customer interview per week, minimum. Not always a formal sit-down — a 15-minute call works.

**What to ask:** (see also: Mom Test skill)
- "Walk me through the last time [trigger situation] happened."
- "What did you do? What tools did you use?"
- "What was the hardest part?"
- "What happened next?"

**What not to ask:**
- "Would you use a feature that does X?" (hypothetical, unreliable)
- "Do you like this idea?" (validation-seeking, gets polite answers)

**What to listen for:**
- The moment of frustration (push force in JTBD)
- The workaround they've invented (a workaround is a solution in disguise)
- The comparison to something else ("it's like what I do in Excel but...")
- The thing they wish existed, described in terms of outcomes ("I just want to know every Monday who I should check in on")

---

## Assumption Testing

For every solution you're considering, list the assumptions it depends on. Test the riskiest ones before building.

**Assumption types:**
- **Desirability** — do customers want this?
- **Usability** — can customers use this without help?
- **Feasibility** — can we build this with what we have?
- **Viability** — is there a business model here?

Small tests:
- Show a screenshot and watch their reaction (desirability)
- Give them a prototype and watch them click without guiding them (usability)
- Prototype with mock data before wiring up the real DB (feasibility proxy)
- Ask "what would this be worth to you?" without proposing a price (viability)

---

## Story Mapping

When translating insights into a backlog, story mapping keeps the user journey visible:
1. Write the user's activity across the top (not features — activities: open app → check who's at risk → reach out)
2. Under each activity, list the tasks that make it up
3. Draw a line: above = MVP, below = later
4. The line should represent a working system, not a feature list

---

## Common Failure Modes

- **Interview theater** — doing interviews to feel like you're doing discovery, but not changing any decisions based on what you hear
- **Confirmation bias** — interviewing customers who you know like the product; ignoring the ones who left
- **Jumping to solutions** — hearing a problem and immediately proposing a feature; this shuts down the interview
- **Too much synthesis, not enough action** — building elaborate opportunity trees but never testing any assumptions
- **Losing the thread** — accumulating insights in a doc nobody reads; insights need to connect to decisions

---

## Applied to DojoFlow

Current state (Mar 2026): White Crane pilot is the primary discovery vehicle. Grandmaster and Master's feedback in March = the most valuable interview data in the product's history.

Key insights already captured:
- Core JTBD: "keep every student progressing so none leave silently"
- Stripe deprioritized: "too close to a busy period" — reveals seasonal sensitivity to new tools
- Email flagged as highest-leverage: "we send zero emails currently" — huge gap in their practice

Discovery to do next:
- What does "a student leaving silently" actually look like from the instructor's side? (interview the moment)
- What do they do today when a student misses 2 weeks? (current behavior = the workaround to beat)
- What would they actually do if they saw an absence alert? (test before building the automation)
