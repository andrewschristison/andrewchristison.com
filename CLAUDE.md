# andrewchristison.com

> A Windows 95-inspired desktop environment. Not a portfolio site, not a blog, not a landing page. An explorable space where work and life coexist.

**This is andrewchristison.com.** A personal site for Andrew Christison.
Repo: ~/projects/andrewchristison.com
NOT Retencity. NOT Ask K. NOT DojoFlow. NOT Pondlog. NOT CropGraph.

If this file describes any other product, STOP and alert me — wrong file loaded.

## Target Reaction (First 3 Seconds)

**"oooo, cool. what's this?"**

## Read First

- `BRIEF.md` — Full creative brief. Every build decision traces back to this document.
- `docs/STICKIES.md` — Numbered persistent instructions. Load at every session start.
- `docs/SESSION_HANDOFF.md` — Current project state. What was just done, what's next.

## Tech Stack

- Single HTML file (or minimal bundle) with CSS and vanilla JS
- No framework, no build step
- Google Fonts via CDN
- Web Audio API for sound effects (no external audio files)
- Deployable as static site (Netlify, Vercel, any static host)
- No database, no API, no auth

## Directory Structure

```
/
├── CLAUDE.md                    # This file — project identity
├── BRIEF.md                     # Creative brief — read before any work
├── index.html                   # The site
├── assets/
│   └── photos/                  # Photo assets (headshot, homestead, bus, etc.)
├── docs/
│   ├── STICKIES.md              # Numbered session rules
│   ├── SESSION_HANDOFF.md       # Current state / handoff context
│   ├── CHANGELOG.md             # What shipped and why
│   ├── PRODUCT_DECISIONS.md     # Design & architecture decisions with reasoning
│   └── EASTER_EGGS.md           # Inventory of hidden content and interactions
├── .agents/
│   └── skills/                  # Strategy, design, and engineering skills
└── .claude/
    └── skills/                  # Mirror of .agents/skills/
```

## Core Interactions

Windows must be:
- **Draggable** by title bar
- **Minimizable** to taskbar (with indicator showing minimized state)
- **Closable** with recovery (reopen from desktop icon or start menu)
- **Stackable** with z-index management (click brings to front)
- **Resizable** if feasible

Taskbar fixed at bottom with: start button/menu, open/minimized window indicators, real-time clock.

Start menu is explorable, fun, and contains all windows plus Easter eggs.

## Content Sections (Windows)

| Window | State on Load | Description |
|--------|--------------|-------------|
| About | Open | Small, sticky-note sized. Photo, name, one human line. |
| Work | Open | Retencity (anchor), Ask K, Pondlog, CropGraph. Each links out. |
| Movement | Desktop icon | Martial arts lineage + running PRs. |
| Homestead | Desktop icon | Port Angeles, 6.5 acres, animals, family context, @theneighborshomestead. |
| The Bus | Desktop icon | 2002 school bus conversion, 2018-2019, @neighborbus. |
| Writing Space | Desktop icon | Low-pressure, uncategorized. Spatial not temporal. |
| Notepad | Easter egg | A note to self. |
| Recycle Bin | Desktop icon | Something unexpected inside. |

## Design Tokens

- **Palette:** Warm, not Microsoft grey. Aged paper, worn wood, Olympic Peninsula tones. See BRIEF.md.
- **Typography:** Monospace for system UI (window titles, taskbar, labels). Characterful font for content. No pixel fonts unless it earns it.
- **Chrome:** Win95 bevels adapted warm (light top-left, dark bottom-right). Tactile, satisfying.
- **Sound:** Subtle chimes and clicks. Easy to mute. Web Audio API, no external files.
- **Easter eggs:** Everywhere. Reward the curious. Track in docs/EASTER_EGGS.md.

## Links (External)

- retencity.com — primary professional presence
- ask-k.retencity.com — Ask K product
- pondlog.co — Pondlog product
- cropgraph.com — CropGraph product
- LinkedIn — linked contextually, not prominently
- @neighborbus (Instagram) — from bus window
- @theneighborshomestead (Instagram) — from homestead window

## Mobile

Desktop experience is priority. Mobile gets a different, adapted experience (vertical card stack preserving window aesthetic). It does not simulate a desktop on 375px.

## Out of Scope for v1

- In Process podcast (future desktop icon)
- DojoFlow / Banyan Stand (future work card or icon)
- CMS or writing tool — shelf is hand-coded
- Blog, RSS, email capture
- Deep SEO beyond basic meta tags
- Dark mode (potential future Easter egg via "Display Settings")

## Session Notes

### 2026-05-15: Full site commit + SEO/GEO infrastructure
First commit of the actual site (index.html and most assets were untracked until now). Added robots.txt, sitemap.xml, llms.txt, humans.txt, canonical link, Open Graph block, Twitter card block, and JSON-LD Person schema in the head. External favicon.svg replaces the inline data-URI. Zero visible UI changes. See PD-011, PD-012.

### 2026-05-15: Easter eggs + privacy + copyright
Built 8 new Easter eggs (EE-005 through EE-012): Screensaver, Internet Explorer, Minesweeper, Drag-to-Recycle-Bin, Clippy / Snoop Guide, Run dialog, Desktop icon reorder, Cursor trails. Restructured the Start menu with click-expand accordion submenus (Programs/Games, Settings/Mouse) plus Run..., Internet Explorer, and Privacy entries. Added vertical "© 2026 Andrew Christison" rail. Created `/privacy.html` and added it to the sitemap. All Easter egg state is session-only; only `ac-sound` lives in localStorage. See PD-013, PD-014, and `docs/EASTER_EGGS.md`.
