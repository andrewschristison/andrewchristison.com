# Refactoring UI

## Core Idea

Good UI is not about taste — it's about decisions. Almost every design problem can be solved by working through a checklist of specific, learnable decisions. The goal is a UI that communicates hierarchy, trust, and state clearly — not one that's "pretty."

---

## The Most Important Decisions

### 1. Visual hierarchy — not everything is equally important

Every screen has one primary action, a few secondary ones, and a lot of supporting content. Your type sizes, weights, and colors should make that hierarchy obvious without the user having to think.

- **One font weight for primary content, one for secondary, one for disabled** — three levels is usually enough
- **Muted foreground (`text-muted-foreground`)** for everything that supports but doesn't lead
- **Never use pure black** — `text-foreground` at 90% opacity reads better and feels more refined
- If everything is bold, nothing is bold

### 2. Spacing — use more of it than feels comfortable

Under-spaced UIs feel dense and untrustworthy. When in doubt, add more space.

- **Scale your spacing system** — use 4/8/12/16/24/32/48px steps; never eyeball it
- **Group related things tightly, separate unrelated things generously** — spacing communicates relationship
- Card padding should be at minimum 16px; usually 20-24px feels right
- Don't shrink padding to fit more content — truncate or rethink the layout

### 3. Color — don't use it decoratively

Color should communicate meaning, not decorate. Common uses:
- **Primary** — the one action you want the user to take
- **Destructive/red** — irreversible actions, errors
- **Amber/yellow** — warnings, things that need attention (absence risk, expiring payments)
- **Green** — active, healthy state, success
- **Muted** — secondary information, metadata

If you use amber for something that isn't a warning, you've corrupted the signal.

### 4. Borders are usually the wrong solution

When you reach for a border to separate content, ask if whitespace would do the job without the visual noise. Most nested borders create "div soup" that makes the UI feel heavy.

Use borders for:
- Separating a sidebar from main content
- Cards that need to stand out from a colored background
- Input fields (need affordance)

Avoid borders for:
- Separating items in a list — use spacing
- Visual grouping within a card — use a subtle background or spacing

### 5. Empty states are product moments

An empty state is a user's first experience with a feature. It should:
- Explain what goes here
- Tell the user what to do to fill it
- Look intentional, not like an error

Never show a blank space. Never show "No records found." Show an illustration, a clear label, and a primary action.

### 6. Buttons — three variants maximum

- **Primary** — filled, one per screen, the most important action
- **Secondary/outline** — bordered, lower-priority actions
- **Ghost** — text-only, tertiary actions, icon buttons

If you have two primary buttons on a screen, one of them is wrong.

---

## Typography Decisions

- **Size scale:** 12, 14, 16, 18, 20, 24, 30px — stay on the scale
- **Line height:** body text wants ~1.5; headings want ~1.2
- **Line length:** 60-75 characters for readable paragraphs — wider than that and readers lose their place
- **All-caps labels:** fine for section headers (uppercase + tracking), terrible for body content
- **Truncation:** always better than wrapping in tight spaces; use `truncate` + `title` attribute so content is accessible

---

## Badges and Tags

Use badges to communicate status, not just to add color. Every badge color should have a consistent meaning across the entire app:
- Green = active / success
- Amber = warning / needs attention
- Red = error / destructive / inactive
- Blue = informational / in-progress
- Gray/outline = neutral / secondary

If the same color means different things in different parts of the app, the UI stops communicating and starts decorating.

---

## Common Failure Modes

- **Shadow everywhere** — shadows are for elevation; if every card has a heavy shadow, nothing has elevation
- **Gradient abuse** — gradients on backgrounds rarely add meaning; they add noise
- **Inconsistent border-radius** — pick one radius per component type and stick to it
- **Icon inflation** — icons next to every text label don't add clarity, they add clutter; use icons purposefully
- **Over-disabled states** — graying out half the UI confuses users; prefer hiding or contextual messaging
- **Alert dialog for non-destructive actions** — confirmation dialogs should only appear when the action is irreversible

---

## Applied to DojoFlow

The app uses shadcn/ui which provides a good baseline. Watch for:
- Amber consistently = warning (absence risk, expiring payments, program tags on classes — all correct)
- Green consistently = active state
- Destructive (red) for sign out, delete, revoke — keep this consistent
- Empty states on Programs, Classes, Students should have an action button, not just text
- Card padding: use `p-4` minimum, `p-6` for primary content cards
- Section labels within cards: `text-xs font-medium text-muted-foreground uppercase tracking-wide` — this pattern is already used and should remain consistent
