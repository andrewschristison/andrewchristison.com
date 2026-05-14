# The Design of Everyday Things

## Core Idea

*The Design of Everyday Things* by Don Norman argues that when people make mistakes with designed objects, the fault is almost always the design, not the person. Bad design creates confusion; good design makes correct use obvious and errors impossible or easily recoverable.

This matters for DojoFlow because the primary users — senseis and dojo administrators — are not software professionals. They're martial arts instructors who happen to manage a small business. Every moment of confusion in the interface is time taken away from teaching. Every error that requires support is a trust erosion event.

Norman's principles provide a vocabulary for diagnosing and fixing interface problems before users encounter them.

---

## Core Concepts

### Affordances
An affordance is a relationship between an object and a user that signals how the object can be used. A button affords clicking. A text field affords typing. A drag handle affords dragging.

**The problem:** digital affordances are not physical — a button and a non-interactive element can look identical. Affordances in digital design must be *signified* (made visible).

**Applied to DojoFlow:**
- The check-in button must look like a button (elevated, distinct, clearly tappable) — especially on mobile where the sensei is glancing up from the mat
- The walk-in trial capture button ("Walk-in Trial") must be visually distinct from the check-in flow; they're different actions with different consequences
- Belt rank progression entries in the timeline should not look interactive if they're not; if they are clickable, they must look it

### Signifiers
Signifiers are the cues that communicate how to use an affordance. A button has affordance (can be clicked) but the label and visual styling are the signifiers that communicate what clicking does.

**The gap between affordance and signifier is where confusion lives.**

Good signifiers:
- "Send to 12 families" on the email CTA (not just "Send")
- "Ready to Test" badge on a student card (not an unlabeled green dot)
- "Convert to Active" button on a trial student (not "Update Status")

Bad signifiers:
- An icon without a label in a context where the meaning isn't obvious
- A drag-and-drop interaction with no visual cue that dragging is possible
- An error state that shows a red border with no explanation

### Mappings
Mapping is the relationship between controls and their effects. Good mapping makes the relationship natural and requires no learning.

**Natural mappings use spatial or conceptual analogy:**
- A class roster sorted by last name alphabetically — the user's mental model of a list
- Belt ranks displayed in ascending order bottom-to-top (like a physical belt ladder on a wall)
- Student attendance heatmap: darker = more absences (darker = worse is a natural mapping)

**Bad mappings:**
- Displaying belt ranks in database insertion order instead of progression order
- An "at risk" filter that shows risky students when turned off and safe students when turned on
- Navigation that puts "Communications" under "Students" — the mental model of "I'm sending a message" doesn't start with "I'm managing students"

### Feedback
Feedback is the signal the system gives after an action is taken. Without feedback, users don't know if their action was received, is processing, or failed.

**Feedback principles:**
- **Immediate:** under 100ms feels instantaneous; over 300ms needs a loading indicator; over 1s needs a progress state
- **Informative:** "Sent to 12 families" beats "Done" beats nothing
- **Proportional:** destructive actions need stronger confirmation feedback than reversible ones

**DojoFlow feedback gaps to avoid:**
- Sending a Magic Text with no confirmation of delivery (did Postmark receive it? did it send?)
- Marking attendance with no flash or indicator on the student's row
- Submitting a belt promotion form with no visible success state before redirecting

### Conceptual Models
A conceptual model is the user's internal understanding of how the system works. Good design creates an accurate conceptual model through the interface itself — the user learns how the system behaves by interacting with it, without reading a manual.

**Mismatched conceptual models are the root of most support requests.**

Common mismatches to design against:
- Users think a student's email is the contact email for all communications; the actual model is more complex (adult vs minor, family-linked vs unlinked). The UI should make the resolution path visible.
- Users think "mark attendance" is per-class; the at-risk calculation is cross-class. The UI should communicate "at risk = missed all classes in 14 days" so the model is correct.
- Users think belt stripe counts reset only on promotion; they do, but only for color belts. Black belt behavior is different. The belt management view should make this visible.

### Human Error — Design, Not Blame

Norman's principle: **errors are design failures, not user failures.** When a user makes a mistake, the question is "how did the design allow this?" not "why didn't the user read the instructions?"

**Two types of error:**
1. **Slips** — the user had the right intention but executed incorrectly (tapped the wrong button because targets were too small)
2. **Mistakes** — the user had the wrong conceptual model (thought they were archiving a student, actually deleted them)

**Error prevention strategies:**
- Make destructive actions visually distinct and require confirmation (delete student → modal + "Type the student's name to confirm")
- Make irreversible actions obviously irreversible ("This cannot be undone")
- Constrain invalid inputs at the form level (a belt promotion date cannot be before the previous promotion date)

**Error recovery strategies:**
- Make most actions reversible where possible (archive instead of delete as default)
- Provide clear, actionable error messages ("This email is already associated with another family account — update the existing family instead")
- Never show raw error codes or database messages to users

---

## How to Apply Norman's Principles

Before shipping any new UI, run this checklist:

1. **Affordances:** Does every interactive element look interactive? Does every non-interactive element look static?
2. **Signifiers:** Does the label or visual treatment communicate what the action does, not just that an action exists?
3. **Mappings:** Is the spatial and conceptual layout consistent with the user's mental model of the domain?
4. **Feedback:** Does every action have an immediate, informative response?
5. **Conceptual model:** What model will the user build from this interface? Is it accurate?
6. **Errors:** What's the worst thing a user could do here? Can the design make it impossible, or at least recoverable?

---

## Common Failure Modes

- **Affordance without signifier** — interactive elements that look decorative; users discover actions by accident or not at all
- **Mapping inversion** — controls whose relationship to their effect is the opposite of intuitive; requires memorization
- **Silent actions** — operations that succeed or fail without any visible signal to the user
- **Irreversibility without warning** — destructive actions that execute without confirmation
- **Error messages that blame** — "Invalid input" tells the user nothing; "Email must include @" tells them exactly what to fix
- **Complexity shown to users** — exposing system state (database IDs, technical error codes, internal field names) to users who have no use for it

---

## Applied to DojoFlow

The DojoFlow interface is used by senseis who are often:
- Distracted (checking students in while managing a class)
- Mobile (using a phone or tablet, not a desktop)
- Not technically sophisticated (they know their dojo, not software)

Every interaction must work in this context. Specific areas to apply Norman's principles:

1. **Check-in flow** — target size on mobile must be finger-friendly; feedback must be visible from across a room; no ambiguity between "checked in" and "not yet checked in"
2. **Walk-in trial capture** — signifier must communicate "this creates a new student in the system" before the user taps; not just an icon
3. **Belt promotion form** — mapping should follow the natural progression; error prevention on date fields (can't backdate past previous promotion)
4. **Magic Text compose screen** — feedback on send must distinguish "draft saved," "sent to Postmark," and "delivered" — three different states
5. **Contact completeness warnings** — the warning badge must create a correct conceptual model: "this student has no way to be reached by email"
