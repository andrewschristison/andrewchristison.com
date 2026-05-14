# Nudge

## Core Idea

Richard Thaler and Cass Sunstein's *Nudge* begins from the observation that humans are not the rational actors that classical economics assumes. People do not evaluate options carefully and choose what maximises their long-term welfare. They use heuristics, defer to defaults, follow social norms, avoid effort, and respond to context in predictable and exploitable ways. This is not a flaw to be corrected through better education — it is the stable operating condition of human cognition.

The concept they introduce is **choice architecture**: the way in which choices are presented inevitably influences which choice is made. There is no neutral presentation. The order of options on a form, the default selection on a toggle, the label on a button, the visual weight given to one outcome over another — all of these alter behavior, whether or not the designer intended them to. The question is not whether you are a choice architect. You already are one. The question is whether your architecture was designed or accidental.

The ethical stance Thaler and Sunstein propose for wielding this power responsibly is **libertarian paternalism**: design the default path to lead toward outcomes that serve the user's genuine long-term interests, while always preserving the freedom to deviate. No one is forced. No options are hidden. But the friction, sequencing, and defaults are arranged so that the path of least resistance is also the path of greatest benefit. This is the only ethical foundation for nudge design in a product used with families and children.

The UK Behavioural Insights Team's **EAST framework** — Make it Easy, Attractive, Social, Timely — extends Nudge from a philosophical framework into an operational design checklist. Thaler's later concept of **sludge** — friction that prevents good decisions — completes the toolkit by naming what to remove as well as what to add.

---

## Choice Architecture

There is no neutral interface. Every screen is a set of architectural decisions that shape what the user notices, what feels natural, what requires effort, and what gets skipped. The designer who does not think about choice architecture does not thereby avoid making choices — they simply make them unconsciously, which means they are made by convention, inertia, or accident rather than by intention.

### Defaults

A default is what happens when the user does nothing. It is the most powerful lever in the choice architect's toolkit, for a simple reason: most people, most of the time, accept defaults. They do so through a combination of inertia (changing requires action), trust (if this is the default, someone must have thought about it), and cognitive load avoidance (evaluating every option is work, and the default removes that work). This is not laziness — it is rational resource management. The brain conserves effort by accepting pre-made decisions when the stakes feel manageable.

Setting a default is therefore an act of power. It determines the outcome for every user who does not actively deviate, which in most cases is the majority. The designer who sets a self-serving default — one that benefits the product at the expense of the user — is exploiting this power. The designer who sets a default that reflects genuine analysis of what outcome serves the user's long-term interest is practising libertarian paternalism.

### Sequencing

The order in which information is presented shapes how it is processed. The first item in a list receives more attention than subsequent items. The first number encountered anchors all subsequent numerical judgments. A decision presented before an emotionally engaging context is processed more carefully than one presented after it. Sequencing is choice architecture even when no defaults are involved.

For multi-step forms and workflows, sequencing determines cognitive load: presenting the most effortful decision last (when the user is already committed and has already invested effort) reduces abandonment. Presenting a decision before the user has enough context to evaluate it produces poor choices and second-guessing.

### Framing

The same information presented differently produces different decisions. Losses are weighted more heavily than gains. Percentages and absolute numbers convey the same mathematical fact but feel different. "92% fat-free" and "8% fat" are identical, but one sells more yoghurt. Framing is not deception — it is an acknowledgment that the emotional valence of information is real and affects decision quality. The choice architect's obligation is to frame in ways that help the user make better decisions, not to exploit framing to serve the product's interests at the user's expense.

---

## Default Effects

### Why Defaults Are Chosen

The empirical evidence for default power is overwhelming. Organ donation rates vary from below 15% to above 90% across countries with nearly identical populations — the difference is entirely explained by whether the default is opt-in or opt-out. Retirement savings rates double when employees are automatically enrolled rather than required to opt in. The behavior being requested is identical; the default determines the outcome.

For software products, the equivalent evidence is in form completion rates, feature adoption, and workflow compliance. Features with sensible defaults get used; features that require configuration before they work don't. Workflows whose default path is the correct path complete at higher rates than those requiring deviation to reach the right outcome.

### Setting Defaults That Serve Users

The test for any default is: if the user accepts this without thinking, are they better off or worse off than if they had evaluated every option carefully? A good default is one that a thoughtful, well-informed user who understood their own long-term interests would choose in most cases. A manipulative default is one that benefits the product at the expense of the user's genuine interests.

For DojoFlow, the student form defaulting to "Trial" status rather than "Active" is a good default — it reflects the correct workflow for a new student and prevents an administrative error that is much harder to correct than to prevent. The billing form auto-populating a family rate from sibling count removes a calculation that families would have to perform anyway and nudges toward standard pricing, reducing negotiation friction for the instructor and pricing confusion for the family. These defaults serve the user's genuine interests, not the product's convenience.

