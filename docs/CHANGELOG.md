# Changelog: andrewchristison.com

All notable changes to this project, newest first.
Format: What it does. Why it matters.

---

## 2026-05-15

- **Solitaire shipped, fully playable.** Klondike, single-card draw. Drag-and-drop for moves, double-click face-up tops to auto-send to a foundation, click stock to draw or recycle. Win triggers the classic Win95 card-bounce cascade: cards launch from the foundations with randomized velocities, fall under gravity, bounce off the viewport bottom with 0.7 energy loss, and slide off-screen. `ANDREW WAS HERE` banner overlays the felt. New Game button resets the deal. Warm crosshatch card backs (deep amber on dark brown) and a sage-green felt that fits the Peninsula palette. Reduced-motion skips the cascade but keeps the banner.

- **Refactor:** `.ms-banner` CSS class renamed to `.game-banner` so Minesweeper and Solitaire share the same banner styling. IDs stay per-window.

- **Minesweeper became a real game.** Replaced the static "ANDREW WAS HERE" board with a functional 9x9 / 10-mine Minesweeper. First-click safety, cascade reveal, right-click flags, classic colored numbers (1=blue through 8=gray), live timer and mine counter, smiley reset button with "oh" face on mouse-down. Win and loss overlay a semi-transparent `ANDREW WAS HERE` banner. Game resets when the Minesweeper window is closed and reopened, but persists across minimize/restore (fixed an open-hook bug that was resetting on every restore).

- **Run dialog UX overhaul.** Input now reliably auto-focuses on open via a double-rAF (post window-open animation). Enter submits. After submit: input clears, refocuses, output line flashes paper-yellow for 240ms, soft click sound. Result: typing `goats` then Enter then `miles` feels like sitting at a Win95 prompt instead of fighting form widgets.

- **Cursor trails got dramatic.** Replaced the dim 14px dot with a chevron-shaped cursor-arrow ghost. Lifetime extended from 360ms to 720ms, spawn cadence tightened from 24ms to 14ms (denser), cap at 24 live nodes. Initial opacity 0.72, animated scale-down 1.0 → 0.55 over the lifetime. Still respects `prefers-reduced-motion`.

- **Shipped 8 new Easter eggs and a privacy page.** Screensaver (60s idle starfield), Internet Explorer icon ("Try going outside" → pondlog.co), Minesweeper window with "ANDREW WAS HERE" hidden in cells, drag-to-Recycle-Bin with crumple+respawn, Clippy / Snoop Guide that asks if you'd like help after 4 unique windows, Win95 Run dialog with 4 hidden commands, draggable desktop icons that swap on drop, and a cursor trails toggle in Start → Settings → Mouse. Every animated egg respects `prefers-reduced-motion`. Full inventory in `docs/EASTER_EGGS.md`.

- **Restructured the Start menu with click-expand submenus.** Programs and Settings now host nested menus (Games → Minesweeper, Mouse → Cursor trails). Added Run..., Internet Explorer, and Privacy as first-class entries. The "andrew" rail-text became "© 2026 Andrew Christison" running vertically along the menu's left edge.

- **Added `/privacy.html`.** Standalone Win95-styled window page. No cookies, no analytics, no forms; lists the external sites the home page links out to and the localStorage sound-prefs surface. Linked from Start → Privacy and added to `sitemap.xml`. Footer carries the full "© 2026 Andrew Christison. All rights reserved."

- **First commit of the actual site.** The full Win95-inspired desktop (about 98 KB of index.html), favicon.svg, assets/og-image.png, .gitignore, and assets/photos/ all enter version control. Prior commits were scaffold and skills only; the site itself lived only on disk.

- **Shipped SEO/GEO infrastructure.** Added robots.txt, sitemap.xml, llms.txt, humans.txt, canonical link, Open Graph block, Twitter card block, and JSON-LD Person schema in index.html head. The site is now legible to traditional crawlers (Google, Bing) and to LLM crawlers (llms.txt, schema.org Person), without changing any visible UI or window behavior.

- **Replaced data-URI favicon with external favicon.svg.** Mushroom mark now ships as a real file at the root, picked up by browsers and feed readers that don't parse data URIs. The Win95 four-pane data-URI that previously lived inline in index.html is gone.

- **Locked a single canonical source for identity facts.** Andrew's name, role, location, products, and external links express the same values across robots.txt, sitemap.xml, llms.txt, humans.txt, meta description, OG, Twitter, and JSON-LD. DRY for content. Future updates touch one place per fact, not seven.

## 2026-05-14

- **Project scaffold created.** CLAUDE.md, BRIEF.md, STICKIES.md, and supporting docs initialized. 56 skills synced from gundry-agents and pruned. Foundation set for build sessions.

- **Creative brief finalized.** Desktop metaphor, content architecture, design direction, window behavior, Easter eggs, and mobile approach locked in BRIEF.md. Every build decision traces back to it.
