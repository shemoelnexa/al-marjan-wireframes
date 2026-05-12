# Marjan brand & design language application — design spec

**Date:** 2026-05-12
**Scope target:** 28 HTML files + `styles/wireframe.css`
**Approach approved:** C (Full visual rebuild) + extrapolate Marjan voice for new sections
**Source of truth:** `https://marjan.ae/` (homepage, /about-us, /development/our-approach, /hospitality-portfolio, /sustainability, /our-business/hospitality/wynn-al-marjan-island) — audited 2026-05-12 from rendered HTML and compiled CSS bundles (`template_main.min.css`, `template_theme-overrides.min.css`).

---

## 1. Brand foundations (locked from marjan.ae)

### 1.1 Identity
- **Wordmark:** "Marjan" (no "Al" prefix). Set in display face, slight tracking, no symbol.
- **Descriptor:** *Master Developer of Ras Al Khaimah*.
- **Voice anchor:** *Designed for Life, Defining the Future of Ras Al Khaimah*.
- **Legal entity in footer:** Marjan LLC.

### 1.2 Color tokens (replace current cream/bronze palette wholesale)

| Token | Hex | Source on marjan.ae | Usage |
|---|---|---|---|
| `--ink` | `#00002E` | Dominant brand color (47 CSS occurrences) | Primary text, headers, buttons, footer |
| `--ink-deep` | `#000006` | Deep accent | Footer ground, hero overlay base |
| `--navy` | `#282856` | Secondary brand | Section dividers, hover states |
| `--navy-soft` | `#3B5173` | Tertiary | Subtle backgrounds, dark-section accents |
| `--mist` | `#13294B` | Cool deep | Gradient stops in image placeholders |
| `--paper` | `#FFFFFF` | Body bg | Default background |
| `--surface` | `#F9F9F9` | Section alt | Alternating section background |
| `--surface-2` | `#F5F5F5` | Stat strip | Stat / utility band background |
| `--line` | `#E5E7EB` | Borders | Dividers, card borders |
| `--line-soft` | `#D7D7D7` | Soft borders | Form fields, table rows |
| `--muted` | `#999999` | Secondary text | Captions, eyebrows on light bg |

