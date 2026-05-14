# Jobs-to-Be-Done (JTBD)

## Core Idea

People don't buy products — they hire them to make progress in a specific circumstance. The "job" is the underlying goal, not the feature request. A parent hiring a martial arts school isn't buying classes; they're hiring progress toward "my kid grows up disciplined and confident."

Understanding the job unlocks what to build, what to ignore, and how to talk about the product.

---

## The JTBD Structure

**Job statement:** `When [situation], I want to [motivation], so I can [outcome].`

Example for DojoFlow:
- When a student goes quiet for two weeks, I want to catch it before they disappear, so I can keep every student progressing.
- When a parent asks "how is my kid doing?", I want to answer with real data, not gut feel.

**Three layers of the job:**
1. **Functional** — the practical task (track attendance, send a follow-up email)
2. **Emotional** — how the user wants to feel (confident, in control, not anxious)
3. **Social** — how the user wants to be seen (professional sensei, attentive instructor)

The emotional and social layers are often more durable than the functional one. Build for all three.

---

## The Switch Moment

Users switch products (or do nothing) based on four forces:

- **Push** — frustration with the current situation (spreadsheets are embarrassing)
- **Pull** — attraction to the new solution (DojoFlow looks like it actually works)
- **Anxiety** — fear of the switch going wrong (what if I lose data?)
- **Habit** — comfort with the status quo ("I know how my spreadsheet works")

Push + Pull must outweigh Anxiety + Habit for a switch to happen. If adoption is slow, diagnose which force is dominant before adding features.

---

## How to Apply It

**Scoping features:** Before building, ask "what job does this feature get hired for?" If you can't name the job, don't build it. If two features serve the same job, build only the one that serves it better.

**Prioritization:** Jobs with the most push (user pain) and the highest frequency are highest priority. DojoFlow's core job — "don't let students leave silently" — is high-pain, high-frequency, and currently served by nothing.

**Copy and positioning:** Lead with the outcome, not the feature. "Keep every student progressing" beats "attendance tracking and automated reminders."

**Discovering jobs:** Listen for the narrative around when/why people started looking for a solution. The trigger event and the first thought are gold. (See also: Mom Test skill.)

---

## Common Failure Modes

- **Feature tourism** — building features for jobs nobody hired you for, because they sound cool
- **Demographic targeting** — assuming all small dojo owners have the same job (they don't — a competitive tournament school has different jobs than a family rec program)
- **Job inflation** — making the job statement so broad it could justify anything ("help instructors do their job better")
- **Mistaking the functional for the whole** — building a great attendance tracker but ignoring the emotional job of "feel like a professional"
- **Serving the buyer's job, not the user's job** — the owner who pays is not always the instructor who uses it daily; their jobs differ

---

## Applied to DojoFlow

Core job (validated Mar 2026, White Crane pilot): **"Help me keep every student progressing so none leave silently."**

All features should be evaluated against this. A feature that doesn't help the sensei prevent silent churn is a distraction, regardless of how technically interesting it is.

Sub-jobs in priority order (pilot feedback):
1. Surface students who are at risk before they're already gone (absence tracking, risk indicators)
2. Reach out to at-risk students in a way that doesn't feel like spam (Magic Text, segmented broadcast)
3. Know who to call without hunting through a spreadsheet (contact completeness)
4. Handle a belt test without scrambling (readiness badges, test eligible dates)
