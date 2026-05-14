# Lean Startup

## Core Idea

Every product decision is a hypothesis. Build the minimum thing needed to test it, measure whether the hypothesis was right, and learn before building more. The goal is not to execute a plan — it's to find a plan that works before you run out of time and money.

The Build-Measure-Learn loop is the unit of work, not the sprint or the feature.

---

## The Validated Learning Loop

1. **Identify the riskiest assumption** in your current plan
2. **Design the smallest experiment** that would validate or invalidate it
3. **Build the MVP** — minimum viable product to run the experiment (often not code)
4. **Measure the signal** (behavior, not opinions — what people do, not what they say)
5. **Learn and decide** — persevere, pivot, or kill

Most teams skip steps 1 and 2 and go straight to building. Then they can't tell if the thing they built is working because they never defined what "working" meant.

---

## The MVP Principle

An MVP is not a bad version of the product. It's the smallest thing that:
- Delivers real value to real users
- Tests your riskiest assumption
- Teaches you something you couldn't learn any other way

Common MVP forms:
- **Concierge MVP** — do the job manually for one customer before automating it (validate demand before building)
- **Wizard of Oz MVP** — the user thinks it's automated; you're doing it by hand (Magic Text is almost this — Claude generates, human reviews)
- **Landing page + waitlist** — test whether people want the thing before building it
- **Feature flag for one user** — ship to one customer and watch them use it

What an MVP is NOT: a buggy v1 with all planned features half-done.

---

## Innovation Accounting

Three stages of a startup learning loop:
1. **Establish a baseline** — measure current metrics with the MVP
2. **Tune the engine** — make small changes and measure whether they move the metrics
3. **Pivot or persevere** — if the metrics aren't moving after reasonable effort, the hypothesis is wrong

The trap: teams measure "vanity metrics" (page views, features shipped, signups) instead of "actionable metrics" that indicate whether the core hypothesis is true.

For DojoFlow: the core metric is **student retention rate** (or a proxy like: of students who were absent 2+ weeks and received a follow-up, what % returned?). Features that don't move that number aren't working.

---

## The Pivot Types

A pivot is not giving up — it's a structured course correction based on learning:
- **Zoom-in pivot** — one feature becomes the whole product (the attendance absence tracker was a feature; maybe it's the product)
- **Customer segment pivot** — the product works, but for a different customer than planned
- **Platform pivot** — from app to API, or vice versa
- **Value capture pivot** — changing how you make money (per-seat → per-school flat fee)
- **Technology pivot** — same job, different technology stack

The test: does the new direction better serve a real customer's real job?

---

## Common Failure Modes

- **Premature scaling** — hiring, building infrastructure, or acquiring customers before finding product-market fit
- **Vanity metrics** — measuring things that look good but don't indicate whether the hypothesis is true
- **The "just one more feature" trap** — adding features instead of testing whether the current ones work
- **Ignoring qualitative feedback** — treating everything as an A/B test; sometimes the right move is to talk to five customers
- **Building the vision** — building toward the 3-year roadmap instead of the next validated step
- **Fake MVP** — calling something an MVP because it's small, but never defining what it's supposed to test

---

## Applied to DojoFlow

Current state (Mar 2026): White Crane pilot is a concierge/Wizard of Oz MVP. The sensei is using the tool manually, and feedback is direct.

Key hypotheses to test:
1. If we surface absent students prominently, instructors will reach out more — **test:** does the absence risk indicator on Programs lead to follow-up emails?
2. If Magic Text drafts a message, instructors will send it — **test:** open rate / send rate on drafted messages
3. If we send automated absence follow-ups, students return more — **test:** return rate for students who got an email vs. those who didn't

Don't build Stripe until hypothesis 1 is proven. The pilot explicitly said payments can wait — that's a Lean Startup insight: the retention problem is more urgent than the billing problem.
