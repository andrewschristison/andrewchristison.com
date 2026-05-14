# The Pyramid Principle

## Core Idea

*The Pyramid Principle* by Barbara Minto is the most influential framework for structured communication in professional settings. Its central claim: the natural order of human thought is deductive — we receive a point, then evaluate the evidence. Most people communicate in the reverse order — evidence first, conclusion buried at the end. This is the source of almost all unclear writing and unclear thinking.

The pyramid reverses the sequence: state the governing thought first, then support it. The reader knows where you're going before you take them there. Every supporting point answers a question the reader is already asking.

---

## The Pyramid Structure

A pyramid has one governing thought at the top. Below it are groupings of supporting arguments. Below those are the facts and data that validate each argument.

```
               ┌─────────────────────┐
               │   Governing Thought  │
               └─────────────────────┘
              /           |           \
     ┌────────┐      ┌────────┐      ┌────────┐
     │  Key   │      │  Key   │      │  Key   │
     │ Point 1│      │ Point 2│      │ Point 3│
     └────────┘      └────────┘      └────────┘
      /      \        /      \        /      \
  [data]  [data]  [data]  [data]  [data]  [data]
```

**The governing thought answers the question the reader has before they start reading.** Everything else exists to support it.

---

## SCQA — The Opening Frame

Before the pyramid, Minto prescribes a situational opening that earns the right to state the governing thought. The SCQA framework:

### Situation
The context the reader already knows — the stable state before the problem. Brief. Shared. Not where the insight lives.

> "DojoFlow has been live at White Crane for three months."

### Complication
The disruption to the stable situation — what changed, what went wrong, what tension arose. This is what makes the document necessary.

> "We've learned that senseis can't use the communications features because over half of their students have no email address on file."

### Question
The question the complication raises in the reader's mind — the question the document will answer. State it explicitly.

> "What should we build next to unblock email communications?"

### Answer
The governing thought — the answer to the question. This is the top of the pyramid. Everything else is support.

> "We should build contact completeness warnings before building any new email features — the lever is worthless without the addresses."

The SCQA opening earns the reader's attention by matching their mental model (Situation), disrupting it (Complication), surfacing the natural question (Question), and then answering it directly (Answer). No preamble, no suspense, no burying the lede.

---

## Top-Down vs Bottom-Up Construction

### Top-Down (Deductive)
Start with the governing thought. Then ask: what question does this raise? Then answer that question. Then ask what question *that* raises. Continue until you reach supporting data.

Top-down is faster to construct when you already know your conclusion. Use it for communication documents.

```
Governing thought: "Build contact completeness first."
→ Why? Because email campaigns won't work without addresses.
→ Why not? 53% of students have no resolvable email.
→ How do we know? Query of current student data.
→ What does that mean? Every email feature we build is currently worthless.
```

### Bottom-Up (Inductive)
Start with the data. Look for the idea that groups the data. State the insight the data supports. Roll it up to a governing thought.

Bottom-up is slower but useful when you don't yet know what the data says. Use it for analysis; convert to top-down for the final document.

**In practice:** most documents should be written top-down even if they were researched bottom-up. The reader should receive conclusions, not your research journey.

---

## Grouping and MECE

Every grouping of points in the pyramid must be **MECE**: Mutually Exclusive, Collectively Exhaustive.

- **Mutually exclusive:** no overlap between points — two points don't cover the same ground
- **Collectively exhaustive:** together, the points cover all the ground — nothing important is left out

MECE prevents two common failures:
1. **Overlap:** supporting points that say the same thing twice, giving false impression of multiple reasons
2. **Gaps:** supporting points that prove only part of the case, leaving the reader with unanswered objections

**Testing MECE:** after writing three supporting points, ask: (a) do any two points overlap? (b) could someone accept all three points and still reject the governing thought? If yes to either, the grouping is broken.

---

## The Governing Thought

The governing thought is not a topic. It is not a question. It is a complete, arguable claim.

**Not a governing thought:**
> "This document discusses our product roadmap."

**Not a governing thought:**
> "What should we build next?"

**A governing thought:**
> "The highest-leverage next build is contact completeness warnings, not new email features, because the email lever doesn't work without addresses."

