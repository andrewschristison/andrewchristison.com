# Tiny Habits

## Core Idea

BJ Fogg's *Tiny Habits* is built on a single behavioral insight that runs counter to most product and self-improvement thinking: **motivation is an unreliable foundation for behavior change**. Willpower fluctuates. Enthusiasm fades. Designing for the motivated user guarantees that your product works when people are already inclined to act and fails when they need it most — on bad days, tired days, distracted days.

The alternative Fogg proposes is the **Fogg Behavior Model**: B = MAP. Behavior happens when Motivation, Ability, and Prompt converge at the same moment. If a desired behavior is not occurring, one of the three elements is missing or misaligned. This is a diagnostic framework as much as a design framework. When a feature isn't being used, the question is not "how do we motivate users more?" It is "which of the three is failing, and what is the minimum intervention to restore convergence?"

The Tiny Habits method follows directly: take any behavior you want to install, make it as small as possible (small enough to do on your worst day), anchor it to an existing behavior that already reliably happens, and celebrate immediately after. The celebration is not optional — it is the mechanism by which the brain encodes the habit. Emotion creates habit, not repetition.

For DojoFlow, this framework has two applications. The first is designing the product's workflows so that the behaviors you want instructors and students to perform are tiny, prompted, and immediately satisfying. The second is understanding the habits your product is trying to install in users' lives — and auditing whether the current design actually supports that installation.

---

## The Fogg Behavior Model: B = MAP

### Motivation

Motivation is the desire or willingness to perform a behavior at a given moment. Fogg models it on a dimension from negative (avoiding, resisting) to positive (wanting, eager). Critically, motivation fluctuates constantly — it is context-dependent, mood-dependent, and time-of-day dependent. A person's motivation to review their student absence queue is higher on Monday morning than on Friday afternoon after teaching three classes.

The design error that follows from misunderstanding motivation is building features that only work when motivation is high. A four-step approval flow for a Suggested Send is manageable when an instructor has energy and focus. It is abandoned when they are depleted. The way to make a feature robust across motivational states is not to optimize for the high-motivation version — it is to reduce ability requirements so that the low-motivation version still works.

Fogg's counter-intuitive prescription: **do not try to increase motivation**. Motivational campaigns, reminder streaks, and guilt-inducing notifications all attempt to push users up the motivation axis. They work occasionally and backfire frequently. The more reliable lever is always ability — make the behavior easier, not the person more motivated.

### Ability

Ability is the capacity to perform a behavior at the moment it is prompted. Fogg breaks ability into six components, which he calls the **ability chain**: time (does the person have enough time?), money (can they afford it?), physical effort (is the behavior physically feasible?), mental effort (how much cognitive load is required?), social deviance (does performing the behavior require going against social norms?), and non-routine (does the behavior require departing from the existing flow of the day?).

The weakest link in the ability chain is what determines whether the behavior happens. A behavior that requires very little time, no money, no physical effort, but high mental effort will fail on the mental effort dimension. Identifying the weakest link for each DojoFlow workflow determines where design effort produces the greatest return.

For most instructor-facing features in DojoFlow, the binding constraints are **mental effort** and **non-routine**. Instructors are not short on time in the aggregate, but they are cognitively loaded during and immediately after class. Any feature that requires holding information in mind, comparing options, or departing from their natural post-class routine will fail more often than it succeeds.

### Prompt

The prompt is the signal that initiates the behavior. Without a prompt, behavior does not happen — even when motivation and ability are both present. Fogg identifies three types:

**External prompts** are cues from the environment: a notification, a banner, a badge count, an email, a physical object in view. They are the most common type used in product design and the most fragile. External prompts require the product to interrupt the user's attention, which is expensive (it costs the user attention), annoying at high frequency, and easily ignored through habituation.

**Internal prompts** are emotional or physiological states that cue behavior: the feeling of anxiety that makes an instructor think "I should check if anyone is drifting," the feeling of accomplishment after marking attendance that makes them think "I should send that follow-up." Internal prompts cannot be directly engineered, but they can be cultivated by successfully completing the loop repeatedly until the association forms. The goal of any habit-forming product is to eventually have external prompts replaced by internal ones.

**Action prompts** — which Fogg calls the anchor in the Tiny Habits method — are the most powerful type. An action prompt is triggered by completing an existing behavior: *after I do X, I do Y*. Action prompts do not require the product to interrupt the user, do not require the user to feel a particular emotion, and do not habituate because the anchor behavior itself is not going anywhere. Designing features as action prompts — things that happen after a reliable existing behavior — is the highest-leverage prompt design available.

---

## The Tiny Habits Method

The recipe: **After I [ANCHOR HABIT], I will [TINY BEHAVIOR]. Then I will celebrate.**

The anchor must be an existing behavior that already reliably occurs in the user's life. The tiny behavior must be small enough to execute even on the worst day — if the smallest version is not achievable on a bad day, it is not yet tiny enough. The celebration must happen immediately and feel genuine — a smile, a sense of satisfaction, a small acknowledgment. The brain does not distinguish between sources of positive emotion; what matters is that the emotion occurs immediately after the behavior, wiring the association.

Fogg's insight about the celebration is the most frequently misunderstood part of the method. Designers focus on the anchor and the tiny behavior and treat celebration as a soft recommendation. But without genuine positive emotion at the moment of completion, the habit does not wire. The celebration is the mechanism, not the optional encouragement.