### The Ethics of Default-Setting

In a product used with families and children, default ethics require a higher bar than consumer software. An instructor who accepts a default that incorrectly classifies a student's status, billing rate, or communication preference creates downstream harm for a family. This means defaults must be conservative where errors are costly, and defaults must be clearly visible — not hidden in fine print or revealed only on submission.

Defaults should also be explained where they are non-obvious. "Defaulting to Trial status — change if this student is enrolling directly" is more ethical than a silent default that the instructor does not notice. Transparency about defaults is part of the libertarian paternalist compact: we have chosen this default because we believe it is right for most cases; you are free to change it; here is why we chose it.

---

## The EAST Framework

The UK Behavioural Insights Team distilled the behavioral economics literature into four properties of behaviors that reliably get performed versus abandoned. A desired behavior is more likely to occur when it is Easy, Attractive, Social, and Timely. Each dimension is independently actionable and can be evaluated for any feature.

### Easy

Reduce friction to near zero for behaviors you want to occur. Add friction deliberately for behaviors you want to slow down. The ease of a behavior is not fixed by the behavior itself — it is a product of how the interface presents and supports it.

The kiosk tile grid is the clearest Easy example in DojoFlow. Typing a name is harder than recognising and tapping a tile. For young children, typing a full name under social pressure — other students arriving, class starting — fails the Easy test. The tile grid removes the typing requirement entirely for enrolled students; the search bar remains for assistant instructors and open-enrollment arrivals who cannot be pre-populated. The design choice was not about aesthetics — it was about reducing the ability requirement to the minimum necessary for the target user population.

The Mark All cascade in attendance marking is the same principle applied to the instructor's workflow. Tapping each student individually to mark a full class present is friction that accumulates. A single "Mark All" tap that cascades across the roster in 20ms intervals is the same outcome with a fraction of the effort. Removing that friction removes the temptation to defer attendance marking until after class, which removes the risk that it doesn't happen at all.

The "Teaching today?" prompt on the kiosk success screen is Easy because it appears at the right moment without requiring any navigation. The instructor does not need to open a student profile, find an attendance record, and set a flag. The prompt is there; it requires one tap. If it required any more than that, the teaching credit system would not be used consistently.

### Attractive

A behavior that feels rewarding to perform is more likely to be repeated. Attractiveness is not superficial — it is the mechanism by which positive emotion encodes the habit. The visual and interactive design of a completion moment determines whether the brain tags that behavior as worth repeating.

The green success flash on the kiosk is attractive because it is specific, immediate, and visually distinct from the neutral screen state. It is not a grey notification or a text confirmation — it is a full-screen color change with the student's name. The brain registers it as an event, not an acknowledgment. That distinction matters for habit encoding.

Belt color dots on the student list and profile are attractive because they make status visually distinct without requiring reading. The instructor's eye lands on the belt rank and reads it immediately. Color is pre-attentive — processed before conscious attention — which means it is attractive in the most literal sense: it pulls the eye without effort.

An animated checkmark on message approval, a count decrementing in the Suggested Sends queue, a stripe increment on the check-in success screen — these are all attractive completion signals. They are not decoration. They are the reward side of the habit loop, and they must be designed with the same intention as the functional logic.

### Social

Behavior is shaped by social norms — what others are doing, what is expected, what is visible to others. People are more likely to perform a behavior when they believe it is what most people in their situation do, when their own behavior is visible to people they care about, and when they feel part of a group whose identity the behavior expresses.

For the kiosk, showing "18 classes toward your next stripe" on the check-in success screen is a social signal — it makes the student's progress feel like a position within a larger community of people on the same journey. The stripe system itself is social: stripes are awarded by the instructor in front of the class, which makes every achievement a public event. DojoFlow's role is to surface the data that makes those social moments possible and to frame individual progress in the context of the community.

Attendance counts visible to the student at check-in serve a similar function. Knowing your own class count is informational. Knowing your class count in a context where peers are checking in around you is social — it makes the accumulation feel like participation, not just record-keeping.

The Social dimension also applies to instructors. Suggested Sends norms an instructor behavior: following up with at-risk students. Once the queue is a standard part of the instructor's workflow, "I reviewed my queue this week" becomes the expected behavior — and not reviewing it becomes a deviation from the norm. The system creates its own social expectation.

### Timely

Interventions are most effective when they occur at the moment when the person is most receptive and when the decision is most relevant. The same nudge applied at the wrong moment is ignored or resented; applied at the right moment, it is welcomed and acted on.

