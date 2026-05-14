# Influence Psychology

## Core Idea

People make decisions through mental shortcuts — heuristics built over millions of years of social evolution. *Influence* by Robert Cialdini identifies six of these principles and explains how they operate automatically, often below conscious awareness. Understanding them is not about manipulation; it's about designing experiences and communications that align with how humans actually decide.

Used honestly, these principles reduce friction between a genuinely good product and the decision to adopt it. Misused, they erode trust the moment the customer feels the gap between promise and reality.

---

## The Six Principles

### 1. Reciprocity — Give first
When someone gives us something, we feel obligated to give back. This is one of the most universal social norms across cultures and contexts.

**Genuine application:**
Give real value before asking for anything. Not a demo request disguised as a free resource — actual value the prospect can use regardless of whether they become a customer.

**DojoFlow applications:**
- Publish a practical guide: "How to spot the 3 students most likely to leave your dojo this month" — useful whether or not they use the product
- During the pilot: proactively share an insight ("you have 4 students who haven't attended in 14 days — here they are") before asking for feedback
- Trial onboarding: give a pre-populated dashboard with sample data so the sensei experiences value immediately, before they've done any setup work

**Warning:** Reciprocity must be genuine. A "free" resource that is actually a veiled sales pitch triggers the opposite of reciprocity — resentment.

### 2. Commitment and Consistency — Small yeses lead to big yeses
Once people take a position or make a small commitment, they behave consistently with it. Public commitments are more durable than private ones.

**Genuine application:**
Design onboarding so users make small, meaningful commitments early. Each completed step makes the next one more likely.

**DojoFlow applications:**
- Trial signup: ask the sensei to enter one real student before anything else — they've now committed to the product having real data
- Belt test prompt: "Do you want DojoFlow to track this student's test eligibility going forward?" — a small yes that increases engagement with the belt management feature
- Retention messaging: "You said your goal was to keep every student progressing — here's who needs a message this week" — anchors to their own stated goal

**Onboarding design principle:** Make the first action easy and meaningful, not a form to fill out. The first commitment should feel like progress, not homework.

### 3. Social Proof — What others do guides what we do
In situations of uncertainty, people look to the behavior of others as evidence of the correct action. The more similar the others, the more influential the proof.

**Genuine application:**
Show real examples from real people who closely resemble your target customer. Generic testimonials are weaker than specific, named, detailed ones.

**DojoFlow applications:**
- "White Crane Martial Arts, Washington State — the first dojo to run fully on DojoFlow" is stronger than "dojos across the US"
- Specific outcomes: "After the sensei sent a Magic Text to 4 at-risk students, 3 came back within two weeks" is more compelling than "improves retention"
- When expanding: senseis trust other senseis more than they trust software companies; testimonials should sound like one sensei talking to another

**What not to do:** Fake reviews, inflated user counts, or testimonials from generic "martial arts school owners" with no name or dojo attached. Specificity signals authenticity; vagueness signals fabrication.

### 4. Authority — Expertise reduces uncertainty
People defer to credible experts when they're uncertain. Credentials, track records, and demonstrations of knowledge all signal authority.

**Genuine application:**
Establish credibility through demonstrated expertise, not claimed expertise. Show the reasoning, not just the conclusion.

**DojoFlow applications:**
- The domain model in CLAUDE.md (belt progression rules, contact resolution logic, attendance risk thresholds) is a form of authority — building this level of domain knowledge into the product signals deep understanding of how dojos actually work
- Publishing content that demonstrates expertise in dojo retention: "Why students leave martial arts schools in the first 90 days" — research-backed, specific, useful
- Citing White Crane pilot data specifically: real numbers from a real dojo, not industry averages
- Founder credibility: if the founder has a martial arts background or family connection to a dojo, this is worth stating explicitly

### 5. Liking — People say yes to people they like
We are more likely to be persuaded by people we like. Liking is driven by similarity, familiarity, physical appearance, and genuine compliments.

**Genuine application:**
Be human. Write like a person, not a company. Express genuine enthusiasm for the customer's work. Acknowledge shared values.

**DojoFlow applications:**
- Magic Text should sound like it came from a person who cares, not a marketing automation system — this is already a design principle, and it's correct
- Customer communications from the founder should be personal: name the sensei, reference their specific situation, show you know their dojo
- Onboarding and support language: the tone of a martial arts instructor community, not a SaaS startup
- Shared identity: "We built this because someone in our family runs a dojo" — the liking principle is activated by genuine connection, not manufactured warmth

### 6. Scarcity — Less available, more desirable
Things that are rare or limited in availability are perceived as more valuable. Deadlines, limited quantities, and exclusivity all trigger scarcity.

**Genuine application:**
Use scarcity honestly — only when it reflects reality. False scarcity destroys trust the moment it's discovered, and it always gets discovered.

**Honest scarcity for DojoFlow:**
- Pilot access: "We're accepting 5 dojos into the next pilot cohort — White Crane is the first" — genuine scarcity during early access
- Founder time: "I'm doing onboarding calls personally for the first 10 schools" — genuinely limited
- Beta pricing: "Founding school pricing is available until we exit beta" — a real transition point with a real deadline

**What not to do:** Fake countdown timers, invented "only 3 spots left" messaging, or artificial urgency on a SaaS subscription with unlimited capacity. The martial arts community is small and tight-knit — word of deceptive practices travels.

---

## How to Apply These Principles

Map each principle to your current conversion flow and identify where it is absent or applied badly:

| Stage | Principle to activate |
|-------|----------------------|
| First awareness | Social proof (who else like me uses this?) |
| Trial signup | Liking (do I trust this person/company?) |
| Onboarding | Commitment/consistency (small wins that build investment) |
| Trial-to-paid decision | Authority (do they know this domain?), Reciprocity (what have they already given me?) |
| Referral ask | Liking + Social proof (I trust them; I want my peers to know about this) |

---

## Common Failure Modes

- **Manufactured urgency** — fake deadlines and countdown timers; erodes trust permanently when discovered
- **Social proof inflation** — rounding up user counts, using stock photo testimonials; specificity is the test of authenticity
- **Authority claims without demonstration** — "industry-leading" and "trusted by thousands" without evidence
- **Reciprocity as a transaction** — giving a "free" resource that is clearly a sales pitch; the gift must be genuinely useful
- **Consistency as a trap** — using commitment/consistency to lock users into a direction they'll later regret; they'll churn and never return

---

## Applied to DojoFlow

Influence principles that are already working:
- **Liking:** Magic Text tone is personal and warm; this is correct
- **Authority:** Deep domain model built into the product (belt rules, contact resolution, attendance risk definitions) signals genuine domain expertise

Influence principles to deliberately activate:
- **Reciprocity:** Publish one genuinely useful resource for dojo owners before the product launches publicly
- **Social proof:** Build a detailed White Crane case study — specific numbers, named dojo, before/after workflow — before pitching the next school
- **Commitment:** Redesign trial onboarding so the first action is entering a real student (small commitment) rather than exploring a demo
- **Scarcity:** Pilot cohort framing — "we're working with 5 founding schools" — is authentic and activates scarcity without deception
