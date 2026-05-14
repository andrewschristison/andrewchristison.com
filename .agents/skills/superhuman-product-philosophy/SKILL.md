# Superhuman Product Philosophy

## Core Idea

Rahul Vohra built Superhuman into a category-defining email product not by surveying the most users or shipping the most features, but by finding a small group of people who would be *very disappointed* without it — and building exclusively for them until that group grew large enough to sustain the business.

The philosophy has three interlocking parts: a rigorous measurement of product-market fit, an obsessive focus on the highest-expectation users, and a product standard where speed is a first-class value rather than an engineering concern. Together they produce a product that a specific kind of user experiences as irreplaceable — and that experience is the only durable competitive advantage.

---

## The 40% Rule

### Why NPS and CSAT Are the Wrong Metrics

Net Promoter Score asks: "Would you recommend this product?" CSAT asks: "Were you satisfied?" Both measure sentiment in a moment, anchored to the user's expectations rather than to the product's indispensability. A user can be satisfied with a product they'd happily abandon tomorrow. A user can be unsatisfied with a product they couldn't function without.

Neither metric captures the thing that actually predicts business survival: whether your product has become something people genuinely depend on.

### The Sean Ellis Question

Sean Ellis identified the right question in 2009: **"How would you feel if you could no longer use this product?"**