Suggested Sends fires when absence crosses 14 days — not at the end of the month, not daily as a reminder, but at the specific threshold where the data suggests re-engagement is both urgent and still plausible. The timing is calibrated to the behavior being nudged: 14 days absent is the point where a student is at risk but not yet lost. Two weeks later, the follow-up is a win-back attempt with much lower odds.

The "Teaching today?" prompt appears during the 3-second check-in success window. This is the correct moment — the assistant instructor is physically present, the check-in just occurred, the attendance record is being written. Prompting teaching credit at any other moment (in a student profile, in an admin settings panel) would be too removed from the event it documents. The timing makes the prompt feel natural rather than intrusive.

The motivation wave — Fogg's observation that motivation is highest at the moment of inspiration and decays rapidly — is a timing insight. Belt promotion is the peak of the student's motivation. The congratulations message should queue at the exact moment of promotion, not the next time an instructor thinks to follow up. Timely nudges ride the motivation wave; untimely ones arrive after it has passed.

---

## Libertarian Paternalism

Libertarian paternalism is the ethical doctrine that makes nudge design defensible. The core claim: it is legitimate to design choice architectures that guide people toward outcomes that serve their long-term interests, provided that no options are removed and deviating from the default path remains genuinely easy.

The "libertarian" component is non-negotiable. A nudge that is actually a shove — where deviating from the default is difficult, options are hidden, or the user is not aware that a choice was made on their behalf — is manipulation, not libertarian paternalism. The freedom to choose differently must be real and visible.

The "paternalism" component is also non-negotiable. The designer cannot hide behind user autonomy as a reason to avoid thinking about whether the default path actually serves the user. Claiming "we just present options neutrally" is false — there is no neutral presentation — and it is an abdication of responsibility. The designer chose the defaults, the sequencing, the framing. Owning that responsibility and exercising it in the user's interest is what separates ethical from unethical choice architecture.

For DojoFlow, libertarian paternalism has three primary applications. Suggested Sends nudges instructors toward following up with at-risk students: the message is drafted, the student is surfaced, the action is made easy. But the instructor always reads, always edits, always approves. Nothing sends automatically. The paternalism is in the nudge; the liberty is in the review and the opt-out. The "Teaching today?" prompt nudges toward teaching credit logging, but a single tap dismisses it with no follow-up. The kiosk attendance record is an upsert — idempotent, with no locked state — so any check-in that was made in error can be corrected. The nudges are real; the freedom is real.

The specific concern for a school management tool is that the users being affected include minors. An instructor nudged by a poorly designed default toward sending a message to a family is making a communication choice on behalf of that family. The ethical bar for defaults in communication workflows must therefore be higher than for administrative defaults: a communication default should never result in a message being sent without explicit instructor review, regardless of how convenient automated sending would be.

---

## Sludge

Thaler coined **sludge** as the inverse of nudge: friction, complexity, and burden that prevents people from making good decisions or accessing outcomes they are entitled to. Where nudges smooth the path toward good outcomes, sludge creates barriers that cost users time, effort, and wellbeing without serving any legitimate purpose.

Sludge is everywhere in legacy administrative systems. The physical card stamp system at White Crane is sludge: the Grandmaster must physically locate the card, stamp it, file it, remember where it is, and manually track progress toward the next belt. None of that friction serves the student's development — it is overhead accumulated by the absence of a better system. DojoFlow eliminates this sludge by moving the tracking to the check-in record, making progress visible digitally, and removing the physical maintenance burden entirely.

### Identifying Sludge in Forms

Form sludge takes several recognisable forms. Unnecessary fields — information the form collects but the system does not use — add completion cost with no benefit. Unclear labels — field names that require interpretation or that mean different things to different users — produce errors and re-work. Redundant confirmation steps — "are you sure?" dialogs for non-destructive actions — insult the user's time. Inline validation errors that only appear on submission, after the user has completed the form and moved on mentally, are sludge. Progress indicators that do not indicate actual progress are sludge.

For DojoFlow's student form, the question is: which fields are genuinely required at the moment of student creation, and which can be deferred to a later profile completion step? A walk-in trial student needs a name and a date to be useful to the system. Belt rank, family linkage, billing profile, and contact details are all useful — but requiring all of them before a student can be created is sludge for the walk-in moment. The design should match the required fields to the information that is actually available and necessary in the specific context of entry.

### The Sludge Audit

Before shipping any feature, run a sludge audit: What must the user do to complete this workflow? For every step, ask: does this step produce information the system actually uses? Does this step prevent an error that could not be caught another way? If the answer to both is no, the step is a candidate for removal. Apply this recursively until what remains is the minimum necessary for the workflow to produce a correct output.

