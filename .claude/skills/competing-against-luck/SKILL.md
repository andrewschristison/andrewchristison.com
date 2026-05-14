# Competing Against Luck

## Core Idea

*Competing Against Luck* by Clayton Christensen is the definitive theoretical treatment of Jobs-to-Be-Done. Where the companion skill (`jobs-to-be-done`) covers application, this skill covers the underlying theory in depth: why people make the choices they do, what a "job" actually is, and why demographic and psychographic segmentation consistently fails to predict purchase behaviour.

The central claim: customers don't buy products. They hire them to make progress in a specific circumstance. Understanding the circumstance — not the customer — is the key to building products that win reliably rather than by luck.

---

## The Hiring Metaphor

Customers "hire" products to do a job, and "fire" them when a better candidate appears or when the product fails at the job. This framing is not metaphorical decoration — it changes how you investigate customer behaviour.

**The wrong question:** "What kind of customer buys our product?"
**The right question:** "What job were they trying to get done when they hired our product?"

A 54-year-old dojo owner and a 32-year-old dojo owner may have completely different jobs, despite being in the same demographic segment. Conversely, a martial arts school owner and a yoga studio owner may have identical jobs ("don't let students drift away silently") despite being in completely different industries.

Demographics describe who the customer is. Jobs describe what the customer is trying to accomplish. Only jobs predict behaviour.

---

## The Three Dimensions of a Job

Every job has three layers. Most products address only the functional layer.

### 1. Functional Dimension
The practical, tangible task the customer is trying to accomplish.

> "Know which students are at risk of leaving before they actually leave."

This is the job most products try to solve. It's necessary but not sufficient.

### 2. Emotional Dimension
How the customer wants to feel — or wants to avoid feeling — as a result of hiring the product.

> "Feel like a responsible instructor who doesn't let students fall through the cracks."
> "Stop feeling anxious that someone left and I didn't notice until it was too late."

The emotional dimension is often what drives the switch from "this seems useful" to "I need this." A product that nails the functional job but ignores the emotional job feels cold and clinical. The sensei doesn't just want a dashboard — they want to feel like they're doing right by their students.

### 3. Social Dimension
How the customer wants to be seen by others as a result of hiring the product.

> "Be the kind of instructor parents trust to know their child's progress."
> "Be seen by peers as running a professional school, not a side hustle."

The social dimension explains why senseis care about personalised messages more than automated blasts — a personalised message signals attentiveness to the parent, which signals professionalism to the community.

**All three dimensions must be addressed.** A product that solves the functional job while making the user feel anxious or look unprofessional will be fired, no matter how capable it is.

---

## Circumstances Over Demographics

The Job-to-be-Done is defined by circumstances, not by who the customer is. Christensen's formulation:

> **"When [circumstance], I want to [progress], so I can [outcome]."**

The circumstance is the key variable. The same person has different jobs in different circumstances:
- When a student hasn't shown up in two weeks, the sensei wants to send a personal message without spending 20 minutes composing it
- When a belt test is coming up, the sensei wants to know exactly who is ready without manually reviewing attendance logs
- When a parent calls to ask how their child is doing, the sensei wants to answer confidently with real data

These are three different jobs, potentially hired by three different products, held by the same person.

**Design implication:** don't design for personas (the 45-year-old male dojo owner in the Pacific Northwest). Design for circumstances (the moment a student misses their second class in a row).

---

## Job Stories vs User Stories

Traditional user stories describe a role and a feature: *"As a dojo owner, I want attendance tracking so I can know who is present."*

Job stories describe a circumstance, a motivation, and an expected outcome:

> *"When I sit down on Monday morning before the week's classes start, I want to immediately see which students haven't been in for two weeks, so I can reach out before they drift any further."*

The job story captures:
- **When:** Monday morning, before classes — timing and context matter
- **Motivation:** see who's drifting — not "view a report," but a specific concern
- **Outcome:** reach out before further drift — the success state is defined

User stories optimize for feature delivery. Job stories optimize for outcome delivery. The difference determines whether you build the right feature.

---

## The Four Forces

When a customer switches to a new product (or from doing nothing to doing something), four forces are at work:

