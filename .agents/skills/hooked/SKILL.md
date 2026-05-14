# Hooked

## Core Idea

Nir Eyal's *Hooked* argues that the most valuable consumer products are not used because of advertising or persuasion — they are used out of habit. Habits form when a product gets woven into the routine triggers of a user's emotional life: a moment of boredom, a spike of anxiety, a flicker of loneliness. The product becomes the reflex response to that internal state.

The mechanism is the **Hook Model**: a four-phase loop that, repeated enough times, moves the user from conscious choice to automatic behavior. Products that successfully hook users don't need to push people to return — the users push themselves.

Understanding the Hook Model is equally useful for building products that form good habits and for recognizing when a product has crossed from habit-forming into manipulative. The ethics matter as much as the mechanics.

---

## The Hook Model

The four phases run in sequence. Each pass through the loop strengthens the association between the internal trigger and the product.

### Phase 1 — Trigger

The initiating event. There are two types:

**External triggers** are sensory cues from the environment: a notification, a badge count, an email subject line, a kiosk screen lighting up. They tell the user what to do next explicitly. External triggers are necessary to acquire users, but insufficient to retain them. They depend on the product interrupting the user's attention — which is expensive and fragile.

**Internal triggers** are emotional states that become associated with the product through repeated use. Boredom → open Instagram. Uncertainty → Google something. Anxiety about a student drifting → open DojoFlow. Internal triggers are powerful because they are free, always present, and the product does not need to do anything to fire them.

The goal of the Hook Model is to move users from external to internal triggers as quickly as possible. Every time an external trigger fires and the user completes the loop, the internal trigger grows stronger.

### Phase 2 — Action

The simplest behavior performed in anticipation of a reward. Eyal uses BJ Fogg's model: **Motivation + Ability + Trigger** must all be present for an action to occur.

The design implication is to **reduce friction relentlessly**. Motivation is volatile; ability is something the product controls. Every extra tap, every loading spinner, every required field that can be optional is a place where motivation runs out before the action completes. The simplest possible action that still delivers the reward is the right action.

Action examples by effort level: viewing a notification (near-zero effort), opening an app (low), tapping a button (low), filling a form (medium), writing a message (high). High-effort actions require high motivation. Design for low effort; reserve high-effort actions for high-stakes moments.

### Phase 3 — Variable Reward

The reason the loop doesn't get boring. Fixed rewards (the same outcome every time) produce habituation — the brain stops caring. **Variable rewards** maintain engagement because the brain's dopamine response is stronger when the outcome is uncertain.

Eyal identifies three reward types:

**Rewards of the Tribe** — social validation, belonging, recognition from others. Likes, comments, leaderboards. For DojoFlow: an instructor seeing that their message to a drifting student got a reply. The outcome (did they respond?) is uncertain — which is what makes the action (send the message) feel worth doing.

**Rewards of the Hunt** — acquiring resources, information, or status through effort. Scrolling for interesting content, searching for a deal, finding the perfect candidate in a list. For DojoFlow: an instructor scanning the at-risk dashboard for the student most urgently needing a call. The hunt itself is the reward — the moment of recognition when a name stands out.

**Rewards of the Self** — intrinsic satisfaction, mastery, completion. Closing all the tasks in an inbox, finishing a level, reaching a milestone. For DojoFlow: a student earning their first stripe. The instructor checking off the last student for belt testing. Completion as identity.

Effective products combine at least two reward types. The most habit-forming products hit all three.

### Phase 4 — Investment

An action the user takes that loads the next trigger and increases the product's value over time. Investments are usually effort, data, reputation, or skill — things the user puts *into* the product.

Investments make switching costly. The more a user has invested, the more they lose by leaving. A student's attendance history, a school's entire roster and belt records, an instructor's library of Magic Text message history — all of these are investments that increase the cost of switching to a competitor.

Crucially, investments load the **next trigger**. A student's attendance record feeds their stripe count — which creates a new milestone (internal trigger: "I'm close to my second stripe"). An instructor approving a Suggested Send creates a communications log entry — which they will check next time they open the app (internal trigger: "did anything change?").

---

## External vs Internal Triggers: The Transition

The explicit goal in product design is to make internal triggers replace external ones. The path:

1. External trigger (notification, banner, direct message) gets user into the app
2. User completes the loop and gets a variable reward
3. The emotional state that preceded the loop gets associated with the product
4. Next time that emotional state arises, the user reaches for the product before any external trigger fires