The kiosk passes this audit cleanly: the student selects their class, taps their tile or types their name, sees the confirmation. Each step is necessary: class selection routes the record; identification creates it; confirmation provides feedback. There are no confirmation dialogs, no "are you sure?" prompts, no redundant entry steps. The attendance marking mode similarly passes: the instructor opens the mode, taps tiles or uses Mark All, exits. No submission button, no save step, no confirmation dialog — the upsert handles idempotency, eliminating the need for lock states or confirmation.

---

## Feedback Loops

Thaler and Sunstein's work on feedback draws from the observation that people make systematically better decisions when they receive immediate, clear, specific feedback on the outcomes of their choices. The feedback must be immediate (delayed feedback loses the association with the behavior), clear (ambiguous feedback is ignored or misread), and specific (aggregate feedback is less actionable than granular feedback).

### Kiosk Success Flash as Feedback Loop

The green full-screen flash after check-in is a feedback loop: the student performed a behavior (tapped their tile), and the system immediately confirmed the outcome (attendance recorded, identity acknowledged). The feedback is immediate (within 1 second), clear (green = success; a separate state for already-checked-in prevents double-tap confusion), and specific (the student's name is displayed, confirming whose record was written).

The stripe progress display — "X classes toward your next stripe" — extends this feedback into the motivational dimension. It is specific (a number, not a vague "you're making progress"), immediate (shown at the moment of check-in), and emotionally resonant (it connects today's action to a meaningful future milestone). Without this display, the check-in is a completed transaction with no visible connection to outcome. With it, the check-in becomes a counted vote for the identity "I am getting closer."

### Belt Stripe Progress as a Feedback Loop

The stripe system itself is a feedback mechanism that exists outside DojoFlow — the physical stripes are applied to the belt — but DojoFlow's job is to make the underlying data available and visible so the feedback can be accurate and consistent. If the instructor does not know how many classes a student has attended since their last promotion, they cannot give accurate feedback at the right moment. The class count on the student profile and the check-in success screen are what make the stripe system work as a feedback loop rather than an approximation.

### Teaching Sessions Badge as Instructor Feedback

The "X teaching sessions" count badge on assistant instructor profiles in StudentDetail is feedback for the instructor reviewing the record — not the student. It makes a usually invisible quantity (how many times has this student served as a teaching assistant?) immediately visible and specific. The design decision to show "0 teaching sessions" on profiles with no logged sessions is intentional: it surfaces the gap rather than hiding it, creating a prompt for retroactive annotation and an accurate baseline from which future counts are measured.

---

## Applied to DojoFlow: Choice Architecture Audit

Any DojoFlow feature can be audited against a consistent set of choice architecture questions. Apply this audit before shipping and again in QA.

**What is the default? Is it the right default?** For every form field, toggle, and workflow entry point: what happens if the user takes no action? Is that outcome the one that serves most users in most cases? For student creation during a walk-in trial, the default status of "Trial" is correct — most students created in that context are trials. For attendance marking, the default state of "not yet present" is correct — the instructor marks present, not absent, which prevents accidental mass-absence records. Check every default against the question: if this user accepts this without thinking, are they better off or worse off?

**Where is the sludge? What friction can be removed?** Identify every step in the workflow that requires user action. For each step, ask whether it produces information the system uses or prevents an error that cannot be caught elsewhere. Remove every step that fails this test. In the Suggested Sends approval flow, the minimum necessary steps are: read the draft, optionally edit, tap approve. Any step beyond these is sludge.

**Is the timing right?** Apply the EAST Timely test: is this nudge, prompt, or feedback appearing at the moment when the user is most receptive and the behavior is most relevant? Suggested Sends at 14 days: yes. "Teaching today?" during the check-in success window: yes. Contact completeness warning on the Students page when the instructor is already looking at students: yes. A billing configuration prompt during kiosk check-in: no.

**What feedback does the user get? Is it immediate?** After every action, the user should receive a signal that confirms the outcome. The signal must appear immediately (within 1 second), must be unambiguous (green for success, a distinct state for error), and must be specific enough to confirm which record was affected. Silent form submissions, spinners without confirmation, and success states that disappear before they register are feedback failures.

**Are we preserving choice while guiding toward good outcomes?** Every nudge in DojoFlow must pass the libertarian paternalism test: can the user deviate easily and without penalty? The Suggested Sends review flow passes: the instructor can edit, dismiss, or ignore any message. The kiosk check-in passes: there is no lock state, records can be corrected. A system that sent follow-up emails automatically without instructor review would fail this test — and must never be built.

**Who is the choice architect here — us or accident?** For every feature, identify which choices the architecture is making on the user's behalf. If any of those choices were made by convention, framework default, or designer inertia rather than deliberate analysis, revisit them. The order of navigation items, the sort order of the student list, the first tab open on a student profile, the label on the primary call-to-action button — all of these are choice architecture decisions. Own them.
