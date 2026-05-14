# Microinteractions

## Core Idea

Microinteractions are the small, functional animations and responses that happen around a single use case — a toggle switching, a message sending, a check-in confirming. They are not decoration. They are the product's way of communicating: "I heard you. Here's what happened."

Done well, microinteractions make technology feel human. Done poorly (or omitted), they make it feel unresponsive and cold. In a product like DojoFlow where trust is the core value, every interaction that goes unacknowledged is a small erosion of confidence.

---

## The Four-Part Structure

Every microinteraction has four components:

### 1. Trigger
What initiates the microinteraction — user-initiated (tap, click, scan) or system-initiated (a new absence is detected, a student becomes belt-eligible).

- **User trigger:** Student scans QR code at check-in
- **System trigger:** DojoFlow detects a student hasn't attended in 14 days

Design the trigger to be discoverable (user) or attention-appropriate (system). A system trigger that fires at the wrong moment is an interruption, not a service.

### 2. Rules
What happens when the trigger fires — the logic that determines the outcome. Rules are invisible to the user but felt in the result.

- One trigger → one clear outcome (don't branch inside a microinteraction)
- Rules should handle edge cases silently (duplicate check-in → idempotent, no error flash)
- Keep rule complexity out of the UI; the interface expresses the result, not the logic

### 3. Feedback
The part the user sees, hears, or feels. Feedback is how the microinteraction communicates its rules.

**Good feedback is:**
- **Immediate** — under 100ms feels instantaneous; over 1s needs a loading state
- **Proportional** — a destructive action warrants more feedback than a toggle
- **Specific** — "Kai checked in at 6:02 PM" beats a generic success toast
- **Ephemeral** — it appears, conveys information, then gets out of the way

**DojoFlow feedback examples:**
- Check-in flash: green pulse + student name + timestamp on the class view
- Belt promotion: momentary confetti burst + "🥋 Kai promoted to Blue Belt" banner
- Send confirmation: "Message sent to 12 families" with a fade-out after 3s
- At-risk flag: subtle amber dot on the student card, not a modal interruption

### 4. Loops and Modes
- **Loop:** Does the microinteraction repeat? What happens the second and tenth time? (Check-in beep on first scan vs. "already checked in" on duplicate)
- **Mode:** Does the microinteraction change the larger UI state? (Enabling Magic Text mode changes the compose field's behaviour — that's a mode)

Loops that feel good the first time often feel annoying at scale. Design for the 100th use, not the first.

---

## How to Apply It

**Before building any interactive element, define all four parts explicitly.** Write them in a comment or PR description:
- Trigger: what fires it
- Rules: what the logic is
- Feedback: exactly what the user sees/hears
- Loop/Mode: how it behaves on repeat or state change

**Animation timing reference:**
- 0–100ms: instant (state toggles, button presses)
- 100–300ms: snappy (card expansions, drawer opens)
- 300–500ms: considered (screen transitions, data loads)
- 500ms+: always show a loading indicator

**Use motion to communicate direction and hierarchy.** A check-in card that slides in from the bottom communicates "this is new". A student card that fades out communicates "this is resolved". Motion that doesn't communicate anything should be cut.

---

## Common Failure Modes

- **No feedback** — the user clicks and nothing happens; they click again; now it fires twice
- **Generic feedback** — "Success!" tells the user nothing; "Kai checked in" tells them everything
- **Feedback that outlasts its usefulness** — a success toast that stays for 8 seconds becomes a UI element to work around
- **Microinteractions that lie** — showing a green flash before the server confirms the check-in; if the request fails, the user has been told the wrong thing
- **Overlooking system triggers** — the at-risk notification that fires mid-class is worse than no notification at all
- **Animating everything** — motion applied uniformly has no meaning; reserve it for moments that matter

---

## Applied to DojoFlow

The dojo office is often chaotic — class starting, parents arriving, phone ringing. Every microinteraction must work in that context: fast, legible at a glance, and non-interruptive unless truly urgent.

Priority microinteractions to get right:
1. **Check-in confirmation** — must be instant and student-specific; the instructor glances up from the mat
2. **At-risk flag appearance** — ambient, not alarming; a dot or badge the instructor notices between tasks
3. **Message send confirmation** — close the loop so the sensei knows the family was reached
4. **Belt promotion** — the one moment where celebration is appropriate; earn the delight
5. **Form validation** — inline, immediate, never on submit-only; missing email should surface on blur
