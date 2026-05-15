# Changelog: andrewchristison.com

All notable changes to this project, newest first.
Format: What it does. Why it matters.

---

## 2026-05-15

- **First commit of the actual site.** The full Win95-inspired desktop (about 98 KB of index.html), favicon.svg, assets/og-image.png, .gitignore, and assets/photos/ all enter version control. Prior commits were scaffold and skills only; the site itself lived only on disk.

- **Shipped SEO/GEO infrastructure.** Added robots.txt, sitemap.xml, llms.txt, humans.txt, canonical link, Open Graph block, Twitter card block, and JSON-LD Person schema in index.html head. The site is now legible to traditional crawlers (Google, Bing) and to LLM crawlers (llms.txt, schema.org Person), without changing any visible UI or window behavior.

- **Replaced data-URI favicon with external favicon.svg.** Mushroom mark now ships as a real file at the root, picked up by browsers and feed readers that don't parse data URIs. The Win95 four-pane data-URI that previously lived inline in index.html is gone.

- **Locked a single canonical source for identity facts.** Andrew's name, role, location, products, and external links express the same values across robots.txt, sitemap.xml, llms.txt, humans.txt, meta description, OG, Twitter, and JSON-LD. DRY for content. Future updates touch one place per fact, not seven.

## 2026-05-14

- **Project scaffold created.** CLAUDE.md, BRIEF.md, STICKIES.md, and supporting docs initialized. 56 skills synced from gundry-agents and pruned. Foundation set for build sessions.

- **Creative brief finalized.** Desktop metaphor, content architecture, design direction, window behavior, Easter eggs, and mobile approach locked in BRIEF.md. Every build decision traces back to it.
