---
name: market-research
description: 'Research competitors, analyse GTM strategies, and document opportunities in the dojo management software market. Use before committing to any new feature, pricing strategy, or go-to-market decision. Produces structured artifacts in docs/research/.'
license: MIT
metadata:
  author: dojo-admin
  version: "1.0.0"
---

# Market Research — Dojo Admin

A structured framework for researching the dojo/martial arts studio management software market before building features or choosing GTM strategies. Produces a documented artifact that feeds into the feature planning process.

## Core Principle

**Every opportunity should be compared against what customers already use, what they hate about it, and how they'd switch.** The goal is not to build a "better" version of existing software — it's to identify where the current solutions fail dojo owners and build something that genuinely fits their job-to-be-done.

## Scoring

**Goal: 10/10.** When producing a market research artifact, rate it 0-10. A 10/10 includes: identified competitors with honest pros/cons, at least 2 GTM strategy options with tradeoffs, an opportunity gap statement, and a recommendation grounded in evidence.

---

## 1. Competitor Landscape

### Known Competitors

| Product | Focus | Pricing | Strengths | Weaknesses |
|---------|-------|---------|-----------|------------|
| **Jackrabbit Martial Arts** | Martial arts studios | $45–$130/mo | Deep martial arts features, belt tracking | Dated UI, steep learning curve, complex pricing |
| **Pike13** | Gyms & studios | $129+/mo | Clean UX, great scheduling | Weak martial arts specifics, expensive for small dojos |
| **Zen Planner** | Martial arts & fitness | $99–$348/mo | Strong community, good integrations | Slow, reports are confusing, support issues |
| **Mindbody** | Fitness/wellness | $79–$599/mo | Market leader, consumer-facing app | Enterprise-focused, overkill for small dojos, very expensive |
| **WellnessLiving** | Fitness studios | $89+/mo | Feature-rich, good value | Complex, not martial-arts specific |
| **iClassPro** | Gymnastics/dance/martial arts | $75+/mo | Strong for families, payment features | Old design, limited mobile experience |
| **Kicksite** | Martial arts only | $49–$149/mo | Purpose-built for martial arts, simple pricing | Limited integrations, basic reporting |
| **Glofox** | Boutique fitness | $110+/mo | Beautiful consumer app, modern stack | Not martial arts specific, focused on fitness |

### Positioning Map

```
                    HIGH PRICE
                        |
     Mindbody •    Zen Planner •
                        |
    Pike13 •            |
LOW SPECIFICITY --------+-------- HIGH MARTIAL ARTS SPECIFICITY
                        |
    WellnessLiving •    |          Kicksite •
                        |   Jackrabbit •
                   LOW PRICE
```

---

## 2. Research Framework

When running `/market-research` for a specific topic, follow this structure:

### Step 1: Define the Question
- What decision are we making? (feature, pricing, GTM strategy, positioning)
- What would change our mind about building this?

### Step 2: Competitive Analysis
For each relevant competitor:
- Does their product solve this need? How?
- What do customers complain about? (Check G2, Capterra, Reddit r/martialarts, Facebook groups)
- What's their pricing model for this capability?
- What would make a customer switch away from them for this?

### Step 3: GTM Strategy Options
Generate at least 2 distinct go-to-market strategies with honest trade-offs:

| Strategy | Description | Pros | Cons | Best if... |
|----------|-------------|------|------|------------|
| Direct SEO | Rank for "dojo management software" | Low CAC, compounding | Slow (6–18 months) | You have time |
| Partner channel | Integrate with martial arts associations | High trust, warm leads | Slow, relationship-dependent | You know instructors |
| Bottom-up PLG | Free tier, upgrade when dojo grows | Viral word-of-mouth | Low revenue density early | Product is very sticky |
| Paid acquisition | Facebook/Instagram to dojo owners | Fast to test, measurable | High CAC, requires good conversion | You have budget |
| Community-led | Sponsor tournaments, create resources | Builds brand loyalty | Not predictable | Long-term brand play |

### Step 4: Opportunity Gap Statement

Write one clear statement:
> "Dojo owners who use [competitor] are frustrated by [pain] when they try to [job-to-be-done]. No current solution handles [specific gap]. We can win by [unique approach]."

### Step 5: Recommendation

One clear recommendation with reasoning. Include what we'd need to see to know we're right.

---

## 3. Output Format

Every `/market-research` run produces a file in `docs/research/<topic>.md` with this structure:

```markdown
# Market Research: <Topic>

**Date:** YYYY-MM-DD
**Question:** What decision are we making?
**Inputs:** Customer interviews, competitor reviews, industry data

## Competitor Analysis
[Table with competitors relevant to this specific question]

## Customer Pain Evidence
[Quotes from interviews, reviews, forums — verbatim, not paraphrased]

## GTM Strategy Options

### Option 1: <Name>
**Description:**
**Pros:**
**Cons:**
**Best for:**

### Option 2: <Name>
...

## Opportunity Gap
[One clear statement]

## Recommendation
[Decision + reasoning + what we'd need to be wrong]

## Open Questions
[What we still don't know]
```

---

## 4. Sources

When researching, check:
- **G2** and **Capterra** for competitor reviews (filter for 1–3 stars to find real pain)
- **Reddit:** r/martialarts, r/smallbusiness, r/gymowners
- **Facebook Groups:** "Martial Arts School Owners", "Dojo Business Network"
- **App Store / Play Store** reviews for mobile apps
- Competitor blog posts (what problems they claim to solve = what customers ask about)
- Pricing pages (features listed = what people pay for)

---

## 5. Red Flags in Research

- Confirmation bias — only citing evidence that supports the idea
- Asking customers "would you use this?" instead of "tell me about the last time you had this problem"
- Using competitor feature lists as a product roadmap
- Treating one loud customer as representative of all customers
- Conflating what people say they'll pay with what they actually pay
