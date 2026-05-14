# UX Heuristics (Nielsen's 10 + Practical Extensions)

## Core Idea

Good UX isn't subjective — it can be evaluated against a set of principles. Nielsen's 10 heuristics are the most durable framework for identifying usability failures before they reach users. When reviewing UI decisions, run through these as a checklist, not a vibe check.

---

## Nielsen's 10 Heuristics

### 1. Visibility of System Status
The system should always keep users informed about what's going on, through appropriate feedback within reasonable time.

**In practice:**
- Loading states on every async operation (skeleton loaders, spinners)
- Progress indicators for multi-step operations (broadcast send: "Sending 3/12...")
- Success/error feedback after mutations (toast notifications)
- Pending states on buttons after click (disable + show spinner)

**Failure modes:** Silent failures, buttons that do nothing visibly, background jobs with no status.

### 2. Match Between System and Real World
The system should speak the users' language. Use words, phrases, and concepts familiar to the user, rather than system-oriented terms.

**In practice:**
- "Belt Test Candidates" not "students where next_test_eligible_date ≤ today + 30"
- "Lapsed Students" not "inactive_attendance_segment_30d"
- "Absent 2+ Weeks" not "attendance_gap_14_days"
- Money displays as "$120/mo" not "monthly_tuition: 120.00"

**Failure modes:** Database column names surfacing in UI, developer-friendly labels instead of user-friendly ones.

### 3. User Control and Freedom
Users often choose system functions by mistake. They need an "emergency exit" — undo, cancel, back.

**In practice:**
- Confirm dialogs before destructive actions
- "Cancel" on every modal and form
- Back navigation in detail views
- Soft deletes / undo for deletions where feasible

**Failure modes:** No confirmation before deleting a student. No way to cancel a broadcast mid-send. Forms with no cancel button.

### 4. Consistency and Standards
Users shouldn't have to wonder whether different words, situations, or actions mean the same thing.

**In practice:**
- Badge colors: amber = warning, green = active, red = danger — always
- Destructive actions always use `variant="destructive"` button
- Date formats consistent across all pages (parseLocalDate pattern)
- Action placement consistent: primary action top-right, destructive action bottom or separate

**Failure modes:** "Archive" in one place, "Deactivate" in another for the same concept. Badge colors with different meanings per page.

### 5. Error Prevention
Better than good error messages is a careful design which prevents a problem from occurring in the first place.

**In practice:**
- Disable "Send" until a recipient segment is selected and a message is composed
- Validate email format before submit, not after
- Confirm when a bulk action affects more than N records
- Make the dangerous zone visually distinct (red section for revoke/delete)

**Failure modes:** Submitting a form that will fail because of missing data. Allowing enrollment in an inactive class.

### 6. Recognition Over Recall
Minimize the user's memory load. Objects, actions, and options should be visible or easily retrievable.

**In practice:**
- Show linked class names on program cards (don't make users remember which class belongs to which program)
- Show last message sent date in communications history
- Keep filters visible as chips/tags, not hidden in a menu
- Belt level shown with color indicator, not just a text string

**Failure modes:** Users have to navigate away to check a piece of information they need for the current decision. Empty field labels with no placeholder or example.

### 7. Flexibility and Efficiency of Use
Accelerators — unseen by novice users — may speed up the interaction for expert users.

**In practice:**
- Keyboard shortcuts for power users (mark present, navigate to next student)
- Quick search on long lists
- Bulk actions for common operations (mark all present, enroll multiple students)
- Pre-filled defaults based on previous actions

**Failure modes:** Every operation requires 5 clicks; no shortcuts. Re-entering the same information every time.

### 8. Aesthetic and Minimalist Design
Every extra unit of information in a dialogue competes with the relevant units of information and diminishes their relative visibility.

**In practice:**
- Remove fields and columns that aren't acted on
- Don't show billing information if billing isn't live
- Hide advanced options behind an "Advanced" toggle
- One primary action per screen; secondary actions de-emphasized

**Failure modes:** Tables with 12 columns, 3 of which are ever read. Dashboard KPIs that aren't linked to any action. Long forms with rarely-needed fields.

### 9. Help Users Recognize, Diagnose, and Recover from Errors
Error messages should be expressed in plain language, precisely indicate the problem, and constructively suggest a solution.

**In practice:**
- "Couldn't send message — check your Postmark configuration" not "Error 500"
- "No students match this segment" with a link to fix the segment filter
- Form validation errors next to the relevant field, not just at the top
- If a mutation fails, preserve the user's input

**Failure modes:** Generic "Something went wrong." No guidance on how to fix it. Form resets on error, losing the user's input.

### 10. Help and Documentation
Even though it is better if the system can be used without documentation, it may be necessary to provide help. Focus on the user's task.

**In practice:**
- Tooltips on non-obvious UI elements (what does "segment" mean to a first-time user?)
- Inline helper text below form fields
- Empty states that explain the concept, not just "no data"
- First-run onboarding that demonstrates core value immediately

**Failure modes:** Dashboard shows all zeros with no explanation of how to get started. Belt rank field with no indication of valid values.

---

## Extended Heuristics (Practical Additions)

### 11. Appropriate Defaults
Pre-fill the most likely answer. Make the path of least resistance the right path.
- New class defaults to today's day of week
- Attendance form defaults to today's date
- New student defaults to "active" status

### 12. Progressive Disclosure
Show the minimum needed to make a decision; reveal complexity only when the user asks for it.
- Student list: name, belt, status, attendance % — that's enough; full profile on click
- Program card: name, count, risk — classes inline but details on drill-down
- Form fields: required fields first, optional behind "Show more"

### 13. Feedback Loops Close to the Action
Feedback should appear where the action was taken.
- Inline toast ("Program updated") near the save button, not in the corner
- Validation error adjacent to the field, not at form top
- "Copied!" appears on the icon button that was clicked, not elsewhere

---

## Applying Heuristics in Code Review

When reviewing UI changes, scan for:
1. Does every async action show loading state and error state?
2. Is there a way to undo or cancel every significant action?
3. Do all labels match user language, not developer language?
4. Are badge/color meanings consistent across pages?
5. Is the primary action obvious? Is there only one?
6. Does the empty state explain what to do?

---

## Applied to DojoFlow

High-value heuristic improvements:
- **Heuristic 1:** Broadcast send progress (already done: "Sending 3/12") ✓
- **Heuristic 2:** "Students haven't attended in 2+ weeks" not "absent_2_weeks segment count" ✓
- **Heuristic 4:** Amber = warning used consistently (absence risk, expiring payments, program tags) ✓
- **Heuristic 6:** Linked classes now inline on program cards ✓ (previously required navigation)
- **Heuristic 8:** Billing placeholder language removed from Programs page ✓
- **Heuristic 10:** Empty states on all key pages should have action buttons, not just explanatory text