**No separate accent token.** Marjan uses `--ink` (#00002E) as both primary text *and* CTA fill — there is no contrasting brand accent in their system. We follow suit.

**Deliberately removed:** every `--cream*`, `--sand`, `--bronze*` token. Marjan's palette is cool/navy-led; the existing warm coastal palette is editorial fiction we picked, not their brand. **The current Hard Rock reference page will be re-skinned under this palette and is no longer the visual reference.**

### 1.3 Typography

```css
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:ital,wght@0,300;0,400;0,500;0,600;0,700;1,400&family=Montserrat:wght@300;400;500;600;700&display=swap');

--font-display: 'Montserrat', -apple-system, BlinkMacSystemFont, "Helvetica Neue", sans-serif;
--font-sans:    'IBM Plex Sans', -apple-system, BlinkMacSystemFont, "Helvetica Neue", sans-serif;
```

- **Body:** IBM Plex Sans 400, 16px, 1.65 line-height. Confirmed from `template_main.min.css`.
- **Display (H1, H2, large stats):** Montserrat. Weights 500/600. Tighter letter-spacing (-0.02em on H1).
- **Italics:** rare on marjan.ae. Remove all `<em>` italic-as-accent treatments from current wireframes.
- **No serif at all.** Fraunces is fully removed.
- **All-caps eyebrows:** IBM Plex Sans 600, 11px, letter-spacing 0.18em — unchanged pattern, recolored to `--ink` or `--muted`.

### 1.4 Imagery treatment
Keep CSS-gradient image placeholders (wireframe convention — no asset wrangling), but restyle gradients to Marjan's cool/cinematic mood:
- Replace `--img--sea/dawn/sand/cream/bronze/night` warm gradients with cool navy-led gradients overlaying golden-hour drone-style warmth at horizon.
- Add a consistent dark vignette `linear-gradient(180deg, transparent 40%, rgba(0,0,6,0.55) 100%)` so hero text remains legible.
- Hero images: full-bleed, `min-height: 80vh`, headline centered with eyebrow above, single CTA below.

---

## 2. Voice & copy rewrite rules

### 2.1 Headline formula
Every page H1 follows one of these patterns from marjan.ae:
- *Gerund + future-state*: "Building a World-Class Hospitality Ecosystem"
- *Verb + benchmark*: "Setting a New Benchmark for Destination Development"
- *Designed/Shaping + outcome*: "Shaping the Future of Ras Al Khaimah"

### 2.2 Vocabulary register (use these, drop the wireframe filler)
- Use: *master developer · masterplanned · world-class · future-ready · transformative · long-term value · connectivity · liveability · placemaking · benchmark · RAK Vision 2030 · destination · catalyst · stewardship.*
- Drop: *editorial · luxury bar · framework · architecture (as metaphor) · narrative.* All wireframe meta-language.
- Numbers: spell the unit alongside the figure (e.g. *"US$5.1 billion total investment"*, *"145,000 sq ft meetings centre"*, *"2,300+ projected new jobs"*). Match Wynn page convention.

### 2.3 Section pattern
Every content section uses Marjan's three-beat pattern:
1. **Eyebrow** (uppercase, 11px, letter-spacing 0.18em).
2. **Sectional H2** (Montserrat 500, 40–56px, tight tracking).
3. **Opening paragraph** (IBM Plex Sans 400, 17px, 2 measured sentences, no rhetorical flourish).

Then sub-blocks within the section repeat bold subtitle + body paragraph (also matches their Our Approach page).

### 2.4 Per-page voice — what each Phase 2 page must say
For sections that exist on marjan.ae, port real copy (lightly adapted to wireframe needs).
For new Phase 2 sections (Investment / Careers / Resources / Legal), extrapolate.

| File | H1 (proposed) | Eyebrow | Source approach |
|---|---|---|---|
| `index.html` (Phase 2 navigator) | *Phase 2 — Extending the Marjan Story* | SITEMAP NAVIGATOR | Reframe sitemap-navigator language in brand voice |
| `pages/development/future-developments.html` | *Building What Comes Next for Ras Al Khaimah* | DEVELOPMENT PIPELINE | Adapt from /development/our-approach |
| `pages/hospitality/hard-rock.html` | *Hard Rock Hotel Al Marjan Island* + subhead in Wynn voice | HOSPITALITY · UNDER DEVELOPMENT | Mirror Wynn page structure exactly |
| `pages/hospitality/branded-residences.html` | *Branded Residences for a New Era of Coastal Living* | HOSPITALITY · RESIDENCES | Adapt from /hospitality-portfolio |
| `pages/hospitality/for-operators.html` | *A Partner-Led Platform for World-Class Operators* | HOSPITALITY · FOR OPERATORS | Extrapolate |
| `pages/hospitality/market-insights.html` | *Reading Ras Al Khaimah's Hospitality Growth Story* | HOSPITALITY · MARKET INSIGHTS | Extrapolate |
| `pages/investment/overview.html` | *Investing in Ras Al Khaimah's Defining Decade* | INVESTMENT · OVERVIEW | Extrapolate from /ras-al-khaimah/why-invest tone |
| `pages/investment/by-sector.html` | *Capital Strategies Across Marjan's Sectors* | INVESTMENT · BY SECTOR | Extrapolate |
| `pages/investment/residential.html` | *Long-Term Value in Coastal Residential* | INVESTMENT · RESIDENTIAL | Extrapolate |
| `pages/investment/hospitality.html` | *Hospitality Investment in a Globally Ascendant Destination* | INVESTMENT · HOSPITALITY | Extrapolate |
| `pages/investment/commercial.html` | *Commercial Real Estate at RAK's Inflection Point* | INVESTMENT · COMMERCIAL | Extrapolate |
| `pages/investment/staff-accommodation.html` | *Purpose-Built Workforce Housing at Scale* | INVESTMENT · STAFF ACCOMMODATION | Extrapolate |
| `pages/investment/process.html` | *A Clear, Disciplined Path from Inquiry to Handover* | INVESTMENT · PROCESS | Extrapolate, mirror Our Approach numbered steps |
| `pages/news-media/latest-news.html` | *Marjan in the News* | NEWS & MEDIA · LATEST | Adapt from /press-releases |
| `pages/news-media/media-centre.html` | *A Working Resource for the Press* | NEWS & MEDIA · MEDIA CENTRE | Extrapolate |
| `pages/news-media/publications.html` | *Reports, Reviews, Briefings* | NEWS & MEDIA · PUBLICATIONS | Extrapolate |
| `pages/news-media/in-the-media.html` | *Marjan, As Seen Elsewhere* | NEWS & MEDIA · IN THE MEDIA | Extrapolate |
| `pages/careers/working-at-marjan.html` | *Working at Marjan — Building the Emirate's Next Chapter* | CAREERS · WORKING AT MARJAN | Extrapolate |
| `pages/careers/current-openings.html` | *Current Openings* | CAREERS · OPENINGS | Extrapolate |
| `pages/careers/life-at-marjan.html` | *Life at Marjan* | CAREERS · LIFE AT MARJAN | Adapt from /life-at-marjan |
| `pages/resources/downloads.html` | *Documents, Brochures, Specifications* | RESOURCES · DOWNLOADS | Extrapolate |
| `pages/resources/faqs.html` | *Frequently Asked* | RESOURCES · FAQS | Extrapolate |
| `pages/resources/glossary.html` | *Glossary of Terms* | RESOURCES · GLOSSARY | Extrapolate, formal register |
| `pages/resources/investment-calculator.html` | *Modelling Your Investment* | RESOURCES · CALCULATOR | Extrapolate |
| `pages/legal/legal-notices.html` | *Legal Notices* | LEGAL · NOTICES | Formal register, mirror UAE corporate norms |
| `pages/legal/regulatory.html` | *Regulatory Information* | LEGAL · REGULATORY | Formal |
| `pages/legal/anti-corruption.html` | *Anti-Corruption Policy* | LEGAL · POLICY | Formal |
| `pages/legal/data-protection.html` | *Data Protection* | LEGAL · POLICY | Formal |

### 2.5 Navigation (locked)
Top nav stays as the 7 Phase 2 sections (per locked memory). Footer keeps the 5-column structure but relabels via the new voice. No change to URL structure.

---

## 3. Component / pattern rebuild

The current `wireframe.css` will be rewritten section-by-section to mirror marjan.ae's module library. The patterns below replace the existing equivalents.

### 3.1 Header
- Sticky, white 85% + blur (keep current behavior).
- Logo: word "MARJAN" in Montserrat 600, 18px, letter-spacing 0.12em, color `--ink`.
- Nav links: IBM Plex 500, 12.5px, letter-spacing 0.06em, *sentence case* (marjan.ae uses uppercase — we keep uppercase to match: `text-transform: uppercase`).
- CTA button on right: solid `--ink` background, white text, no rounding.

### 3.2 Hero (replaces `.wf-hero` and `.wf-index-hero-v2`)
- Full-bleed dark photo placeholder, min-height 80vh.
- Eyebrow + H1 centered or left-aligned (left for content pages, centered for landing).
- H1: Montserrat 500, clamp(48px, 7vw, 88px), tracking -0.02em, color white.
- Subhead: IBM Plex 400, 18–20px, max-width 720px, color rgba(255,255,255,0.85).
- One primary CTA (solid white-on-ink or ink-on-white depending on overlay).

### 3.3 Editorial block (replaces `.wf-block`)
- Eyebrow `--ink` uppercase 11px.
- H2 Montserrat 500, clamp(36px, 4vw, 56px), `--ink`, no italic accent.
- Paragraph 17px IBM Plex, max-width 680px, `--ink` at 80% opacity for body weight feeling.
- Sub-blocks (used heavily on Our Approach page): bold IBM Plex 600 18px title + IBM Plex 400 16px paragraph. Vertical rhythm 28px between sub-blocks.

### 3.4 Stats strip (replaces `.wf-stats-strip` and `.wf-stat`)
- Dark band background `--ink-deep`.
- Numerals Montserrat 500, clamp(48px, 5vw, 72px), white, letter-spacing -0.03em.
- Label below: IBM Plex 500 12px, white at 60%, letter-spacing 0.14em, uppercase.
- Use Marjan's stat phrasing (unit + descriptor): *"120M / Sq ft of masterplanned land"* rather than just *"120M / land"*.

### 3.5 Portfolio grid (replaces `.wf-card` for Hospitality, Hard Rock, By-Sector)
- 3-up grid, full-width tile per card, taller aspect (3:4 image).
- Tile overlay: bottom-aligned eyebrow + property name + status pill.
- Hover: no transform; subtle overlay darkening only.
- Status pill: small uppercase chip ("Now Open" / "Under Development" / "Coming 2027") in white border, white text, transparent fill — matches Wynn page tag style.

### 3.6 Process / numbered steps (Investment Process, Our Approach analog)
- Vertical layout (`.wf-process-v` style we already have, but restyled).
- Step number: Montserrat 500, 64px, color `--navy`, letter-spacing -0.04em.
- Step title: Montserrat 500, 24px, `--ink`.
- Step body: 16px IBM Plex, max-width 640px.
- Rule between steps: 1px `--line`.

### 3.7 CTA / Inquiry band
- Full-bleed `--ink-deep` background.
- Display headline white, body white at 80%, two CTAs (primary white-on-ink + ghost outline white).
- Pattern mirrors marjan.ae's footer-precede inquiry band.

### 3.8 Footer
- Full `--ink-deep` background, all text on white-tinted ranges.
- Brand block left (wordmark + descriptor + tagline), 4 link columns right.
- Newsletter subscribe row above footer-bottom — single field + button, IBM Plex.
- Footer-bottom: copyright, social icon row (FB / X / IG / LinkedIn), legal links.

### 3.9 Specialist patterns (preserve, restyle)
The Phase 2 wireframe already has good specialist components — keep their structure, restyle to new palette/type:
- `.wf-accordion` (FAQs) — IBM Plex titles, `--ink` color, `+` indicator in `--navy`.
- `.wf-glossary` (Glossary) — letter blocks use Montserrat 80px in `--ink`.
- `.wf-az-nav` — restyle to `--ink` accents.
- `.wf-doc` + `.wf-toc` (Legal pages) — restyle to ink/navy, no bronze.
- `.wf-feature`, `.wf-news-row` (News) — restyle to new palette.
- `.wf-tool` (Calculator) — restyle, replace cream with `--surface`.
- `.wf-files` (Downloads) — restyle.
- `.wf-jobs` (Careers) — restyle.
- `.wf-essay` (Life at Marjan) — restyle.
- `.wf-process` / `.wf-process-v` — see 3.6.

---

## 4. Implementation order

Group the 28 files into 4 implementation phases so the user can review at each phase boundary:

1. **Foundation** — rewrite `styles/wireframe.css` end-to-end (tokens, typography, components). Verify against `index.html` first.
2. **Anchor pages** — `index.html`, `pages/hospitality/hard-rock.html` (the named reference), `pages/development/future-developments.html`. These set the voice + visual bar.
3. **Bulk content rewrite** — all Hospitality, Investment, News & Media, Careers pages.
4. **Utility & legal** — Resources (Downloads, FAQs, Glossary, Calculator), Legal (all 4 docs).

After each phase, a checkpoint: open the page in the live-server URL, eyeball, fix, move on.

---

## 5. Out of scope (explicit)

- No new pages, no IA changes beyond what the current sitemap holds.
- No real photography assets — gradient placeholders only.
- No JavaScript additions beyond existing details/accordion native behavior.
- No responsive breakpoint changes unless a component visibly breaks under the new type scale.
- No translation / Arabic locale support.
- The PDF sitemap, README files, git workflow — untouched.

---

## 6. Definition of done

- Every one of the 28 HTML files renders under the new palette and type system without leftover cream/bronze/Fraunces visual artifacts.
- Every page's H1 + opening section follow the gerund-led / benchmark-led voice with no wireframe-meta copy left ("polished mid-fidelity", "low-fi structural only" etc.).
- Footer descriptor and tagline match marjan.ae phrasing.
- Live-server preview at `http://localhost:5500/` cycles through all 28 pages with no console errors and visually consistent voice/visuals.
- Single git commit per implementation phase (4 commits total).
