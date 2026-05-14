# Web Typography

## Core Idea

Typography is not decoration. It is the primary medium through which a web interface communicates. *Practical Typography* by Matthew Butterick argues that most web typography is mediocre by default — not because designers are careless, but because browser defaults and framework defaults are tuned for neutrality, not readability or hierarchy.

Good typography makes reading effortless and hierarchy legible at a glance. Bad typography creates cognitive friction the reader doesn't consciously notice — they just find the interface harder to use.

In a B2B admin panel like DojoFlow, where senseis scan dashboards under time pressure and parents read messages on phones, typography is a functional requirement, not an aesthetic one.

---

## Type Hierarchy

Hierarchy tells the reader where to look first, second, and third. Without hierarchy, everything is equally important — which means nothing is important.

**The three levels every interface needs:**
1. **Primary** — the one thing the user should notice first (student name on a StudentDetail page, KPI number on the dashboard)
2. **Secondary** — contextual information that supports the primary (belt rank, attendance percentage, family name)
3. **Tertiary** — metadata the user only needs if they're looking for it (enrollment date, last updated timestamp)

**Establishing hierarchy with Tailwind:**
```
Primary:    text-xl font-semibold text-gray-900
Secondary:  text-sm font-medium text-gray-700
Tertiary:   text-xs text-gray-500
```

**The hierarchy test:** squint at the page. Without reading, can you tell what the most important information is? If everything looks equally bold or equally light, hierarchy has failed.

---

## Line Length

Line length (measure) determines how comfortable a block of text is to read. Too short and the eye jumps lines constantly; too long and the eye loses its place returning to the left margin.

**The rule:** 45–75 characters per line for body text. 65–70 is the sweet spot.

**In Tailwind:** `max-w-prose` sets `max-width: 65ch` — the correct default for reading columns. Apply it to any block of paragraph text.

**Applied to DojoFlow:**
- Email compose body: constrain to `max-w-prose` so the sensei can read their drafted message at a comfortable measure
- Dashboard descriptions and empty states: don't let text span the full container width; constrain it
- Student notes and communication log entries: `max-w-prose` in the detail view

---

## Line Spacing (Leading)

Line spacing (leading) affects the density and readability of text. Too tight and lines visually bleed together; too loose and the text loses cohesion.

**The rule:** body text line height should be 1.4–1.6× the font size. Display text and headings can be tighter (1.1–1.3×).

**In Tailwind:**
- `leading-normal` (1.5) is correct for most body text
- `leading-tight` (1.25) works for headings
- `leading-relaxed` (1.625) is good for mobile body text where readability is more strained

**Applied to DojoFlow:**
- Student list rows: `leading-tight` — the user is scanning, not reading
- Communication previews in the log: `leading-normal` — the user reads these
- Dashboard KPI tiles: `leading-none` for the number, `leading-tight` for the label

---

## Font Pairing

A typeface choice is a tone choice. In a B2B admin panel, the goals are:
- **Legibility** at small sizes and on screens of varying quality
- **Authority** — the interface should feel professional and trustworthy
- **Neutrality** — the UI should not compete with content; the student's data should be the focus

**Principles for pairing:**
- Don't use more than two typefaces in an interface
- Pair a geometric sans-serif for display/headings with a humanist sans-serif for body, or use one family with multiple weights
- Never pair two serif fonts or two fonts from the same family

**For DojoFlow (Tailwind/shadcn context):**
- The default shadcn/ui stack uses the system font stack (`font-sans`) — acceptable and performant
- If custom fonts are added: Inter (body) + any geometric sans for display is a reliable pairing; Inter alone with weight variation is also correct
- Avoid decorative fonts — they signal "consumer app" in a B2B context that requires professional credibility

---

## Typographic Color

Typographic color is the visual density of a text block — how dark or light it appears relative to the page. It is affected by font weight, letter spacing, line spacing, and font size collectively.

**The goal:** match typographic color to the reading context.

- Dense, heavy text signals "read this carefully" — appropriate for legal terms, destructive action confirmations
- Light, open text signals "scan this" — appropriate for dashboard labels, list metadata
- Consistent color across similar elements tells the reader these things are the same kind of thing

**Common mistakes:**
- All-caps labels with tight tracking read darker than intended — adjust weight down if using all-caps
- Bold used so frequently it loses meaning — reserve `font-semibold` and `font-bold` for genuine emphasis
- Gray text too light for accessibility — `text-gray-400` on white fails WCAG AA for body text; use `text-gray-500` minimum for secondary text, `text-gray-600` for anything that needs to be read

**Accessibility rule of thumb:**
- Primary text: `text-gray-900` (contrast ratio ~17:1 on white)
- Secondary text: `text-gray-600` (contrast ratio ~7:1)
- Tertiary/disabled: `text-gray-400` only for decorative or truly non-essential text; never for anything that conveys information

---

## Punctuation and Detail

Butterick's most distinctive contribution: the details of punctuation and spacing matter more than most designers realize.

**Key rules for web interfaces:**
- **One space after a period.** Two spaces are a typewriter habit. Remove them.
- **Curly quotes, not straight quotes.** React renders straight quotes by default; use `&ldquo;`, `&rdquo;`, `&lsquo;`, `&rsquo;` or configure Prettier to handle them.
- **Em dashes (—) not double hyphens (--)** for mid-sentence breaks. `&mdash;` in HTML.
- **Ellipses (…) not three periods (...)** in UI text. The three-period version has uneven spacing.
- **Never underline text that isn't a link.** Underlines mean links on the web; using them for emphasis confuses users.

---

## How to Apply This in Tailwind/React

**Establish a type scale and stick to it.** Shadcn/ui provides a sensible default; don't add arbitrary `text-[13px]` values. Use the defined scale.

**Create consistent text style components** for the patterns you use repeatedly:
```tsx
// Reusable: don't repeat Tailwind strings across 20 components
const PageTitle = ({ children }) => (
  <h1 className="text-2xl font-semibold text-gray-900 leading-tight">{children}</h1>
)
const FieldLabel = ({ children }) => (
  <label className="text-sm font-medium text-gray-700">{children}</label>
)
const MetaText = ({ children }) => (
  <span className="text-xs text-gray-500">{children}</span>
)
```

**Review every new page with the squint test:** squint until the text blurs. Does hierarchy emerge naturally? Or does everything look the same weight?

---

## Common Failure Modes

- **Hierarchy by size alone** — using only font size to distinguish levels; weight and color are equally important levers
- **Too much bold** — when everything is emphasised, nothing is; reserve bold for genuine priority
- **Inaccessible gray** — secondary text that's too light to read in bright environments or on low-contrast screens
- **Full-width text blocks** — paragraph text that spans the entire container; always constrain reading columns
- **Ignoring line spacing** — using default line height for all text regardless of context; compact lists and readable paragraphs have different needs
- **Inconsistent scale** — ad-hoc font sizes for one-off cases; adds visual noise and undermines hierarchy

---

## Applied to DojoFlow

Priority typography work before public launch:

1. **Audit hierarchy on key pages** — Dashboard, Students list, StudentDetail: can a first-time user identify the most important information without reading every element?
2. **Constrain text blocks** — communications log entries, message compose body, empty state descriptions: apply `max-w-prose`
3. **Accessible secondary text** — audit all `text-gray-400` usage; replace with `text-gray-500` minimum for any text that conveys information
4. **Consistent label style** — all form labels, column headers, and card labels should use the same weight and color; derive a `FieldLabel` component if they're currently inconsistent
5. **Communication tone via typography** — Magic Text messages sent to parents should display in a comfortable reading measure with `leading-relaxed`; it's a letter, not a table row