Three answer options only:
- **Very disappointed**
- **Somewhat disappointed**
- **Not disappointed** (it doesn't really matter)

The threshold: **if 40% or more of your surveyed users answer "very disappointed," you have product-market fit.** Below 40%, you don't — regardless of what any other metric says.

Why this question works: it measures replacement cost, not satisfaction. A user who would be "very disappointed" has no adequate substitute. That means the product is doing a job nothing else does as well. That is the definition of product-market fit.

### The Follow-Up Questions

The survey should include three follow-up questions:

1. **"What type of person do you think would benefit most from [product]?"**
   — This identifies the user's mental model of the ideal customer. Very disappointed users often describe themselves or their situation accurately. Their description is your positioning brief.

2. **"What is the primary benefit you get from [product]?"**
   — Extract the exact language. Do not paraphrase. The words users choose to describe the benefit they experience are the words your marketing should use. This is the functional job.

3. **"How could we improve [product] for you?"**
   — This question is ONLY valuable when asked of "very disappointed" users. Improvement suggestions from "not disappointed" users are noise — they describe what would make them happier with something they'll abandon anyway.

### How to Read the Results

The 40% is not the only signal. The distribution tells a story:

- **High "very disappointed," low "not disappointed":** strong PMF in a segment; scale it
- **Low "very disappointed," high "not disappointed":** no PMF anywhere; do not add features; find the job
- **Moderate "very disappointed," high "somewhat disappointed":** emerging PMF; convert "somewhat" by studying what "very" has that they don't
- **Clustered "very disappointed" in one user type:** PMF exists in a niche; narrow the product to that niche before expanding

The number alone is insufficient. You need to cross-reference the "very disappointed" answers with user attributes — what type of user are they? What use case? What company size? That cross-reference tells you not just whether you have PMF but *where* you have it.

---

## Find Your Bright Spots

### The Counterintuitive Move

Most product teams look at low-satisfaction users and ask: "What can we build to win them over?" This is the wrong move. A user who answered "not disappointed" is telling you they don't have the job your product was designed to do, or they have it but your product doesn't do it well enough to matter. Adding features for them produces a bloated product that serves no one particularly well.

Vohra's insight: **ignore "not disappointed" users entirely during the PMF phase.** Do not try to convert them. Do not build for them. Do not read their feedback as directionally meaningful.

Instead: **study "very disappointed" users obsessively.**

### What to Look for in the "Very Disappointed" Cohort

Aggregate their answers to the follow-up questions. Look for:

- **Clustering by use case or context:** are they all power users? All in a specific industry? All doing the same specific task? This is your core use case.
- **Common language:** what words do they use to describe the benefit? If 60% of "very disappointed" users use the word "fast," speed is a core product value — not an engineering concern.
- **What they love vs what they want:** the "primary benefit" answer is what they love; the "how to improve" answer is what they want more of. Both are directional. The love is the core. The want is the roadmap.
- **Who they think the ideal user is:** their answer to "what type of person benefits most" is often the clearest positioning statement you'll ever receive. Users in this cohort who can articulate who the product is for are describing themselves in the third person.

### The Segment Pivot

If the "very disappointed" cohort is too small to sustain the business at scale, but it's clearly defined, that is not a failure — it is a signal. The options are:

1. **Narrow the product** to serve that cohort better, deepen PMF, then expand
2. **Expand the cohort** by finding more people with the same use case (distribution problem, not product problem)
3. **Re-examine the cohort definition** — are the "very disappointed" users a subset of a larger addressable group you haven't fully reached yet?

The wrong move: broaden the product to serve a larger but less-defined audience in hope that the PMF number improves. It won't. Breadth without depth produces "somewhat disappointed" at scale.

---

## Speed as a Product Value

### The 100ms Constraint

Human perception processes actions as "instantaneous" if they complete within 100 milliseconds. Above 100ms, the lag registers. Above 1000ms, the user becomes conscious of waiting. Above 10,000ms, attention breaks entirely.

Superhuman treats **every user-initiated action completing in under 100ms** as a hard product constraint — not a performance goal, not a nice-to-have, not something to address when there's time. It is a product requirement with the same status as correctness.

This constraint is unusual because performance is typically treated as an engineering quality issue, downstream of feature development. Vohra treats it as a product value upstream of feature development. A slow feature is a broken feature.

### Speed Is Not a Feature — It Is a Feeling

The experience of speed is not linear. A product that responds in 50ms does not feel "twice as fast" as a product that responds in 100ms — it feels qualitatively different. The feeling is not "fast" vs "faster." It is "this works" vs "this works, I think."

Slow software communicates something to the user: their time is not valued. Every lag is a tiny tax. Every spinner is a small insult. Users habituate to these insults and stop noticing them consciously — but they accumulate as a general sense that the product is slightly unpleasant to use.

Fast software communicates the inverse: the product was built by people who understand that your time is finite and your attention is precious.

**The competitive implication:** a competitor who ships the same feature set but faster wins the UX comparison without the user being able to articulate why. "It just feels better" is almost always a speed diagnosis.

### How to Apply the 100ms Constraint

- **Measure first, optimise second:** you cannot know what to optimise without instrumenting the slowest actions first
- **Optimistic UI updates:** write to state immediately; confirm with the server in the background; if the server rejects, roll back with an error — do not wait for the server before updating the UI
- **Perceived vs actual performance:** skeleton screens, instant visual feedback, and pre-fetching do not make the product faster, but they make it feel faster; both matter
- **Never accept "good enough":** a 300ms response that ships is not better than a 90ms response that ships one sprint later; speed is a product quality dimension, not a polish task

### The Asymmetry of Speed Degradation

It takes significantly more work to make a fast product slightly faster than to prevent a fast product from becoming slow. Performance debt compounds faster than feature debt. Every database query added without a performance budget, every unoptimised render, every additional network round-trip is a small withdrawal from the speed account.

Establish performance budgets before shipping features, not after slowness is noticed.

---

## High-Expectation Customer (HXC)

### Julie Supan's Framework

Julie Supan, who led marketing at Dropbox, YouTube, and Airbnb, articulates the HXC framework: **design for the most demanding, most sophisticated user in your target market.**

The high-expectation customer is defined not by demographics but by psychographics:
- They have high standards for the tools they use
- They can immediately tell the difference between something done well and something done adequately
- They refuse to tolerate experiences that waste their time or treat them as average
- They have strong opinions about what a product *should* do, formed by experience with the best tools in adjacent categories
- When they find something that meets their standards, they become vocal advocates

The HXC is not the power user. A power user uses every feature. The HXC uses features they consider well-made and abandons features they find poorly designed. They are a quality filter, not a usage maximiser.

### Why Designing for the HXC Works

If your product satisfies the highest-expectation user in the category, it will satisfy every user with lower expectations. The inverse is not true: a product designed for the median user will fail to satisfy the HXC, and the HXC's judgement — expressed through advocacy or vocal criticism — has disproportionate market influence.

The HXC is also the most valuable early adopter. They have:
- The vocabulary to describe what they love and why (your marketing brief)
- The network reach to spread word-of-mouth among similar high-expectation users
- The standards to notice and report genuinely important product failures

A product built for the HXC self-selects for the best kind of growth: earned advocacy from demanding users who chose you despite having high alternatives.

### What the HXC Is Not

- **Not the enterprise buyer:** the buyer who approves the budget is often not the user with the highest expectations; design for the user, not the approver
- **Not the most technically sophisticated user:** sophistication is not the same as high expectations; an HXC can be non-technical but refuse to tolerate bad UI
- **Not the loudest user:** vocal users on Twitter or in support tickets are not always high-expectation; they may be low-expectation users frustrated by a gap, not high-expectation users whose standards weren't met
- **Not a demographic:** age, role, company size don't define the HXC; standards and taste do

---

## Selective Scarcity and Positioning

### Turning Away Wrong-Fit Users

Vohra ran Superhuman with a waitlist and a mandatory onboarding interview during the PMF phase. Every new user was screened. Users who didn't fit the core use case (power email users who processed high-volume, high-stakes correspondence daily) were not admitted.

This is counterintuitive from a growth lens but precise from a PMF lens: **admitting wrong-fit users dilutes the "very disappointed" signal and pulls the product toward mediocrity.** Every feature requested by a wrong-fit user is a feature that moves the product away from the core.

The waitlist also creates legitimate scarcity: users who wait feel they earned access. Users who earned access are more likely to engage seriously, form habits, and become advocates.

### Premium Pricing as a Quality Filter

Charging a premium price selects for users who value the product at the price point. Users who choose a premium product over a cheaper alternative have already answered one survey question: they believe the product is worth more than the alternatives.

Premium pricing also funds the product quality that justifies the premium. A race to the bottom on price forces cost-cutting on the product quality dimensions — support, polish, performance — that high-expectation customers care most about.

**The positioning implication:** never compete on price. Price competition is a race to the bottom where no one builds a great product because no one can afford to. Compete on meaning: "this product is for people who take X seriously." People who take X seriously will pay more for a product that takes X seriously.

### "For People Who Take X Seriously"

The strongest positioning statements define not what the product does but who it is for and what it says about them. Superhuman's implicit positioning: "for people who take email seriously enough to pay $30/month and invest in learning keyboard shortcuts." That positioning filters for exactly the HXC cohort.

Every onboarding step, every premium feature, every pricing decision should reinforce this. The product is not for everyone. It is for the right people.

---

## Common Failure Modes

- **Using NPS instead of the Sean Ellis question:** NPS measures sentiment; the Ellis question measures dependency; only dependency predicts business survival
- **Averaging the survey results:** a 38% "very disappointed" score is not "close to PMF" if it's spread evenly across five different use cases; drill into who the 38% are before drawing conclusions
- **Building for "not disappointed" users:** they don't have the job; more features won't change that; you will bloat the product and dilute the core
- **Treating speed as polish:** moving performance work to a later sprint after features ship; speed debt compounds and the cost of reclaiming it grows non-linearly
- **Designing for the median:** the median user's tolerance for mediocrity will cap your product quality; design for the HXC and the median is automatically served
- **Confusing early adoption with PMF:** enthusiastic early adopters in a startup's network are not representative of the market; measure the Ellis question before concluding you have PMF
- **Waitlist theater:** using a waitlist as a marketing tactic rather than a quality gate; only effective if you actually screen users and reject wrong-fit ones

---

## Applied to DojoFlow

### Applying the 40% Rule to White Crane

The White Crane pilot is a single-school deployment — too small for a statistically meaningful survey. But the framework still applies:

**Survey to run after 6–8 weeks of real use:**
> "How would you feel if you could no longer use DojoFlow?"

Run it with Grandmaster and Master Nicholls separately. Their use cases differ:
- Grandmaster: strategic oversight, big-picture student retention
- Master Nicholls: day-to-day instruction, attendance, individual student progress

If either answers "not disappointed," that is a product signal, not a relationship signal. Follow up: "What would you use instead?" and "What do you wish DojoFlow did that it doesn't do now?"

The goal at this stage is not 40% — the goal is understanding which specific capability makes them "very disappointed" to lose. That capability is the core. Everything else is secondary.

### Who DojoFlow's HXC Is

The HXC for DojoFlow is **not** the average dojo owner running a 20-student hobby school. The HXC is:

> **The growth-minded owner of a 50–200 student school who has outgrown Kicksite or the spreadsheet, cares about student outcomes as much as revenue, and refuses to tolerate software that treats their school like a generic gym.**

This person:
- Has already decided that running a school seriously requires serious tools
- Is frustrated that existing software is built for billing-first, students-second
- Will immediately notice whether the product was built by people who understand martial arts pedagogy or by people who copy fitness-studio SaaS
- Has strong opinions about what "professional" looks like for a dojo
- Will advocate loudly if the product meets their standards — and criticise loudly if it doesn't

**Design implication:** every DojoFlow feature should pass this test — "would the owner of a serious, growth-oriented school think this was built for them, or for a generic gym manager?" The language should feel like it was written by someone who knows what a Dan promotion means. The UX should feel like it was designed by someone who understands the sensei's relationship with their students is not a transaction.

This is distinct from Grandmaster specifically. Grandmaster is a pilot user with enormous domain credibility. The HXC as a market segment is the owner who has graduated beyond spreadsheets and the cheapest SaaS option, and is ready for something built for them.

### Speed Implications

**Kiosk check-in:** the kiosk is used in the 60 seconds before a class starts, with 20 students queueing. Every interaction must complete in under 100ms (local state), with server confirmation in the background. A spinner between name search and the check-in confirmation screen is a product failure in this context. Students will walk past it.

The current kiosk does optimistic UI updates — this is correct. The risk is database write latency being perceived through edge cases (duplicate check-in state, enrollment-required state). These states must resolve in under 100ms of appearance, not under 100ms from button press.

**Suggested Sends queue:** the approval action — the sensei tapping "send" on a drafted follow-up message — must feel instantaneous. If the sensei is doing this on a phone between classes, a 3-second wait for Postmark confirmation will make the feature feel unreliable. The right architecture: update the queue state immediately (mark as sent), fire the Edge Function async, surface any delivery error separately. Never make the sensei wait for the email server.

**Magic Text drafting:** the draft request makes a call to the Claude API. Current latency will be perceptible. This is acceptable once (loading state is expected for AI generation), but the result must appear complete — not streamed character by character in a way that looks unpolished. If streaming is used, it should look intentional and fast, not choppy.

### Positioning: Progression vs Price

**Wrong positioning (competing on price):**
> "Affordable martial arts software that replaces your spreadsheet."

This attracts price-sensitive users who will churn to the next cheaper option and whose feedback will pull the product toward commodity features.

**Right positioning (competing on meaning):**
> "For instructors who take student progression seriously."

This attracts the HXC: the owner who has already decided that their students' outcomes are worth investing in. These users will pay more, stay longer, and advocate more loudly.

The implicit claim in "for instructors who take student progression seriously" is that DojoFlow is the platform that takes it as seriously as they do. Every product decision should make that claim true:
- Contact completeness warnings: "we know that an unreachable student is a student you can't help"
- Magic Text: "we know your message to a drifting student needs to sound like you, not a CRM blast"
- Kiosk: "we know check-in happens in 60 chaotic seconds before class, not in a quiet office"
- Suggested Sends: "we know you'll forget to follow up when you're focused on the mat"

None of these features are generic gym-management features. All of them are features a sensei who takes student progression seriously immediately understands and wants. That specificity is the brand.
