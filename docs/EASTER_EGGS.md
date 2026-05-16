# Easter Eggs: andrewchristison.com

_Inventory of hidden content and interactions. Each entry: what it is, where it lives, how it's triggered, and what the visitor finds._

---

## Built

### EE-001: Recycle Bin
**Location:** Desktop icon (and Start menu).
**Trigger:** Click the Recycle Bin icon.
**Content:** Opens a window listing "things I was sure of at 18" with the footer "1 item · the rest got composted."

### EE-002: Notepad
**Location:** Desktop icon (and Start menu).
**Trigger:** Click the Notepad icon.
**Content:** A short, personal note from Andrew to himself.

### EE-003: Shut Down overlay
**Location:** Start menu → Shut Down...
**Trigger:** Click Shut Down.
**Content:** Full-screen overlay reading "Andrew has stepped away." with subtext "Click anywhere to wake up." Click or Escape dismisses with a soft chime.

### EE-004: Konami code (dusk wallpaper)
**Location:** Anywhere on the page.
**Trigger:** Up, Up, Down, Down, Left, Right, Left, Right, B, A.
**Content:** Wallpaper warms to a dusk/sunset variant. A second sequence toggles it back. Plays an unlock arpeggio.

### EE-005: Screensaver (added 2026-05-15)
**Location:** Full-viewport overlay above windows, below modals.
**Trigger:** 60 seconds of no pointermove, pointerdown, keydown, wheel, or touchstart.
**Content:** A starfield drifting outward from center on a near-black background. Any input dismisses and resets the idle timer. Respects `prefers-reduced-motion`: shows a dimmed overlay with the "andrewchristison.com" wordmark instead of animation.

### EE-006: Internet Explorer (added 2026-05-15)
**Location:** Desktop icon (blue "e" with gold orbital ring) and Start menu → Programs → Internet Explorer.
**Trigger:** Click.
**Content:** Small window: "This browser has been retired. Try going outside." with a link to pondlog.co (opens in a new tab).

### EE-007: Minesweeper (added 2026-05-15, made playable same day)
**Location:** Start menu → Programs → Games → Minesweeper.
**Trigger:** Click.
**Content:** Functional Minesweeper. 9x9 beginner board, 10 mines, first-click safety (mines placed only after first click, never on the clicked cell or its 8 neighbors). Left-click reveals (cascade-reveals empty regions); right-click toggles a flag. The mine counter shows mines remaining (`MINES − flags`, can go negative for over-flagging). The timer counts seconds while in play, max 999. Smiley face is the reset button and shows live state: ☺ while idle/playing, 😮 while a click is in progress (mouse-down feedback), 😎 on win, 💀 on loss. On win the remaining mines auto-flag; on loss all mines reveal with the clicked one highlighted in red. Both outcomes overlay a 60% alpha `ANDREW WAS HERE` banner that dismisses on click.

### EE-008: Drag to Recycle Bin (added 2026-05-15)
**Location:** Any desktop icon dropped onto the Recycle Bin.
**Trigger:** Drag a desktop icon and release while hovering the Recycle Bin.
**Content:** Icon vanishes with a band-pass-filtered crumple sound, waits 3 seconds, then respawns at its original position with a "nice try" tooltip that fades after 2 seconds. The icon's window is still reachable from the Start menu during the pause.

### EE-009: Clippy / Snoop Guide (added 2026-05-15)
**Location:** Slides up from bottom-right above the taskbar.
**Trigger:** Once per session, after 4 unique windows have been opened.
**Content:** Inline-SVG paper clip with eyes. Speech bubble: "It looks like you're exploring someone's entire life. Would you like help?" Two buttons: **Yes** opens About; **No, I'm snooping** replies "Respect." for ~1.2s then Clippy slides away. Reduced motion swaps the slide for a fade.

### EE-010: Run dialog (added 2026-05-15)
**Location:** Start menu → Run...
**Trigger:** Click.
**Content:** Win95 Run-box-styled window. Submit (Enter or OK) to evaluate:
- `hello` → Hello World.
- `goats` → Currently: 2. Named: yes.
- `miles` → 4:38:39
- `help`  → Try going for a run.
- anything else → Bad command or file name.

### EE-011: Desktop icon reorder (added 2026-05-15)
**Location:** Any desktop icon.
**Trigger:** Drag an icon onto another icon's slot.
**Content:** The two icons swap positions in the grid. The Recycle Bin is fixed (cannot be moved; only acts as a drop target). Arrangement is session-only; reload restores the default order.

### EE-012: Cursor trails (added 2026-05-15)
**Location:** Start menu → Settings → Mouse → Cursor trails (toggle).
**Trigger:** Toggle on.
**Content:** Small accent-soft dots fade behind the pointer as it moves. Off by default. Disabled (and not rendered) under `prefers-reduced-motion`.

### EE-clock-right-click
**Location:** Right-click the taskbar clock.
**Content:** Time-of-day-aware tooltip ("morning is for clarity", "evening", "still up?") that fades after ~2.4 seconds.

### EE-devtools-message
**Location:** Browser developer tools console.
**Content:** A welcome paragraph naming the konami code and shutdown button. Greets curious developers without giving everything away.

### EE-copyright-rail
**Location:** Vertical sidebar of the Start menu (Win95-idiom placement). Added 2026-05-15.
**Content:** "© 2026 Andrew Christison" reading bottom-to-top along the left edge of the Start menu. Only visible while the Start menu is open.

---

## Planned (Not Yet Built)

_New ideas land here before they ship. Currently empty; the planned items from v1 are now built._