For software products, the celebration is the design of the completion moment. A green flash. A satisfying sound. A count incrementing. A success state that lingers just long enough to register. These are not decorative — they are the neurological substrate of habit formation.

---

## The Motivation Wave

Motivation is not stable — it moves in waves. It peaks at the moment of inspiration: when a student earns their belt, when an instructor attends a seminar and feels re-energized, when a parent sees their child achieve something they didn't think possible. Motivation then decays rapidly and returns to baseline. This decay is not a character flaw; it is how human motivation biology works.

The practical implication is **design for the peak**. The moment of highest motivation is the moment when behavior change is easiest to install. A student who has just been promoted to a new belt will, at that exact moment, be more willing to commit to the next level, sign up for extra classes, or recruit a friend than they will be at any point in the following weeks. That is the moment to extend the hook, ask for the commitment, or send the next-level invitation — not two weeks later when motivation has returned to baseline.

For instructors, the motivation wave matters for onboarding and habit installation. The first week with DojoFlow is the peak. The instructor is energized, curious, and willing to explore. Every key habit the product wants to install — checking the Suggested Sends queue, reviewing attendance after class, sending the first Magic Text message — should be prompted in that first week, when motivation is high enough to overcome the non-routine barrier. Once the habits are wired, they persist even as motivation returns to baseline.

---

## Ability Audit

For every DojoFlow feature, the ability chain provides a structured diagnostic. Run it before building and again before shipping:

**Time:** How many seconds does this take at the moment it is typically performed? If the answer is "it depends on how much the user wants to engage," the feature has not been designed for a specific moment. Time requirements must be evaluated against the time available in the specific context — kiosk check-in happens while other students are arriving; it must complete in under 5 seconds. Suggested Send approval happens between classes; it should be completable in under 30 seconds per message.

**Mental effort:** How many decisions does the user make? How much information do they need to hold in working memory? Does the feature require reading, comparing, or calculating? Every decision adds to the mental effort cost. The target for any habit-critical feature is one decision or zero.

**Non-routine:** Does performing the behavior require departing from what the user naturally does at this moment? Features that fit into existing workflows succeed; features that require users to remember to visit a separate screen fail. The Suggested Sends queue must be encountered naturally in the instructor's flow — not require a deliberate navigation to a sub-section.

**Physical effort:** For the kiosk specifically, the physical action required of young students determines success. Large tap targets, visual recognition over typing, proximity of the kiosk to the natural path into the dojo — these are ability factors that make or break the check-in behavior for the youngest users.

---

## Applied to DojoFlow

**Kiosk check-in as Tiny Habit anchor:**
The check-in loop is already structured as a Tiny Habit. Anchor: arriving at class (existing, reliable). Tiny behavior: tap your tile or type your name (seconds, zero decisions). Celebration: green flash with name (immediate, designed). The kiosk's stripe progress display — "X classes toward your next stripe" — extends the celebration into motivation by making the investment visible. Every element of the kiosk design should be evaluated against the Tiny Habits recipe: is the anchor clear? Is the behavior tiny enough for a six-year-old who just ran in from the car? Is the celebration genuine?

**Suggested Sends as action prompt, not external trigger:**
The current design of Suggested Sends as a queue the instructor navigates to is an external prompt — it depends on the instructor being motivated enough to remember the queue exists and navigate to it. The more powerful design is to make it an action prompt: after the instructor opens DojoFlow (existing, reliable daily habit), the Suggested Sends queue is the first visible element, requiring zero navigation. The anchor is app open; the tiny behavior is reviewing one message. The celebration is the queue count decreasing. This reframing dramatically reduces the non-routine and mental effort barriers.

**Belt promotion as motivation wave moment:**
The moment a belt promotion is recorded in DojoFlow is the peak of the student's motivation wave. The system should respond to that moment by queuing a congratulations message for instructor approval (tiny behavior anchored to the promotion action) and — when the communication infrastructure is live — automatically surfacing what the student needs to know about the next level. Not a week later. At the moment. The motivation wave is real and brief; the product must be ready to act when it peaks.

**Instructor onboarding and habit installation:**
The first week is the only time motivation is reliably high enough to overcome the non-routine barrier for all DojoFlow workflows. Onboarding should be designed to install the three critical habits before motivation decays: (1) check Suggested Sends queue when opening the app, (2) mark attendance during or after each class, (3) send at least one Magic Text message before the first week ends. Each of these should be prompted as a Tiny Habit recipe during onboarding — not a feature tour, but an anchor-behavior-celebration sequence. The goal is that by day 8, all three behaviors are wired to anchors that pre-exist DojoFlow, so they continue running at baseline motivation.

**Designing for the depleted instructor:**
Every instructor-facing workflow should be imagined at the moment of lowest motivation and highest depletion: end of a Friday class, running late, students still in the room asking questions. If the feature requires more than one decision and thirty seconds, it will not be used in that moment. If it is not used in that moment, it may never become a habit — because the high-motivation moments are few and the depleted moments are many. The kiosk passes this test because the students run it themselves. The Suggested Sends queue passes this test if it surfaces automatically and requires only one tap per message. Any feature that requires the instructor to navigate, remember, or decide in a depleted state will become a dead feature.