For DojoFlow, the target internal trigger for instructors is the low-level anxiety of **"I wonder if anyone is slipping away."** Once that anxiety reliably resolves by opening DojoFlow (and finding actionable information), the habit is formed. The external trigger (email digest, dashboard notification) is the scaffolding — the internal trigger is the destination.

---

## The Manipulation Matrix

Eyal's ethical framework for habit-forming products. Two questions:

1. **Does this product materially improve the user's life?**
2. **Would I use this product myself?**

This produces four quadrants:

| | Would use it myself | Wouldn't use it myself |
|---|---|---|
| **Improves users' lives** | Facilitator — build with confidence | Peddler — misalignment between maker and user |
| **Does not improve users' lives** | Entertainer — defensible if honest | Manipulator — do not build |

**Facilitators** have the highest ethical standing and the most durable businesses. The product serves the user's genuine long-term interest, and the maker believes in it enough to use it themselves. This is where DojoFlow must operate.

**Manipulators** exploit the Hook Model to create engagement that does not serve the user. Slot machine mechanics, infinite scroll designed to prevent stopping, social validation systems designed to create anxiety rather than relieve it. These produce short-term engagement and long-term harm to users and brand.

**The specific concern for school management tools:** The students being tracked are often minors. The habit-forming mechanics (attendance streaks, belt progression visuals, milestone notifications) operate on children's psychology. The ethical question is not just "does this help the instructor?" but "does this serve the student's genuine long-term development?" Designing streak mechanics that pressure attendance for its own sake — rather than genuine engagement with learning — crosses into manipulation.

The test: if a student's parent could see every design decision in the product, would they approve?

---

## Common Failure Modes

- **Substituting external triggers for internal ones indefinitely** — sending more notifications when engagement drops, rather than asking why the product failed to form an internal trigger
- **Variable reward without genuine value** — randomness for its own sake (gamification that adds points but no meaning); the brain habituates quickly when the reward has no intrinsic worth
- **Investment that locks in the wrong users** — making it painful to leave for users who are not well-served; this creates resentment, not loyalty
- **Skipping the action phase** — designing a complex action and hoping motivation carries users through; motivation is volatile; reduce friction instead
- **Designing for engagement rather than outcomes** — maximizing time-in-product when the user's actual goal is to accomplish something and leave; this is manipulation, not habit formation
- **Ignoring the ethics layer** — treating the Manipulation Matrix as optional; habit-forming design without ethical constraint produces products that are harmful and, eventually, legislated against

---

## Applied to DojoFlow

**Kiosk check-in as a micro-hook:**
The check-in loop is: External trigger (kiosk screen, class starting) → Action (student taps their name tile or types their name) → Variable reward (green flash + name + time: identity confirmation — "I'm here, I'm a martial artist, I showed up") → Investment (attendance record created, which increments the class count toward the next belt stripe — loading the next internal trigger: "I'm getting closer").

The variable component: the student doesn't know exactly when the next stripe milestone hits. That uncertainty is the reward driver. The kiosk's job is to make the action as frictionless as possible (tiles for kids who can't type, large targets) so that motivation never needs to be high.

**Belt stripe system as variable reward:**
Color belt students accumulate classes toward stripe milestones at 12 and 24 classes since last promotion. The reward (stripe awarded) is visible, social (instructor awards it in class), and variably timed (the student knows the threshold but not always exactly where they are). This combines Rewards of the Hunt (tracking progress) with Rewards of the Tribe (public recognition from instructor) and Rewards of the Self (milestone completion).

Design implication: the student-facing progress view (when built) should show progress toward the next stripe but not make it trivially gameable. The goal is genuine attendance driven by investment in the art, not attendance-for-points that evaporates when novelty fades.

**Suggested Sends as external trigger mechanism:**
The Suggested Sends queue is an external trigger directed at the instructor. The trigger: a badge count or dashboard tile showing pending messages. The action: review and approve. The variable reward: uncertainty about whether the student will respond (Reward of the Tribe). The investment: the communications log entry, which the instructor will check next session.

The habit being formed: the instructor develops a routine of checking their queue and acting on it, which gradually becomes an internal trigger ("I should check if anyone needs a follow-up today") rather than waiting for a notification.

**Designing habit-forming instructor workflows:**
The target internal trigger for instructors is low-level concern: "Is everyone okay? Is anyone slipping?" DojoFlow should reliably resolve that concern when opened. This means the Dashboard must surface actionable information immediately — not after navigation, not after loading, not buried in a tab. If opening DojoFlow reliably answers "who needs attention today," the habit forms.

The investment phase for instructors is the accumulation of student context: attendance patterns, message history, belt progress. Every interaction adds to this context, making DojoFlow more useful the longer it's used — and more costly to abandon.