### Push forces (toward a switch)
The frustrations and inadequacies of the current situation that make the customer want to change.
- "I find out a student quit when their payment fails."
- "I spend an hour every Sunday updating a spreadsheet that's always out of date."

### Pull forces (toward the new solution)
The appeal of the new product — what it promises.
- "I can see exactly who is at risk in one glance."
- "It drafts the message for me — I just review and send."

### Anxiety forces (against a switch)
Fears about the new product or the process of switching.
- "What if I lose all my student data in the migration?"
- "What if it's too complicated and I stop using it after a month?"
- "What if the messages it drafts don't sound like me?"

### Habit forces (against a switch)
The comfort of the familiar, even when it's inadequate.
- "I know how my spreadsheet works."
- "At least I understand what's in it."
- "It's good enough — I don't want to learn a new system."

**Push + Pull must outweigh Anxiety + Habit for a switch to happen.**

If DojoFlow adoption is slow, diagnose which force is dominant before adding features. More features don't reduce anxiety; they may increase it. The right response to strong habit forces is familiarity and simplicity, not capability.

---

## The Non-Consumption Opportunity

The most underexplored competitive space is non-consumption — customers who have a job but are currently doing nothing to address it (or doing it with a workaround so inadequate it barely counts).

Most dojo owners are non-consumers of dojo management software. They have spreadsheets, but the spreadsheet doesn't do the job — it stores data; it doesn't flag risk or draft messages. Their job is being done *badly*, not being done by a competitor.

**This is the largest opportunity.** Competing against Mindbody or Kicksite means winning feature comparisons on a spec sheet. Competing against the spreadsheet means making the cost of the current workaround visible and the value of the switch obvious and low-friction.

The entry bar for non-consumers is: can I trust this to not make things worse? Not: does this have every feature I could want?

---

## What Causes a Job to Change

Jobs are stable. Products change. This is why "continuous improvement" of existing features often fails to drive growth — the job the product was hired for was already being done; improvements to it don't expand the market.

New growth comes from identifying jobs that are currently unserved or underserved:
- Jobs being done with inadequate workarounds (spreadsheet → DojoFlow)
- Jobs that are entirely new due to changed circumstances (WhatsApp group coordination → structured Magic Text)

**For DojoFlow:** the job "prevent silent student churn" is currently served by nothing — most senseis have no systematic process. This is not a better version of what exists; it is a solution to a job that was previously just suffered.

---

## Common Failure Modes

- **Demographic segmentation** — targeting "dojo owners aged 35-55 with 50+ students" instead of "people in the circumstance of noticing a student has gone quiet"
- **Feature-driven roadmaps** — building what customers request rather than what serves the job; requests are constrained by customers' imagination of existing solutions
- **Ignoring the emotional and social dimensions** — building a technically excellent tool that makes the user feel surveilled, overwhelmed, or unprofessional
- **Competing on attributes** — comparing feature lists with Kicksite or Mindbody instead of owning the job more completely
- **Solving for the switching customer** — designing for people who are already shopping for solutions, ignoring the vast non-consumption opportunity
- **Misreading the circumstance** — assuming the job is "manage a dojo" when the actual job at the moment of hire is "don't let that one quiet student disappear like the last one did"

---

## Applied to DojoFlow

**The job DojoFlow is hired for (validated Mar 2026):**
> "When a student starts drifting — missing classes, going quiet — I want to catch it before they disappear and reach out in a way that feels personal, so I can keep every student progressing instead of losing them to silence."

This job has all three dimensions:
- **Functional:** detect absence drift before it becomes departure; send a follow-up in seconds
- **Emotional:** feel like a responsible, attentive instructor who doesn't let students fall through the cracks
- **Social:** be seen by parents and the martial arts community as a school that genuinely cares about each student

**Four forces analysis for White Crane:**
- Push: "We currently send zero emails. We have no way to know who is drifting until they're already gone."
- Pull: "I can see at-risk students immediately and send a real message without writing it from scratch."
- Anxiety: "Will this be too complex? Will I actually use it? Will the messages sound like me?"
- Habit: "We've been using spreadsheets for years. I know how they work."

**Strategy implication:** focus on eliminating anxiety (simple onboarding, natural-sounding Magic Text, low setup cost) and reducing habit strength (show the cost of the current spreadsheet approach explicitly). Adding more features doesn't address either force.
