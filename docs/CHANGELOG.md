# Changelog — Ask K

All notable changes to this project, newest first.
Format: What it does. Why it matters.

---

## 2026-04-06

- **Project initialized.** PRD v2.2 approved, CLAUDE.md created, stickies defined, competitive analysis completed. Foundation for Ask K is set — ready for repo creation and first code.

- **Named the product "Ask K" at retencity.ai/ask-k.** Memorable, two syllables, no trademark risk, works as both URL path and brand ("Just Ask K").

- **Confirmed Zendesk Help Center API as primary ingestion method.** Anonymous GET requests to list articles have zero rate limit impact. Hourly incremental polling is viable for catching new feature announcements same-day.

- **Confirmed developers.klaviyo.com runs on ReadMe.io, not Zendesk.** Requires separate crawl strategy (Firecrawl or sitemap-based). Secondary ingestion target.

- **Completed competitive analysis.** No direct competitor exists in this space. Klaviyo's own AI (K:AI) serves end consumers, not Klaviyo users. Gap is real and defensible with tiered knowledge architecture.

- **Defined three-tier knowledge architecture.** Tier 1: automated doc index. Tier 2: curated expert knowledge. Tier 3: embedded practitioner judgment via system prompt. This is the moat.