A governing thought must be arguable — someone could disagree with it. A topic statement cannot be disagreed with. An arguable claim forces you to provide support.

---

## The Inductive vs Deductive Argument

Arguments in the pyramid take two forms:

### Deductive Arguments (syllogistic)
A chain of reasoning where each point follows from the last:

> All men are mortal.
> Socrates is a man.
> Therefore, Socrates is mortal.

Deductive arguments are tight but slow to read. Use for single, critical supporting arguments where the logic must be airtight.

### Inductive Arguments (grouping)
Multiple independent points that all support the same conclusion:

> Contact completeness is highest priority because:
> 1. Email features are worthless without addresses (blocks current features)
> 2. Addresses are fast to collect once the warning surfaces the gap (high leverage, low cost)
> 3. Pilots who see incomplete data take immediate action when prompted (validated by White Crane)

Inductive arguments are faster to write and faster to read. They require MECE grouping — the points must be genuinely independent.

**Most professional documents use inductive arguments.** Deductive arguments appear in legal briefs, technical proofs, and single-clause supporting points.

---

## Applying the Pyramid to Different Formats

### Memos and Emails
Opening sentence = governing thought. First paragraph = three supporting points stated as conclusions. Remaining paragraphs = evidence for each point. Subject line = governing thought compressed to 10 words.

### Presentations
Title slide = governing thought. Each subsequent slide = one supporting point (one claim per slide, never a topic header). Speaker notes = the evidence. The slides form the pyramid visually.

### PRDs and Feature Briefs
Opening = SCQA. Problem statement = the complication. Solution = governing thought. Rationale = MECE supporting points. Out of scope = what explicitly doesn't support the governing thought.

### Bug Reports / Incident Postmortems
Governing thought = the root cause and fix. Supporting points = (1) what happened, (2) why it happened, (3) what we changed. Evidence = logs, timeline, data.

---

## Common Failure Modes

- **Burying the conclusion** — building up evidence for three pages before stating the insight; the reader is lost or skips to the end anyway; lead with the answer
- **Topic headers instead of governing thoughts** — "Background" and "Considerations" are not claims; they are filing systems; every section heading should be an arguable point
- **Non-MECE groupings** — points that overlap (appear to be multiple reasons but are one reason restated) or that leave gaps (accept all three and still have a valid objection); breaks the pyramid's logical completeness
- **SCQA in the wrong order** — jumping to the answer before the complication is established; the reader hasn't been set up to care; the answer lands without weight
- **Padding the middle** — adding a fourth point that isn't necessary because "three feels thin"; MECE determines the count, not aesthetics; two tight MECE points beat four weak ones
- **Conclusions that aren't actionable** — governing thought is "the situation is complex"; this is a finding, not a recommendation; a governing thought should imply or state what to do

---

## Applied to DojoFlow

**The pyramid for DojoFlow's current roadmap decision:**

**Governing thought:**
> Build contact completeness warnings before building any new email features — the communication lever is worthless without addresses, and we can fix the address gap faster than building a new feature would take.

**Supporting point 1 (blocking dependency):**
> Email campaigns cannot reach students who have no email on file — the send mechanism is built, but over half the student records at White Crane have no resolvable email.

**Supporting point 2 (high leverage, low effort):**
> A warning badge on the Students list prompts immediate action from senseis — pilot feedback shows they update records when they can see the gap, not when we describe it in abstract.

**Supporting point 3 (sequencing logic):**
> Building bulk segmented email before addressing the data gap would deliver a feature that fails in production — undermining trust in the platform at the most critical stage of pilot adoption.

**MECE check:**
- Do any two overlap? No — (1) is about the current state, (2) is about the fix, (3) is about the cost of sequencing wrong.
- Can you accept all three and reject the conclusion? No — together they make the case that addresses must come before email features.

**SCQA for a product brief:**
- **Situation:** White Crane pilot is live; email features are built and ready to use.
- **Complication:** Over half of student records have no resolvable email; every email feature fires at ~50% of the intended recipients.
- **Question:** What do we build next to unlock the email communications roadmap?
- **Answer:** Contact completeness warnings — surface the gap before adding more features that depend on the gap being closed.
