# Product Decisions — andrewchristison.com

_Architectural and design decisions with reasoning. When a decision is revisited, the original reasoning prevents re-arguing settled questions._

---

## PD-001: Desktop Metaphor Over Traditional Site Architecture
**Date:** May 14, 2026
**Decision:** The site is a Windows 95-inspired desktop environment, not a traditional multi-page site or single-page scroll.
**Why:** Andrew's content spans professional (lifecycle marketing agency, SaaS products) and personal (martial arts, running, homesteading, family). A traditional site forces these into nav categories that feel disconnected. The desktop metaphor lets them coexist as discoverable windows in the same space — context does the work that explanation can't. It also earns the target reaction ("oooo, cool. what's this?") which a traditional layout cannot.
**Alternatives considered:** Single long-scroll page with anchored sections; multi-page site with nav; personal wiki/garden. All rejected for lacking the curiosity-first quality.

## PD-002: Some Windows Open on Load, Others as Icons
**Date:** May 14, 2026
**Decision:** About and Work windows are open and staggered on load. Movement, Homestead, Bus, Writing Space, and Easter eggs are desktop icons.
**Why:** Fully closed desktop (all icons) requires too much participation before delivering value — visitor might bounce before clicking anything. Fully open desktop overwhelms and removes the discovery reward. The hybrid gives narrative control over first impression (professional + personal intro) while rewarding exploration for the rest.

## PD-003: Win95 Felt, Not Replicated
**Date:** May 14, 2026
**Decision:** The site uses Win95 structural language (window chrome, title bars, bevels, taskbar) with a warmer palette and non-pixel typography. It's "inspired by" not "cosplay."
**Why:** Pixel-perfect Win95 emulation becomes costume — the aesthetic overwhelms the content. The structural system (windows, taskbar, start menu, drag/minimize/close) is the valuable part. Warm palette (aged paper, Peninsula tones) makes it feel lived-in rather than ironic.

## PD-004: Family Is Substrate, Not Section
**Date:** May 14, 2026
**Decision:** No dedicated "Family" section. Family surfaces naturally through the Homestead window (nobody homesteads alone) and the Bus window (a family adventure). 
**Why:** A "Family" page on a professional-adjacent site risks feeling performative (Christmas card energy). Letting family be woven through context is both more honest and more interesting.

## PD-005: Writing Space Has No Category Name
**Date:** May 14, 2026
**Decision:** The writing/notes section avoids definitive naming ("blog," "essays," "journal"). Working title is something neutral — "Notes," "Shelf," "Desk," or even just a symbol.
**Why:** Every label pre-loads expectations. "Blog" implies cadence. "Essays" implies polish. "Journal" implies intimacy. The space is intentionally uncategorized to reduce the psychological barrier to putting things there. Content is arranged spatially, not temporally — no "latest post" energy.

## PD-006: No Contact Form
**Date:** May 14, 2026
**Decision:** No contact form on the site. Professional contact goes through LinkedIn or retencity.com.
**Why:** The site is an environment to explore, not a funnel. Contact forms create conversion pressure that contradicts the "pull up a chair" vibe.

## PD-007: Mobile Gets a Different Experience
**Date:** May 14, 2026
**Decision:** Desktop gets the full desktop metaphor. Mobile gets an adapted layout (vertical card stack preserving window aesthetic) that doesn't simulate a desktop on 375px.
**Why:** Draggable, stackable windows are a desktop interaction model. Forcing them onto mobile creates frustration, not delight. The spirit (windows as containers, warm chrome, discoverable content) translates; the mechanics (drag, stack, minimize) don't.

## PD-008: Podcast and DojoFlow Out of Scope for v1
**Date:** May 14, 2026
**Decision:** In Process podcast and DojoFlow/Banyan Stand are not included in v1. The desktop metaphor makes future addition trivial (new icon or work card).
**Why:** Neither is ready to show. Show the meal, not the ingredients. When they're ready, adding them is as simple as a new desktop icon.

## PD-009: Full Window Interactivity
**Date:** May 14, 2026
**Decision:** Windows are fully interactive: draggable, minimizable to taskbar, closable with recovery, z-index managed. Start menu is explorable. Easter eggs throughout. Sound effects.
**Why:** "Distraction is the point. Oooo what's this?" The site rewards curiosity and play. Half-committing to the metaphor (windows that look like windows but don't act like windows) would feel broken, not charming.

## PD-010: Static Site, No Framework
**Date:** May 14, 2026
**Decision:** Single HTML file with CSS and vanilla JS. No React, no build step, no dependencies beyond Google Fonts.
**Why:** The site has no dynamic data, no auth, no API. A framework adds complexity without value. A single file deploys anywhere, loads fast, and has zero maintenance overhead. The interactivity (window management, sound) is complex but self-contained — vanilla JS handles it cleanly.

## PD-011: SEO/GEO Infrastructure Beyond BRIEF.md Scope
**Date:** May 15, 2026
**Decision:** Added llms.txt, JSON-LD Person, Open Graph, Twitter card, canonical, sitemap, and robots.txt, going beyond the "basic meta tags" originally scoped as the SEO ceiling in BRIEF.md.
**Why:** Discoverability matters even for an environment-first personal site. Recruiters, founders, and curious operators reach Andrew through Google, LinkedIn previews, and increasingly through LLM search (ChatGPT, Perplexity, Claude). Without structured data and llms.txt the site renders as a Win95 curiosity that LLMs struggle to summarize accurately. With them, the same site doubles as a machine-legible identity index. No visible UI cost.
**Alternatives considered:** Sticking strictly to BRIEF.md's "basic meta tags" rule. Rejected because the cost of the additional tags is zero (head-only) and the upside is non-trivial as LLM-mediated discovery grows. BRIEF.md updated implicitly via this PD.

## PD-012: One Canonical Source Per Identity Fact
**Date:** May 15, 2026
**Decision:** Andrew's name, role, location, product list, and external links exist on seven surfaces (meta description, OG, Twitter, JSON-LD, sitemap, llms.txt, humans.txt). Each fact has one canonical phrasing; the surfaces echo it. The README for future edits: change a fact in one place mentally, then sweep the seven.
**Why:** DRY applies to content as much as code. When a job title changes or a new product ships, the update should be mechanical, not a treasure hunt. Without this discipline these surfaces drift, and drift makes structured data worse than no structured data (an LLM citing a stale job title is worse than no citation).
**Alternatives considered:** A build step that generates the metadata surfaces from a single YAML source. Rejected for v1: violates PD-010 (no build step) and the seven surfaces are small enough to maintain by hand. Reconsider if drift actually shows up.
