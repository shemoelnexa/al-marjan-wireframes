# Marjan Brand & Design Language Application — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Apply marjan.ae's actual brand (palette, typography, voice, section modules) to all 28 Phase 2 wireframe pages, replacing the existing cream/bronze editorial language end-to-end.

**Architecture:** Single shared stylesheet (`styles/wireframe.css`) rewritten under new tokens, with every HTML page reauthored to the new component patterns and Marjan voice. No JavaScript additions. Gradient placeholders kept (no real photo assets). Implementation runs in 4 phases (Foundation → Anchor → Bulk → Utility) with a commit at each phase boundary.

**Tech Stack:** Static HTML5 + hand-written CSS3 (custom properties, grid, flex). Google Fonts (Montserrat + IBM Plex Sans). Live-server for preview.

**Spec:** `docs/superpowers/specs/2026-05-12-marjan-brand-application-design.md` — authoritative source for all tokens, voice rules, per-page H1 table, and component patterns.

**Verification model:** Wireframes have no automated tests. Each task is verified by opening the affected page(s) in `http://localhost:5500/`, visually checking under the new design system, and confirming no console errors. Run live-server before starting work:

```bash
cd "/mnt/d/Code Files/al-marjan"
npx --yes live-server --port=5500 --host=0.0.0.0 --no-browser --watch=. --ignore="node_modules,.claude,docs"
```

**Path note:** All file paths in this plan are relative to `/mnt/d/Code Files/al-marjan/`.

---

## File Structure

**Rewritten (one wholesale rewrite):**
- `styles/wireframe.css` — full rewrite. Single file shared by all pages. Sections: (1) Reset & tokens, (2) Base typography, (3) Layout shell, (4) Header & footer, (5) Hero, (6) Editorial blocks, (7) Stats, (8) Cards & portfolio grid, (9) CTAs, (10) Forms & fields, (11) Specialist patterns (accordion, glossary, A–Z nav, calculator, files, jobs, essay, doc/TOC, news, feature, toolbar, chips, tabs, dark section, related strip, image placeholders), (12) Index page (sitemap navigator), (13) Responsive.

**Rewritten (one per page, 28 total):**
- `index.html` — sitemap navigator landing
- `pages/development/future-developments.html`
- `pages/hospitality/{hard-rock,branded-residences,for-operators,market-insights}.html`
- `pages/investment/{overview,by-sector,residential,hospitality,commercial,staff-accommodation,process}.html`
- `pages/news-media/{latest-news,media-centre,publications,in-the-media}.html`
- `pages/careers/{working-at-marjan,current-openings,life-at-marjan}.html`
- `pages/resources/{downloads,faqs,glossary,investment-calculator}.html`
- `pages/legal/{legal-notices,regulatory,anti-corruption,data-protection}.html`

**Untouched:** README, sitemap PDF, `.claude/`, `docs/`, `.git/`.

---

## Task 1: Rewrite `styles/wireframe.css` — tokens, base, typography, layout, header, footer

**Files:**
- Modify (full rewrite): `styles/wireframe.css`

- [ ] **Step 1: Replace the file header (imports + reset + tokens + base typography).** Replace the existing top of `styles/wireframe.css` (the `@import` + `:root` + `body`) with the block below. This is the foundation — every later visual depends on these tokens.

```css
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:ital,wght@0,300;0,400;0,500;0,600;0,700;1,400&family=Montserrat:wght@300;400;500;600;700&display=swap');

/* Marjan — Master Developer of Ras Al Khaimah */

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  /* Brand */
  --ink: #00002E;
  --ink-deep: #000006;
  --navy: #282856;
  --navy-soft: #3B5173;
  --mist: #13294B;

  /* Surfaces */
  --paper: #FFFFFF;
  --surface: #F9F9F9;
  --surface-2: #F5F5F5;

  /* Lines & text */
  --line: #E5E7EB;
  --line-soft: #D7D7D7;
  --muted: #999999;
  --text: #00002E;

  /* Layout */
  --max-w: 1320px;

  /* Type */
  --font-display: 'Montserrat', -apple-system, BlinkMacSystemFont, "Helvetica Neue", sans-serif;
  --font-sans:    'IBM Plex Sans', -apple-system, BlinkMacSystemFont, "Helvetica Neue", sans-serif;
}

html { scroll-behavior: smooth; }

body {
  background: var(--paper);
  color: var(--text);
  font-family: var(--font-sans);
  font-size: 16px;
  line-height: 1.65;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

a { color: inherit; text-decoration: none; }

::selection { background: var(--ink); color: var(--paper); }

/* Page load animation */
@keyframes wfFadeUp {
  from { opacity: 0; transform: translateY(16px); }
  to { opacity: 1; transform: translateY(0); }
}
.wf-anim { opacity: 0; animation: wfFadeUp 0.9s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
.wf-anim-1 { animation-delay: 0.05s; }
.wf-anim-2 { animation-delay: 0.15s; }
.wf-anim-3 { animation-delay: 0.25s; }
.wf-anim-4 { animation-delay: 0.35s; }
.wf-anim-5 { animation-delay: 0.45s; }
```

- [ ] **Step 2: Replace the HEADER block.** Find the `/* ====== HEADER ====== */` section in the existing CSS and replace it with the block below. Keep the wf- selectors so existing HTML keeps working until pages are rewritten.

```css
.wf-header {
  position: sticky;
  top: 0;
  z-index: 50;
  background: rgba(255, 255, 255, 0.92);
  backdrop-filter: saturate(180%) blur(20px);
  -webkit-backdrop-filter: saturate(180%) blur(20px);
  border-bottom: 1px solid var(--line);
}
.wf-header-inner {
  max-width: var(--max-w);
  margin: 0 auto;
  padding: 20px 40px;
  display: flex;
  align-items: center;
  gap: 48px;
}
.wf-logo {
  font-family: var(--font-display);
  font-weight: 600;
  font-size: 18px;
  letter-spacing: 0.12em;
  color: var(--ink);
  text-transform: uppercase;
}
.wf-nav {
  flex: 1;
  display: flex;
  flex-wrap: wrap;
  gap: 28px;
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 0.06em;
  text-transform: uppercase;
}
.wf-nav a {
  color: var(--ink);
  padding: 6px 0;
  position: relative;
  opacity: 0.7;
  transition: opacity 0.25s ease;
}
.wf-nav a:hover { opacity: 1; }
.wf-nav a.is-current { opacity: 1; }
.wf-nav a.is-current::after {
  content: "";
  position: absolute;
  left: 0; right: 0;
  bottom: -2px;
  height: 1px;
  background: var(--ink);
}
.wf-header-cta {
  background: var(--ink);
  color: var(--paper);
  padding: 12px 22px;
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  transition: background 0.25s ease;
}
.wf-header-cta:hover { background: var(--navy); }

/* Breadcrumb */
.wf-breadcrumb {
  max-width: var(--max-w);
  margin: 0 auto;
  padding: 24px 40px 0;
  font-size: 11px;
  color: var(--muted);
  letter-spacing: 0.14em;
  text-transform: uppercase;
  font-weight: 500;
}
.wf-breadcrumb a { color: var(--muted); transition: color 0.25s; }
.wf-breadcrumb a:hover { color: var(--ink); }
.wf-breadcrumb .sep { margin: 0 12px; opacity: 0.5; }

/* Section sub-nav (tabs within a section) */
.wf-section-nav {
  max-width: var(--max-w);
  margin: 0 auto;
  padding: 28px 40px 0;
  display: flex;
  flex-wrap: wrap;
  border-bottom: 1px solid var(--line);
}
.wf-section-nav a {
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.10em;
  text-transform: uppercase;
  padding: 16px 20px 18px;
  color: var(--muted);
  border-bottom: 2px solid transparent;
  margin-bottom: -1px;
  transition: color 0.25s, border-color 0.25s;
}
.wf-section-nav a:hover { color: var(--ink); }
.wf-section-nav a.is-current { color: var(--ink); border-bottom-color: var(--ink); }
```

- [ ] **Step 3: Replace the FOOTER block.** Find the existing `/* ====== FOOTER ====== */` section and replace with the block below. Footer uses `--ink-deep` background.

```css
.wf-footer {
  background: var(--ink-deep);
  color: rgba(255, 255, 255, 0.65);
  padding-inline: max(40px, calc((100% - 1320px) / 2));
}
.wf-footer-inner {
  max-width: var(--max-w);
  margin: 0 auto;
  padding: 88px 0 56px;
  display: grid;
  grid-template-columns: 1.4fr repeat(4, 1fr);
  gap: 56px;
  font-size: 13px;
}
.wf-footer-brand {
  font-family: var(--font-display);
  font-size: 26px;
  font-weight: 500;
  color: var(--paper);
  letter-spacing: -0.01em;
  margin-bottom: 20px;
  line-height: 1.2;
  max-width: 340px;
}
.wf-footer-meta {
  font-size: 13px;
  line-height: 1.7;
  color: rgba(255, 255, 255, 0.55);
  max-width: 340px;
}
.wf-footer h5 {
  font-family: var(--font-sans);
  font-size: 10px;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.55);
  margin-bottom: 22px;
  font-weight: 600;
}
.wf-footer ul { list-style: none; }
.wf-footer li { margin-bottom: 12px; font-weight: 400; }
.wf-footer a { color: rgba(255, 255, 255, 0.78); transition: color 0.25s; }
.wf-footer a:hover { color: var(--paper); }
.wf-footer-bottom {
  max-width: var(--max-w);
  margin: 0 auto;
  padding: 24px 0;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  font-size: 11px;
  color: rgba(255, 255, 255, 0.4);
  display: flex;
  justify-content: space-between;
  gap: 20px;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}
.wf-footer-bottom a { color: rgba(255, 255, 255, 0.7); }
```

- [ ] **Step 4: Replace LAYOUT SHELL.** Find `.wf-shell`, `.wf-main` and replace with:

```css
.wf-shell {
  padding-top: 112px;
  padding-bottom: 112px;
  padding-inline: max(40px, calc((100% - 1320px) / 2));
}
.wf-shell--tight { padding-top: 64px; padding-bottom: 64px; }
.wf-shell--narrow .wf-main { max-width: 960px; margin: 0 auto; }
.wf-shell--surface { background: var(--surface); }

.wf-main { min-width: 0; }
.wf-main > section + section { margin-top: 120px; }
```

- [ ] **Step 5: Verify foundation.** Open `http://localhost:5500/index.html` in the browser. Page will still render (existing HTML is compatible with these selectors). Expected at this stage: header uppercase nav, deep-navy logo wordmark, IBM Plex body text. Old cream sections will look broken — that's expected, the rest of the CSS is rewritten in Task 2 and 3.

- [ ] **Step 6: Commit foundation.**

```bash
git add styles/wireframe.css
git commit -m "css: rewrite foundation tokens, header, footer, shell to marjan.ae brand"
```

---

## Task 2: Rewrite `styles/wireframe.css` — hero, editorial, stats, image placeholders, CTAs

**Files:**
- Modify: `styles/wireframe.css`

- [ ] **Step 1: Replace the HERO block.** Find `/* ====== HERO ====== */` and replace with:

```css
.wf-hero {
  position: relative;
  padding-top: 120px;
  padding-bottom: 120px;
  padding-inline: max(40px, calc((100% - 1320px) / 2));
  background: var(--ink-deep);
  color: var(--paper);
  overflow: hidden;
}
.wf-hero::before {
  content: "";
  position: absolute;
  inset: 0;
  background:
    radial-gradient(ellipse at 80% 30%, rgba(59, 81, 115, 0.45), transparent 55%),
    radial-gradient(ellipse at 20% 80%, rgba(19, 41, 75, 0.4), transparent 55%),
    linear-gradient(160deg, var(--mist) 0%, var(--ink-deep) 70%);
  pointer-events: none;
}
.wf-hero > * { position: relative; z-index: 1; }

.wf-hero-tag {
  display: inline-block;
  font-size: 11px;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.7);
  font-weight: 600;
  margin-bottom: 28px;
}
.wf-hero h1 {
  font-family: var(--font-display);
  font-size: clamp(44px, 6.5vw, 88px);
  font-weight: 500;
  letter-spacing: -0.02em;
  line-height: 1.02;
  color: var(--paper);
  max-width: 1080px;
  margin-bottom: 28px;
}
.wf-hero h1 em { font-style: normal; color: var(--paper); }
.wf-hero .lead {
  font-size: 19px;
  line-height: 1.55;
  color: rgba(255, 255, 255, 0.82);
  max-width: 680px;
  margin-bottom: 40px;
  font-weight: 400;
}
.wf-hero-meta {
  display: flex;
  flex-wrap: wrap;
  gap: 48px;
  padding-top: 32px;
  margin-top: 48px;
  border-top: 1px solid rgba(255, 255, 255, 0.15);
  font-size: 11px;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.55);
}
.wf-hero-meta .item strong {
  display: block;
  color: var(--paper);
  font-size: 22px;
  font-family: var(--font-display);
  font-weight: 500;
  letter-spacing: -0.01em;
  text-transform: none;
  margin-top: 6px;
}

.wf-hero--compact { padding-top: 80px; padding-bottom: 80px; }
.wf-hero--compact h1 { font-size: clamp(36px, 4.5vw, 60px); margin-bottom: 16px; }
.wf-hero--compact .lead { margin-bottom: 24px; font-size: 17px; }
```

- [ ] **Step 2: Replace the EDITORIAL BLOCKS section.** Find `/* ====== CONTENT BLOCKS ====== */` and replace with:

```css
.wf-block {
  border: none;
  padding: 0;
  position: static;
}
.wf-chapter {
  display: flex;
  align-items: center;
  gap: 14px;
  font-family: var(--font-sans);
  font-size: 11px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  font-weight: 600;
  color: var(--muted);
  margin-bottom: 28px;
}
.wf-chapter .num { color: var(--ink); }
.wf-chapter .rule {
  flex: 0 0 32px;
  height: 1px;
  background: var(--line-soft);
}
.wf-chapter .label { color: var(--ink); }

.wf-block-label {
  display: inline-block;
  font-size: 11px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--ink);
  font-weight: 600;
  margin-bottom: 20px;
  opacity: 0.8;
}

.wf-block h2 {
  font-family: var(--font-display);
  font-size: clamp(32px, 4vw, 52px);
  font-weight: 500;
  color: var(--ink);
  margin-bottom: 24px;
  letter-spacing: -0.02em;
  line-height: 1.08;
  max-width: 900px;
}
.wf-block h2 em { font-style: normal; color: var(--navy); font-weight: 500; }
.wf-block h3 {
  font-family: var(--font-display);
  font-size: 22px;
  font-weight: 500;
  color: var(--ink);
  margin-bottom: 10px;
  letter-spacing: -0.01em;
  line-height: 1.25;
}
.wf-block h4 {
  font-family: var(--font-sans);
  font-size: 16px;
  font-weight: 600;
  color: var(--ink);
  letter-spacing: 0;
  margin-bottom: 8px;
}
.wf-block p {
  font-size: 16.5px;
  line-height: 1.7;
  color: var(--ink);
  opacity: 0.78;
  margin-bottom: 18px;
  max-width: 680px;
}
.wf-block p:last-child { margin-bottom: 0; }
.wf-block p.large {
  font-family: var(--font-display);
  font-size: 24px;
  line-height: 1.45;
  font-weight: 400;
  color: var(--ink);
  opacity: 1;
  letter-spacing: -0.01em;
  max-width: 820px;
}
.wf-block ul.bullets { list-style: none; margin-bottom: 18px; }
.wf-block ul.bullets li {
  position: relative;
  padding-left: 22px;
  margin-bottom: 10px;
  line-height: 1.65;
  color: var(--ink);
  opacity: 0.78;
}
.wf-block ul.bullets li::before {
  content: "";
  position: absolute;
  left: 0; top: 0.7em;
  width: 10px;
  height: 1px;
  background: var(--navy);
}

/* Asymmetric editorial split */
.wf-editorial {
  display: grid;
  grid-template-columns: 5fr 7fr;
  gap: 80px;
  align-items: start;
}
.wf-editorial--right { grid-template-columns: 7fr 5fr; }
.wf-editorial--7-5 { grid-template-columns: 7fr 5fr; }
.wf-editorial--5-7 { grid-template-columns: 5fr 7fr; }

/* Pull quote */
.wf-pullquote {
  font-family: var(--font-display);
  font-size: clamp(26px, 3.2vw, 38px);
  font-weight: 400;
  line-height: 1.3;
  letter-spacing: -0.01em;
  color: var(--ink);
  padding: 48px 0;
  border-top: 1px solid var(--ink);
  border-bottom: 1px solid var(--ink);
  margin: 56px 0;
  position: relative;
}
.wf-pullquote::before { content: ""; }
.wf-pullquote cite {
  display: block;
  font-family: var(--font-sans);
  font-size: 11px;
  font-style: normal;
  color: var(--muted);
  font-weight: 600;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  margin-top: 28px;
}
```

- [ ] **Step 3: Replace IMAGE PLACEHOLDERS.** Find `/* ====== IMAGE PLACEHOLDERS ====== */` and replace with cool-navy gradient set:

```css
.wf-img {
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: flex-end;
  justify-content: flex-start;
  background:
    radial-gradient(ellipse at 75% 25%, rgba(59, 81, 115, 0.55), transparent 50%),
    linear-gradient(160deg, var(--mist) 0%, var(--ink-deep) 75%);
  min-height: 280px;
  padding: 20px 24px;
  color: rgba(255, 255, 255, 0.92);
}
.wf-img::before {
  content: "";
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='3' stitchTiles='stitch'/%3E%3CfeColorMatrix values='0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.55 0'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
  opacity: 0.15;
  mix-blend-mode: overlay;
  pointer-events: none;
}
.wf-img::after {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(180deg, transparent 45%, rgba(0, 0, 6, 0.6) 100%);
  pointer-events: none;
}
.wf-img > * { position: relative; z-index: 2; }
.wf-img--tall  { min-height: 420px; }
.wf-img--short { min-height: 200px; }
.wf-img--hero  { min-height: 560px; }

/* Variants — all cool-led, with warm light glints at horizon */
.wf-img--sea   { background:
  radial-gradient(ellipse at 30% 20%, rgba(255, 230, 190, 0.18), transparent 40%),
  linear-gradient(160deg, var(--navy-soft) 0%, var(--ink) 60%, var(--ink-deep) 100%); }
.wf-img--dawn  { background:
  radial-gradient(ellipse at 75% 20%, rgba(255, 200, 140, 0.30), transparent 45%),
  linear-gradient(170deg, var(--mist) 0%, var(--ink) 60%, var(--ink-deep) 100%); }
.wf-img--sand  { background:
  radial-gradient(ellipse at 30% 30%, rgba(255, 240, 220, 0.20), transparent 55%),
  linear-gradient(135deg, var(--navy-soft) 0%, var(--ink) 70%); }
.wf-img--night { background:
  radial-gradient(ellipse at 70% 20%, rgba(59, 81, 115, 0.45), transparent 55%),
  linear-gradient(170deg, var(--ink) 0%, var(--ink-deep) 100%); }
.wf-img--cream { background:
  radial-gradient(ellipse at 25% 30%, rgba(255, 255, 255, 0.25), transparent 60%),
  linear-gradient(135deg, var(--navy-soft) 0%, var(--ink) 100%); }
.wf-img--bronze { background:
  radial-gradient(ellipse at 70% 20%, rgba(255, 210, 150, 0.25), transparent 50%),
  linear-gradient(150deg, var(--mist) 0%, var(--ink-deep) 100%); }
.wf-img--warm  { background:
  radial-gradient(ellipse at 75% 20%, rgba(255, 200, 140, 0.30), transparent 45%),
  linear-gradient(170deg, var(--mist) 0%, var(--ink-deep) 100%); }
.wf-img--cool  { background:
  radial-gradient(ellipse at 30% 20%, rgba(255, 230, 190, 0.18), transparent 40%),
  linear-gradient(160deg, var(--navy-soft) 0%, var(--ink-deep) 100%); }
.wf-img--mono  { background:
  radial-gradient(ellipse at 25% 30%, rgba(255, 255, 255, 0.15), transparent 50%),
  linear-gradient(135deg, var(--navy) 0%, var(--ink-deep) 100%); }

.wf-img-caption {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 10px;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.92);
}
.wf-img-caption::before {
  content: "";
  width: 24px;
  height: 1px;
  background: rgba(255, 255, 255, 0.7);
}
.wf-img-caption .frame-num {
  font-family: var(--font-display);
  font-weight: 500;
  letter-spacing: -0.01em;
  text-transform: none;
  font-size: 12px;
  color: rgba(255, 255, 255, 0.6);
}
.wf-img .caption {
  background: rgba(255, 255, 255, 0.92);
  color: var(--ink);
  padding: 4px 10px;
  font-size: 10px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  font-weight: 600;
}

.wf-band { width: 100%; margin-block: 96px; }
.wf-band .wf-img { min-height: 60vh; }
```

- [ ] **Step 2.5: Verify hero + editorial.** Open `http://localhost:5500/pages/hospitality/hard-rock.html`. Expected: hero is now deep-navy gradient with white text. Body sections use Montserrat headings and IBM Plex paragraphs.

- [ ] **Step 4: Replace CARDS / GRID / CTAs / STATS / FORMS / CHIPS / NOTE / TABS / DARK SECTION / RELATED.** Find each block in turn and replace with the styled versions below.

```css
/* ====== GRID UTILITIES ====== */
.wf-grid { display: grid; gap: 32px; }
.wf-grid--2 { grid-template-columns: 1fr 1fr; }
.wf-grid--3 { grid-template-columns: 1fr 1fr 1fr; }
.wf-grid--4 { grid-template-columns: repeat(4, 1fr); }
.wf-grid--auto { grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); }
.wf-grid--12 { grid-template-columns: 1.4fr 1fr; gap: 80px; align-items: start; }
.wf-grid--tight { gap: 1px; background: var(--line); }
.wf-grid--tight > * { background: var(--paper); padding: 32px; }

/* ====== CARDS — portfolio tile ====== */
.wf-card {
  display: flex;
  flex-direction: column;
  background: var(--paper);
  border: none;
  transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}
.wf-card:hover { transform: translateY(-3px); }
.wf-card .wf-img { min-height: 320px; }
.wf-card-body { padding: 24px 0 8px; }
.wf-card > h4, .wf-card > .meta, .wf-card > p, .wf-card > a:not(.wf-cta) { padding-left: 0; padding-right: 0; }
.wf-card > h4 { padding-top: 22px; }
.wf-card .meta {
  font-size: 10px;
  font-weight: 600;
  color: var(--navy);
  letter-spacing: 0.20em;
  text-transform: uppercase;
  margin-bottom: 12px;
}
.wf-card h4 {
  font-family: var(--font-display);
  font-size: 22px;
  font-weight: 500;
  color: var(--ink);
  margin-bottom: 10px;
  letter-spacing: -0.01em;
  line-height: 1.25;
}
.wf-card p {
  font-size: 15px;
  line-height: 1.65;
  color: var(--ink);
  opacity: 0.78;
  margin-bottom: 18px;
  max-width: 100%;
}
.wf-card a:not(.wf-cta) {
  font-size: 11px;
  color: var(--ink);
  font-weight: 600;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding-top: 14px;
  border-top: 1px solid var(--line);
  transition: gap 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}
.wf-card a:not(.wf-cta):hover { gap: 14px; }

/* ====== CTAs ====== */
.wf-cta-row { display: flex; gap: 14px; flex-wrap: wrap; margin-top: 32px; }
.wf-cta {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background: var(--ink);
  color: var(--paper);
  padding: 16px 28px;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  transition: background 0.25s cubic-bezier(0.16, 1, 0.3, 1);
  border: 1px solid var(--ink);
}
.wf-cta:hover { background: var(--navy); border-color: var(--navy); }
.wf-cta--ghost { background: transparent; color: var(--ink); }
.wf-cta--ghost:hover { background: var(--ink); color: var(--paper); }
.wf-cta--light { background: var(--paper); color: var(--ink); border-color: var(--paper); }
.wf-cta--light:hover { background: transparent; color: var(--paper); border-color: var(--paper); }

/* ====== STATS ====== */
.wf-stat { border: none; padding: 0; text-align: left; }
.wf-stat .num {
  font-family: var(--font-display);
  font-size: clamp(48px, 5.5vw, 72px);
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.035em;
  display: block;
  margin-bottom: 14px;
  line-height: 0.95;
  font-feature-settings: "tnum", "lnum";
}
.wf-stat .num em { font-style: normal; color: var(--navy); }
.wf-stat .label {
  font-size: 11px;
  color: var(--muted);
  letter-spacing: 0.18em;
  text-transform: uppercase;
  font-weight: 600;
  display: block;
  padding-top: 12px;
  border-top: 1px solid var(--ink);
  max-width: 220px;
}

/* ====== TABLES ====== */
.wf-list { width: 100%; border-collapse: collapse; font-size: 14.5px; }
.wf-list th, .wf-list td {
  text-align: left;
  padding: 20px 16px;
  border-bottom: 1px solid var(--line);
}
.wf-list th {
  font-weight: 600;
  color: var(--ink);
  border-bottom: 1px solid var(--ink);
  font-size: 10px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  padding-top: 0;
}
.wf-list tr:hover td { background: var(--surface); }
.wf-list td strong { font-weight: 600; color: var(--ink); }
.wf-list a { color: var(--ink); border-bottom: 1px solid var(--navy); padding-bottom: 1px; }
.wf-list a:hover { color: var(--navy); }

/* ====== FORMS ====== */
.wf-form { display: grid; gap: 16px; max-width: 600px; }
.wf-field {
  border: none;
  border-bottom: 1px solid var(--line);
  padding: 16px 0;
  background: transparent;
  font-size: 15px;
  color: var(--ink);
  font-family: inherit;
  transition: border-color 0.25s;
}
.wf-field::placeholder { color: var(--muted); }
.wf-field:hover, .wf-field:focus { border-bottom-color: var(--ink); outline: none; }
.wf-field--tall { min-height: 110px; padding-top: 16px; }

/* ====== CHIPS ====== */
.wf-chips { display: flex; flex-wrap: wrap; gap: 10px; margin-bottom: 32px; }
.wf-chip {
  border: 1px solid var(--line-soft);
  padding: 10px 18px;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.10em;
  text-transform: uppercase;
  color: var(--ink);
  background: transparent;
  cursor: pointer;
  transition: all 0.25s;
}
.wf-chip:hover { border-color: var(--ink); }
.wf-chip.is-active { background: var(--ink); color: var(--paper); border-color: var(--ink); }

/* ====== NOTE / CALLOUT ====== */
.wf-note {
  background: var(--surface);
  border: none;
  border-left: 2px solid var(--navy);
  padding: 20px 28px;
  font-size: 15px;
  color: var(--ink);
  margin: 28px 0;
  line-height: 1.6;
}
.wf-note strong { color: var(--ink); font-weight: 600; }

/* ====== TABS ====== */
.wf-tabs {
  display: flex;
  border-bottom: 1px solid var(--line);
  margin-bottom: 40px;
  flex-wrap: wrap;
}
.wf-tab {
  padding: 18px 26px;
  border: none;
  background: transparent;
  color: var(--muted);
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  border-bottom: 1px solid transparent;
  margin-bottom: -1px;
  transition: color 0.25s, border-color 0.25s;
  cursor: pointer;
  font-family: inherit;
}
.wf-tab:hover { color: var(--ink); }
.wf-tab.is-active { color: var(--ink); border-bottom-color: var(--ink); }

/* ====== DARK SECTION (full-bleed) ====== */
.wf-dark-section {
  background: var(--ink-deep);
  color: var(--paper);
  padding: 120px 40px;
  padding-inline: max(40px, calc((100% - 1320px) / 2));
  position: relative;
  overflow: hidden;
}
.wf-dark-section::before {
  content: "";
  position: absolute;
  inset: 0;
  background:
    radial-gradient(ellipse at 80% 20%, rgba(59, 81, 115, 0.35), transparent 55%),
    radial-gradient(ellipse at 10% 90%, rgba(19, 41, 75, 0.35), transparent 55%);
  pointer-events: none;
}
.wf-dark-section > * { position: relative; z-index: 1; }
.wf-dark-section .wf-block h2,
.wf-dark-section .wf-block h3,
.wf-dark-section .wf-block h4 { color: var(--paper); }
.wf-dark-section .wf-block p { color: rgba(255, 255, 255, 0.78); opacity: 1; }
.wf-dark-section .wf-block-label,
.wf-dark-section .wf-chapter .label,
.wf-dark-section .wf-chapter .num { color: rgba(255, 255, 255, 0.55); }
.wf-dark-section .wf-stat .num { color: var(--paper); }
.wf-dark-section .wf-stat .num em { color: rgba(255, 255, 255, 0.7); }
.wf-dark-section .wf-stat .label { color: rgba(255, 255, 255, 0.55); border-top-color: rgba(255, 255, 255, 0.4); }
.wf-dark-section .wf-chapter .rule { background: rgba(255, 255, 255, 0.3); }

/* ====== RELATED STRIP ====== */
.wf-related {
  background: var(--surface);
  padding-top: 120px;
  padding-bottom: 120px;
  padding-inline: max(40px, calc((100% - 1320px) / 2));
  border-top: 1px solid var(--line);
}
.wf-related .wf-chapter { margin-bottom: 48px; }
```

- [ ] **Step 5: Verify cards/CTAs/stats.** Open `http://localhost:5500/pages/hospitality/hard-rock.html` and scroll. Cards now use navy meta labels, ink CTAs, dark sections are near-black with subtle navy glow. No bronze or cream should be visible anywhere.

- [ ] **Step 6: Commit.**

```bash
git add styles/wireframe.css
git commit -m "css: rewrite hero, editorial, stats, cards, CTAs, dark section to marjan brand"
```

---

## Task 3: Rewrite `styles/wireframe.css` — specialist patterns + index page + responsive

**Files:**
- Modify: `styles/wireframe.css`

- [ ] **Step 1: Replace INDEX PAGE block.** Find `/* ====== INDEX PAGE (sitemap navigator) ====== */` and replace the entire block with:

```css
.wf-index-header {
  background: rgba(255, 255, 255, 0.92);
  backdrop-filter: saturate(180%) blur(20px);
  border-bottom: 1px solid var(--line);
  position: sticky;
  top: 0;
  z-index: 50;
}
.wf-index-header-inner {
  max-width: var(--max-w);
  margin: 0 auto;
  padding: 20px 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 24px;
}
.wf-index-header-left { display: flex; align-items: center; gap: 24px; }
.wf-index-header .tag {
  font-size: 11px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--muted);
  font-weight: 500;
}
.wf-index-header-right { display: flex; gap: 24px; font-size: 11px; font-weight: 600; letter-spacing: 0.14em; text-transform: uppercase; }
.wf-index-header-right a { color: var(--muted); transition: color 0.25s; }
.wf-index-header-right a:hover { color: var(--ink); }

.wf-index-hero-v2 {
  max-width: var(--max-w);
  margin: 0 auto;
  padding: 96px 40px 64px;
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 64px;
  align-items: end;
}
.wf-index-hero-v2 h1 {
  font-family: var(--font-display);
  font-size: clamp(44px, 6vw, 80px);
  font-weight: 500;
  letter-spacing: -0.02em;
  color: var(--ink);
  margin-bottom: 22px;
  line-height: 1;
}
.wf-index-hero-v2 h1 em { font-style: normal; color: var(--navy); }
.wf-index-hero-v2 .lead {
  font-size: 17px;
  max-width: 620px;
  line-height: 1.6;
  color: var(--ink);
  opacity: 0.78;
}
.wf-index-hero-v2 .legend {
  display: flex;
  flex-direction: column;
  gap: 14px;
  font-size: 12px;
  color: var(--muted);
}
.wf-index-hero-v2 .legend .row { display: flex; align-items: center; gap: 14px; }
.wf-index-hero-v2 .legend .mark {
  width: 28px; height: 18px;
  border: 1px solid var(--ink);
}
.wf-index-hero-v2 .legend .mark--full    { background: var(--ink); }
.wf-index-hero-v2 .legend .mark--partial { background: var(--paper); }
.wf-index-hero-v2 .legend .mark--new     { background: var(--paper); border-style: dashed; border-color: var(--navy); }

.wf-stats-strip {
  max-width: var(--max-w);
  margin: 56px auto 0;
  padding: 0 40px;
}
.wf-stats-strip-inner {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  border-top: 1px solid var(--ink);
  border-bottom: 1px solid var(--ink);
}
.wf-stats-strip .stat {
  padding: 28px 20px;
  border-right: 1px solid var(--line);
}
.wf-stats-strip .stat:last-child { border-right: none; }
.wf-stats-strip .num {
  font-family: var(--font-display);
  font-size: 38px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.025em;
  display: block;
  margin-bottom: 8px;
  line-height: 0.95;
}
.wf-stats-strip .label {
  font-size: 10.5px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--muted);
  font-weight: 600;
}

.wf-section-head {
  max-width: var(--max-w);
  margin: 96px auto 32px;
  padding: 0 40px 20px;
  display: flex;
  align-items: baseline;
  gap: 24px;
  border-bottom: 1px solid var(--line);
}
.wf-section-head h2 {
  font-family: var(--font-display);
  font-size: 34px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.02em;
}
.wf-section-head .desc { color: var(--muted); font-size: 14px; flex: 1; line-height: 1.5; }
.wf-section-head .count {
  font-size: 10px;
  color: var(--ink);
  letter-spacing: 0.18em;
  text-transform: uppercase;
  font-weight: 600;
}

.wf-card-grid {
  max-width: var(--max-w);
  margin: 0 auto;
  padding: 0 40px;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
  gap: 24px;
}

.wf-sec-card {
  background: var(--paper);
  border: 1px solid var(--line);
  padding: 32px;
  display: flex;
  flex-direction: column;
  transition: border-color 0.3s, transform 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}
.wf-sec-card:hover { border-color: var(--ink); transform: translateY(-3px); }
.wf-sec-card-head {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 16px;
  margin-bottom: 24px;
  padding-bottom: 20px;
  border-bottom: 1px solid var(--line);
}
.wf-sec-card-head .num {
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--navy);
  margin-bottom: 8px;
  display: block;
}
.wf-sec-card-head h3 {
  font-family: var(--font-display);
  font-size: 24px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.015em;
  line-height: 1.15;
}
.wf-sec-card-badge {
  font-size: 9.5px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  padding: 6px 10px;
  border: 1px solid var(--ink);
  color: var(--ink);
  white-space: nowrap;
  font-weight: 600;
  align-self: flex-start;
}
.wf-sec-card-badge--full    { background: var(--ink); color: var(--paper); }
.wf-sec-card-badge--partial { background: var(--paper); }
.wf-sec-card-badge--new     { background: var(--paper); border-style: dashed; color: var(--navy); border-color: var(--navy); }

.wf-sec-card-list { flex: 1; list-style: none; margin: 0; padding: 0; }
.wf-sec-card-list a {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 0;
  color: var(--ink);
  border-bottom: 1px solid var(--line);
  gap: 12px;
  font-size: 14px;
  font-weight: 500;
  transition: padding-left 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}
.wf-sec-card-list li:last-child a { border-bottom: none; }
.wf-sec-card-list a:hover { padding-left: 6px; }
.wf-sec-card-list .marker { font-size: 11px; color: var(--navy); }

.wf-sec-card-foot {
  margin-top: 20px;
  padding-top: 16px;
  border-top: 1px solid var(--line);
  font-size: 10px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--muted);
  display: flex;
  justify-content: space-between;
  font-weight: 600;
}
```

- [ ] **Step 2: Replace SPECIALIST PATTERNS block.** Find each of the following sub-blocks and replace in turn:

```css
/* ====== Search ====== */
.wf-search {
  display: flex;
  align-items: center;
  border: 1px solid var(--line);
  background: var(--paper);
  max-width: 720px;
  transition: border-color 0.25s;
}
.wf-search:hover { border-color: var(--ink); }
.wf-search input {
  flex: 1;
  border: none;
  background: transparent;
  padding: 20px 24px;
  font-size: 16px;
  font-family: inherit;
  color: var(--ink);
}
.wf-search input::placeholder { color: var(--muted); }
.wf-search input:focus { outline: none; }
.wf-search button {
  background: var(--ink);
  color: var(--paper);
  border: none;
  padding: 20px 28px;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  cursor: pointer;
  font-family: inherit;
}

/* ====== Doc meta strip (legal pages) ====== */
.wf-doc-meta {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1px;
  background: var(--line);
  border: 1px solid var(--line);
  margin: 32px 0;
  font-size: 12px;
}
.wf-doc-meta .item { background: var(--paper); padding: 18px 22px; }
.wf-doc-meta .item .label {
  display: block;
  font-size: 10px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--muted);
  font-weight: 600;
  margin-bottom: 6px;
}
.wf-doc-meta .item strong {
  color: var(--ink);
  font-weight: 500;
  font-family: var(--font-display);
  font-size: 16px;
}

/* ====== Two-column document layout (legal) ====== */
.wf-doc {
  display: grid;
  grid-template-columns: 1fr 240px;
  gap: 80px;
  max-width: 1240px;
  margin: 0 auto;
  padding: 80px 40px 120px;
  padding-inline: max(40px, calc((100% - 1320px) / 2));
}
.wf-doc-body { min-width: 0; }
.wf-doc-body .article { margin-bottom: 64px; scroll-margin-top: 96px; }
.wf-doc-body .article:last-child { margin-bottom: 0; }
.wf-doc-body .article-num {
  display: block;
  font-family: var(--font-sans);
  font-size: 11px;
  font-weight: 600;
  color: var(--navy);
  letter-spacing: 0.18em;
  text-transform: uppercase;
  margin-bottom: 12px;
}
.wf-doc-body .article h2 {
  font-family: var(--font-display);
  font-size: 30px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.02em;
  line-height: 1.15;
  margin-bottom: 20px;
}
.wf-doc-body .article h3 {
  font-family: var(--font-sans);
  font-size: 15px;
  font-weight: 600;
  color: var(--ink);
  margin-top: 28px;
  margin-bottom: 10px;
}
.wf-doc-body .article p { font-size: 15.5px; line-height: 1.75; margin-bottom: 16px; max-width: 720px; color: var(--ink); opacity: 0.85; }
.wf-doc-body .article ul, .wf-doc-body .article ol { margin: 0 0 16px 22px; }
.wf-doc-body .article li { margin-bottom: 8px; line-height: 1.65; font-size: 15.5px; color: var(--ink); opacity: 0.85; }

.wf-toc {
  position: sticky;
  top: 96px;
  align-self: start;
  font-size: 13px;
}
.wf-toc h4 {
  font-size: 10px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--navy);
  margin-bottom: 16px;
  font-weight: 600;
}
.wf-toc ol { list-style: none; counter-reset: toc-counter; padding: 0; }
.wf-toc li {
  counter-increment: toc-counter;
  border-top: 1px solid var(--line);
  position: relative;
}
.wf-toc li:last-child { border-bottom: 1px solid var(--line); }
.wf-toc li::before {
  content: counter(toc-counter, decimal-leading-zero);
  position: absolute;
  left: 0; top: 14px;
  font-size: 10px;
  color: var(--muted);
  font-weight: 600;
  letter-spacing: 0.06em;
}
.wf-toc a {
  display: block;
  padding: 14px 0 14px 36px;
  color: var(--ink);
  font-weight: 500;
  transition: padding-left 0.25s;
  line-height: 1.4;
}
.wf-toc a:hover { padding-left: 42px; }

/* ====== A-Z nav (glossary) ====== */
.wf-az-nav {
  position: sticky;
  top: 80px;
  z-index: 40;
  background: rgba(255, 255, 255, 0.94);
  backdrop-filter: blur(20px);
  border-top: 1px solid var(--line);
  border-bottom: 1px solid var(--line);
  padding: 16px 40px;
  padding-inline: max(40px, calc((100% - 1320px) / 2));
  display: flex;
  align-items: center;
  gap: 4px;
  flex-wrap: wrap;
}
.wf-az-nav .label {
  font-size: 10px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--muted);
  font-weight: 600;
  margin-right: 20px;
}
.wf-az-nav a {
  font-family: var(--font-display);
  font-size: 18px;
  font-weight: 500;
  color: var(--muted);
  padding: 6px 12px;
  transition: color 0.2s;
}
.wf-az-nav a:hover { color: var(--ink); }
.wf-az-nav a.is-active { color: var(--ink); }
.wf-az-nav a.is-empty { color: var(--line); pointer-events: none; }

/* ====== Glossary ====== */
.wf-glossary .letter-block {
  display: grid;
  grid-template-columns: 100px 1fr;
  gap: 56px;
  padding: 56px 0;
  border-top: 1px solid var(--line);
  scroll-margin-top: 140px;
}
.wf-glossary .letter-block:last-child { border-bottom: 1px solid var(--line); }
.wf-glossary .letter {
  font-family: var(--font-display);
  font-size: 80px;
  font-weight: 500;
  color: var(--ink);
  line-height: 0.9;
  letter-spacing: -0.03em;
}
.wf-glossary dl { display: grid; gap: 32px; }
.wf-glossary dt {
  font-family: var(--font-display);
  font-size: 22px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.01em;
  margin-bottom: 8px;
}
.wf-glossary dt .tag {
  display: inline-block;
  margin-left: 12px;
  font-family: var(--font-sans);
  font-size: 9.5px;
  font-weight: 600;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--navy);
  padding: 3px 8px;
  border: 1px solid var(--navy);
  vertical-align: 4px;
}
.wf-glossary dd { font-size: 15.5px; line-height: 1.7; color: var(--ink); opacity: 0.85; max-width: 760px; }

/* ====== Accordion (FAQ) ====== */
.wf-accordion { border-top: 1px solid var(--line); }
.wf-accordion details { border-bottom: 1px solid var(--line); }
.wf-accordion summary {
  list-style: none;
  cursor: pointer;
  padding: 28px 0;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 32px;
  font-family: var(--font-display);
  font-size: 22px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.01em;
  line-height: 1.3;
  transition: color 0.2s;
}
.wf-accordion summary::-webkit-details-marker { display: none; }
.wf-accordion summary::after {
  content: "+";
  font-family: var(--font-display);
  font-size: 26px;
  color: var(--navy);
  font-weight: 400;
  line-height: 1;
  flex-shrink: 0;
  transition: transform 0.3s;
}
.wf-accordion details[open] summary::after { content: "–"; }
.wf-accordion summary:hover { color: var(--navy); }
.wf-accordion .answer { padding: 0 0 32px 0; font-size: 16px; line-height: 1.7; color: var(--ink); opacity: 0.85; max-width: 820px; }
.wf-accordion .answer p { margin-bottom: 16px; }
.wf-accordion .answer p:last-child { margin-bottom: 0; }
.wf-accordion .answer a { color: var(--ink); border-bottom: 1px solid var(--navy); padding-bottom: 1px; }

/* ====== Feature (news lead) ====== */
.wf-feature {
  display: grid;
  grid-template-columns: 1.3fr 1fr;
  gap: 56px;
  align-items: center;
  border-top: 1px solid var(--ink);
  border-bottom: 1px solid var(--line);
  padding: 56px 0;
}
.wf-feature .wf-img { min-height: 440px; }
.wf-feature .meta {
  display: flex;
  gap: 24px;
  font-size: 10px;
  font-weight: 600;
  color: var(--navy);
  letter-spacing: 0.18em;
  text-transform: uppercase;
  margin-bottom: 20px;
}
.wf-feature h2 {
  font-family: var(--font-display);
  font-size: 40px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.02em;
  line-height: 1.05;
  margin-bottom: 20px;
}
.wf-feature p { font-size: 16px; line-height: 1.65; margin-bottom: 24px; color: var(--ink); opacity: 0.78; }

/* ====== News row (compact) ====== */
.wf-news-row {
  display: grid;
  grid-template-columns: 180px 1fr auto;
  gap: 32px;
  align-items: baseline;
  padding: 28px 0;
  border-bottom: 1px solid var(--line);
}
.wf-news-row:last-child { border-bottom: none; }
.wf-news-row .date {
  font-size: 12px;
  color: var(--muted);
  letter-spacing: 0.08em;
  text-transform: uppercase;
  font-weight: 500;
}
.wf-news-row .body h4 {
  font-family: var(--font-display);
  font-size: 22px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.01em;
  margin-bottom: 8px;
  line-height: 1.25;
}
.wf-news-row .body .meta {
  font-size: 10px;
  color: var(--navy);
  letter-spacing: 0.18em;
  text-transform: uppercase;
  font-weight: 600;
}
.wf-news-row .body p { font-size: 14px; line-height: 1.55; margin-top: 6px; color: var(--ink); opacity: 0.78; max-width: 640px; }
.wf-news-row a.arrow {
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--ink);
}

/* ====== Toolbar (filters) ====== */
.wf-toolbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 24px;
  padding: 20px 0;
  border-top: 1px solid var(--line);
  border-bottom: 1px solid var(--line);
  margin-bottom: 48px;
  flex-wrap: wrap;
}
.wf-toolbar .count {
  font-size: 11px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--muted);
  font-weight: 600;
}

/* ====== Jobs ====== */
.wf-jobs { border-top: 1px solid var(--ink); }
.wf-job {
  display: grid;
  grid-template-columns: 60px 1.5fr 1fr 1fr 1fr auto;
  gap: 24px;
  align-items: center;
  padding: 24px 0;
  border-bottom: 1px solid var(--line);
  font-size: 14px;
}
.wf-job .num {
  font-family: var(--font-display);
  font-size: 18px;
  font-weight: 500;
  color: var(--muted);
}
.wf-job .role {
  font-family: var(--font-display);
  font-size: 20px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.01em;
  line-height: 1.2;
}
.wf-job .role-desc { font-size: 12.5px; color: var(--muted); margin-top: 4px; }
.wf-job .pill {
  display: inline-block;
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--ink);
  padding: 5px 10px;
  border: 1px solid var(--line-soft);
}
.wf-job .apply {
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--ink);
  border: 1px solid var(--ink);
  padding: 10px 18px;
  transition: background 0.2s, color 0.2s;
}
.wf-job .apply:hover { background: var(--ink); color: var(--paper); }

/* ====== Process timeline ====== */
.wf-process {
  position: relative;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 32px;
}
.wf-process::before {
  content: "";
  position: absolute;
  top: 24px;
  left: 0; right: 0;
  height: 1px;
  background: var(--line);
}
.wf-process .step { position: relative; padding-top: 64px; }
.wf-process .step::before {
  content: "";
  position: absolute;
  top: 18px; left: 0;
  width: 12px;
  height: 12px;
  background: var(--ink);
  border: 3px solid var(--paper);
  box-shadow: 0 0 0 1px var(--ink);
}
.wf-process .step .num {
  display: block;
  font-family: var(--font-sans);
  font-size: 11px;
  font-weight: 600;
  color: var(--navy);
  letter-spacing: 0.18em;
  text-transform: uppercase;
  margin-bottom: 10px;
}
.wf-process .step h4 {
  font-family: var(--font-display);
  font-size: 22px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.01em;
  margin-bottom: 12px;
  line-height: 1.2;
}
.wf-process .step p { font-size: 13.5px; line-height: 1.55; color: var(--ink); opacity: 0.78; margin-bottom: 0; }
.wf-process .step .timeline {
  display: block;
  margin-top: 12px;
  font-size: 10px;
  color: var(--muted);
  letter-spacing: 0.14em;
  text-transform: uppercase;
  font-weight: 600;
}

/* ====== Vertical process ====== */
.wf-process-v { display: grid; gap: 4px; }
.wf-process-v .step {
  display: grid;
  grid-template-columns: 88px 1fr;
  gap: 32px;
  padding: 32px 0;
  border-top: 1px solid var(--line);
}
.wf-process-v .step:last-child { border-bottom: 1px solid var(--line); }
.wf-process-v .step .step-num {
  font-family: var(--font-display);
  font-size: 56px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.04em;
  line-height: 0.9;
}
.wf-process-v .step h4 {
  font-family: var(--font-display);
  font-size: 24px;
  font-weight: 500;
  color: var(--ink);
  margin-bottom: 10px;
  letter-spacing: -0.01em;
}
.wf-process-v .step p { font-size: 15px; line-height: 1.65; margin-bottom: 8px; max-width: 720px; color: var(--ink); opacity: 0.85; }
.wf-process-v .step .timing {
  display: inline-block;
  margin-top: 8px;
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--navy);
}

/* ====== Calculator ====== */
.wf-tool {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: 80px;
  align-items: start;
  margin: 56px 0;
}
.wf-tool-inputs {
  background: var(--surface);
  padding: 40px;
  position: sticky;
  top: 96px;
}
.wf-tool-inputs h3 {
  font-family: var(--font-display);
  font-size: 22px;
  font-weight: 500;
  color: var(--ink);
  margin-bottom: 24px;
}
.wf-tool-inputs .field {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  padding: 16px 0;
  border-bottom: 1px solid var(--line);
  font-size: 13.5px;
}
.wf-tool-inputs .field:last-child { border-bottom: none; }
.wf-tool-inputs .field label { color: var(--ink); font-weight: 500; }
.wf-tool-inputs .field .val {
  font-family: var(--font-display);
  font-size: 18px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.01em;
}
.wf-tool-outputs h3 {
  font-family: var(--font-display);
  font-size: 28px;
  font-weight: 500;
  margin-bottom: 24px;
}
.wf-result-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1px;
  background: var(--line);
  border: 1px solid var(--line);
  margin-bottom: 32px;
}
.wf-result-grid .cell { background: var(--paper); padding: 28px; }
.wf-result-grid .cell .label {
  font-size: 10px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--muted);
  font-weight: 600;
  margin-bottom: 10px;
}
.wf-result-grid .cell .val {
  font-family: var(--font-display);
  font-size: 40px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.03em;
  line-height: 1;
}
.wf-result-grid .cell .val em { color: var(--navy); font-style: normal; }

/* ====== Files ====== */
.wf-files {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1px;
  background: var(--line);
  border: 1px solid var(--line);
}
.wf-file {
  background: var(--paper);
  padding: 24px 24px 28px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  transition: background 0.2s;
}
.wf-file:hover { background: var(--surface); }
.wf-file .file-meta {
  font-size: 10px;
  font-weight: 600;
  color: var(--navy);
  letter-spacing: 0.18em;
  text-transform: uppercase;
}
.wf-file h4 {
  font-family: var(--font-display);
  font-size: 18px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.01em;
  line-height: 1.25;
}
.wf-file .info {
  font-size: 12px;
  color: var(--muted);
  margin-top: auto;
  padding-top: 12px;
  border-top: 1px solid var(--line);
  display: flex;
  justify-content: space-between;
  letter-spacing: 0.04em;
}
.wf-file .info a {
  font-weight: 600;
  color: var(--ink);
  letter-spacing: 0.14em;
  text-transform: uppercase;
  font-size: 11px;
}

/* ====== Essay (Life at Marjan) ====== */
.wf-essay { display: grid; gap: 4px; }
.wf-essay-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 32px;
  align-items: center;
  padding: 64px 0;
}
.wf-essay-row--text-image .text { order: 1; }
.wf-essay-row--image-text .text { order: 2; }
.wf-essay-row .text h3 {
  font-family: var(--font-display);
  font-size: 30px;
  font-weight: 500;
  letter-spacing: -0.02em;
  color: var(--ink);
  margin-bottom: 16px;
  line-height: 1.15;
}
.wf-essay-row .text p { font-size: 15.5px; line-height: 1.7; margin-bottom: 14px; max-width: 540px; color: var(--ink); opacity: 0.85; }
.wf-essay-row .text .by {
  font-size: 11px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--navy);
  font-weight: 600;
  margin-top: 16px;
}
.wf-essay-row .wf-img { min-height: 480px; }

/* ====== Category header (utility pages) ====== */
.wf-cat-head {
  display: grid;
  grid-template-columns: 80px 1fr;
  gap: 32px;
  align-items: baseline;
  margin-bottom: 32px;
  padding-bottom: 16px;
  border-bottom: 1px solid var(--ink);
}
.wf-cat-head .cat-num {
  font-family: var(--font-sans);
  font-size: 11px;
  font-weight: 600;
  color: var(--navy);
  letter-spacing: 0.18em;
  text-transform: uppercase;
}
.wf-cat-head h3 {
  font-family: var(--font-display);
  font-size: 26px;
  font-weight: 500;
  color: var(--ink);
  letter-spacing: -0.02em;
  line-height: 1.15;
}
.wf-cat-head p {
  grid-column: 2;
  font-size: 14px;
  color: var(--muted);
  margin-top: 8px;
  line-height: 1.55;
  max-width: 640px;
}
```

- [ ] **Step 3: Replace RESPONSIVE block (keep at bottom of file).** Find the existing `@media` blocks at the bottom and replace with:

```css
@media (max-width: 1100px) {
  .wf-shell { grid-template-columns: 1fr; gap: 48px; }
  .wf-editorial, .wf-editorial--right, .wf-editorial--7-5, .wf-editorial--5-7 { grid-template-columns: 1fr; gap: 40px; }
  .wf-grid--12 { grid-template-columns: 1fr; gap: 40px; }
  .wf-footer-inner { grid-template-columns: 1fr 1fr; gap: 48px; }
  .wf-index-hero-v2 { grid-template-columns: 1fr; gap: 40px; }
  .wf-doc { grid-template-columns: 1fr; gap: 40px; }
  .wf-toc { position: static; }
  .wf-feature { grid-template-columns: 1fr; gap: 32px; }
  .wf-feature .wf-img { min-height: 320px; }
  .wf-process { grid-template-columns: 1fr 1fr; }
  .wf-process::before { display: none; }
  .wf-tool { grid-template-columns: 1fr; gap: 40px; }
  .wf-tool-inputs { position: static; }
  .wf-news-row { grid-template-columns: 120px 1fr; gap: 16px; }
  .wf-news-row a.arrow { grid-column: 1 / -1; }
  .wf-job { grid-template-columns: 40px 1fr; gap: 12px; }
  .wf-job .pill, .wf-job .apply { grid-column: 2; }
  .wf-essay-row { grid-template-columns: 1fr; gap: 24px; padding: 32px 0; }
  .wf-glossary .letter-block { grid-template-columns: 1fr; gap: 24px; }
  .wf-glossary .letter { font-size: 56px; }
}
@media (max-width: 900px) {
  .wf-grid--2, .wf-grid--3, .wf-grid--4 { grid-template-columns: 1fr; }
  .wf-stats-strip-inner { grid-template-columns: repeat(3, 1fr); }
  .wf-stats-strip .stat:nth-child(3n) { border-right: none; }
  .wf-stats-strip .stat:nth-child(n+4) { border-top: 1px solid var(--line); }
  .wf-hero, .wf-related, .wf-dark-section, .wf-footer { padding-inline: 24px; }
  .wf-shell { padding: 64px 24px 80px; }
  .wf-header-inner { padding: 18px 24px; gap: 24px; }
  .wf-nav { font-size: 11px; gap: 18px; }
  .wf-footer-inner { padding: 64px 24px 40px; grid-template-columns: 1fr 1fr; }
  .wf-stats-strip, .wf-card-grid, .wf-section-head { padding-inline: 24px; }
}
@media (max-width: 600px) {
  .wf-stats-strip-inner { grid-template-columns: repeat(2, 1fr); }
  .wf-stats-strip .stat { border-right: 1px solid var(--line); }
  .wf-stats-strip .stat:nth-child(2n) { border-right: none; }
  .wf-stats-strip .stat:nth-child(n+3) { border-top: 1px solid var(--line); }
  .wf-footer-inner { grid-template-columns: 1fr; }
}
```

- [ ] **Step 4: Verify entire CSS file end-to-end.** Spot check: `http://localhost:5500/pages/resources/glossary.html`, `http://localhost:5500/pages/resources/faqs.html`, `http://localhost:5500/pages/careers/current-openings.html`, `http://localhost:5500/pages/legal/legal-notices.html`. All specialist patterns should render with new palette, no bronze visible, fonts are Montserrat + IBM Plex.

- [ ] **Step 5: Commit foundation phase.**

```bash
git add styles/wireframe.css
git commit -m "css: rewrite specialist patterns, index, responsive to marjan brand"
```

---

## Task 4: Rebuild `index.html` (sitemap navigator)

**Files:**
- Modify (full rewrite): `index.html`

- [ ] **Step 1: Replace entire file with the version below.** The structure is the same 7-section card grid, but copy is brand-aligned and the wireframe meta-language is removed.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Marjan — Phase 2</title>
  <link rel="stylesheet" href="styles/wireframe.css" />
</head>
<body>

<header class="wf-index-header">
  <div class="wf-index-header-inner">
    <div class="wf-index-header-left">
      <div class="wf-logo">MARJAN</div>
      <span class="tag">Phase 2 · Sitemap Navigator</span>
    </div>
    <div class="wf-index-header-right">
      <a href="pages/investment/overview.html">Invest</a>
      <a href="pages/news-media/latest-news.html">News</a>
      <a href="pages/careers/working-at-marjan.html">Careers</a>
    </div>
  </div>
</header>

<section class="wf-index-hero-v2">
  <div>
    <span class="wf-hero-tag" style="color: var(--navy);">Phase 2 · Master Developer of Ras Al Khaimah</span>
    <h1>Extending the<br/>Marjan Story</h1>
    <p class="lead">Seven sections and twenty-seven pages building on Phase 1 — investment, hospitality, careers, and the disciplined resources that take Marjan from a destination into a programme.</p>
  </div>
  <div class="legend">
    <div class="row"><span class="mark mark--full"></span> Full section · all sub-pages in scope</div>
    <div class="row"><span class="mark mark--partial"></span> Partial section · selected sub-pages</div>
    <div class="row"><span class="mark mark--new"></span> New section · introduced in Phase 2</div>
  </div>
</section>

<div class="wf-stats-strip">
  <div class="wf-stats-strip-inner">
    <div class="stat"><span class="num">7</span><span class="label">Sections in scope</span></div>
    <div class="stat"><span class="num">27</span><span class="label">Pages delivered</span></div>
    <div class="stat"><span class="num">3</span><span class="label">Sections, full scope</span></div>
    <div class="stat"><span class="num">2</span><span class="label">Sections, partial scope</span></div>
    <div class="stat"><span class="num">2</span><span class="label">Sections, introduced in Phase 2</span></div>
    <div class="stat"><span class="num">28</span><span class="label">HTML pages authored</span></div>
  </div>
</div>

<header class="wf-section-head">
  <h2>All sections</h2>
  <span class="desc">Every page below is authored and reachable from the live navigator.</span>
  <span class="count">7 sections · 27 pages</span>
</header>

<div class="wf-card-grid">

  <article class="wf-sec-card">
    <div class="wf-sec-card-head">
      <div>
        <span class="num">Section 01</span>
        <h3>Development</h3>
      </div>
      <span class="wf-sec-card-badge wf-sec-card-badge--partial">Partial</span>
    </div>
    <ul class="wf-sec-card-list">
      <li><a href="pages/development/future-developments.html"><span>Future Developments</span><span class="marker">→</span></a></li>
    </ul>
    <div class="wf-sec-card-foot">
      <span>1 page</span>
      <span>Pipeline · Land bank</span>
    </div>
  </article>

  <article class="wf-sec-card">
    <div class="wf-sec-card-head">
      <div>
        <span class="num">Section 02</span>
        <h3>Hospitality</h3>
      </div>
      <span class="wf-sec-card-badge wf-sec-card-badge--partial">Partial</span>
    </div>
    <ul class="wf-sec-card-list">
      <li><a href="pages/hospitality/hard-rock.html"><span>Hard Rock Hotel Al Marjan Island</span><span class="marker">→</span></a></li>
      <li><a href="pages/hospitality/branded-residences.html"><span>Branded Residences</span><span class="marker">→</span></a></li>
      <li><a href="pages/hospitality/for-operators.html"><span>For Hospitality Operators</span><span class="marker">→</span></a></li>
      <li><a href="pages/hospitality/market-insights.html"><span>Hospitality Market Insights</span><span class="marker">→</span></a></li>
    </ul>
    <div class="wf-sec-card-foot">
      <span>4 pages</span>
      <span>Operators · Insights</span>
    </div>
  </article>

  <article class="wf-sec-card">
    <div class="wf-sec-card-head">
      <div>
        <span class="num">Section 03</span>
        <h3>Investment Opportunities</h3>
      </div>
      <span class="wf-sec-card-badge wf-sec-card-badge--full">Full</span>
    </div>
    <ul class="wf-sec-card-list">
      <li><a href="pages/investment/overview.html"><span>Investment Overview</span><span class="marker">→</span></a></li>
      <li><a href="pages/investment/by-sector.html"><span>By Sector · hub</span><span class="marker">→</span></a></li>
      <li><a href="pages/investment/residential.html"><span>— Residential</span><span class="marker">→</span></a></li>
      <li><a href="pages/investment/hospitality.html"><span>— Hospitality</span><span class="marker">→</span></a></li>
      <li><a href="pages/investment/commercial.html"><span>— Commercial</span><span class="marker">→</span></a></li>
      <li><a href="pages/investment/staff-accommodation.html"><span>— Staff Accommodation</span><span class="marker">→</span></a></li>
      <li><a href="pages/investment/process.html"><span>Investment Process</span><span class="marker">→</span></a></li>
    </ul>
    <div class="wf-sec-card-foot">
      <span>7 pages</span>
      <span>Sectors · Process</span>
    </div>
  </article>

  <article class="wf-sec-card">
    <div class="wf-sec-card-head">
      <div>
        <span class="num">Section 04</span>
        <h3>News &amp; Media</h3>
      </div>
      <span class="wf-sec-card-badge wf-sec-card-badge--full">Full</span>
    </div>
    <ul class="wf-sec-card-list">
      <li><a href="pages/news-media/latest-news.html"><span>Latest News</span><span class="marker">→</span></a></li>
      <li><a href="pages/news-media/media-centre.html"><span>Media Centre</span><span class="marker">→</span></a></li>
      <li><a href="pages/news-media/publications.html"><span>Publications</span><span class="marker">→</span></a></li>
      <li><a href="pages/news-media/in-the-media.html"><span>In the Media</span><span class="marker">→</span></a></li>
    </ul>
    <div class="wf-sec-card-foot">
      <span>4 pages</span>
      <span>Press · Reports</span>
    </div>
  </article>

  <article class="wf-sec-card">
    <div class="wf-sec-card-head">
      <div>
        <span class="num">Section 05</span>
        <h3>Careers</h3>
      </div>
      <span class="wf-sec-card-badge wf-sec-card-badge--full">Full</span>
    </div>
    <ul class="wf-sec-card-list">
      <li><a href="pages/careers/working-at-marjan.html"><span>Working at Marjan</span><span class="marker">→</span></a></li>
      <li><a href="pages/careers/current-openings.html"><span>Current Openings</span><span class="marker">→</span></a></li>
      <li><a href="pages/careers/life-at-marjan.html"><span>Life at Marjan</span><span class="marker">→</span></a></li>
    </ul>
    <div class="wf-sec-card-foot">
      <span>3 pages</span>
      <span>EVP · Roles · Culture</span>
    </div>
  </article>

  <article class="wf-sec-card">
    <div class="wf-sec-card-head">
      <div>
        <span class="num">Section 06</span>
        <h3>Resources</h3>
      </div>
      <span class="wf-sec-card-badge wf-sec-card-badge--new">New</span>
    </div>
    <ul class="wf-sec-card-list">
      <li><a href="pages/resources/downloads.html"><span>Downloads</span><span class="marker">→</span></a></li>
      <li><a href="pages/resources/faqs.html"><span>FAQs</span><span class="marker">→</span></a></li>
      <li><a href="pages/resources/glossary.html"><span>Glossary</span><span class="marker">→</span></a></li>
      <li><a href="pages/resources/investment-calculator.html"><span>Investment Calculator</span><span class="marker">→</span></a></li>
    </ul>
    <div class="wf-sec-card-foot">
      <span>4 pages</span>
      <span>Utility</span>
    </div>
  </article>

  <article class="wf-sec-card">
    <div class="wf-sec-card-head">
      <div>
        <span class="num">Section 07</span>
        <h3>Legal</h3>
      </div>
      <span class="wf-sec-card-badge wf-sec-card-badge--new">New</span>
    </div>
    <ul class="wf-sec-card-list">
      <li><a href="pages/legal/legal-notices.html"><span>Legal Notices</span><span class="marker">→</span></a></li>
      <li><a href="pages/legal/regulatory.html"><span>Regulatory Information</span><span class="marker">→</span></a></li>
      <li><a href="pages/legal/anti-corruption.html"><span>Anti-Corruption Policy</span><span class="marker">→</span></a></li>
      <li><a href="pages/legal/data-protection.html"><span>Data Protection</span><span class="marker">→</span></a></li>
    </ul>
    <div class="wf-sec-card-foot">
      <span>4 pages</span>
      <span>Compliance</span>
    </div>
  </article>

</div>

<footer class="wf-footer" style="margin-top:96px;">
  <div class="wf-footer-inner">
    <div>
      <div class="wf-footer-brand">Marjan — Master Developer of Ras Al Khaimah.</div>
      <p class="wf-footer-meta">Aligned with RAK Vision 2030. Designed for life, defining the future of the emirate.</p>
    </div>
    <div>
      <h5>Development</h5>
      <ul>
        <li><a href="pages/development/future-developments.html">Future Developments</a></li>
      </ul>
    </div>
    <div>
      <h5>Hospitality</h5>
      <ul>
        <li><a href="pages/hospitality/hard-rock.html">Hard Rock Hotel</a></li>
        <li><a href="pages/hospitality/branded-residences.html">Branded Residences</a></li>
        <li><a href="pages/hospitality/for-operators.html">For Operators</a></li>
        <li><a href="pages/hospitality/market-insights.html">Market Insights</a></li>
      </ul>
    </div>
    <div>
      <h5>Invest</h5>
      <ul>
        <li><a href="pages/investment/overview.html">Overview</a></li>
        <li><a href="pages/investment/by-sector.html">By Sector</a></li>
        <li><a href="pages/investment/process.html">Process</a></li>
        <li><a href="pages/resources/investment-calculator.html">Calculator</a></li>
      </ul>
    </div>
    <div>
      <h5>Resources &amp; Legal</h5>
      <ul>
        <li><a href="pages/resources/faqs.html">FAQs</a></li>
        <li><a href="pages/resources/glossary.html">Glossary</a></li>
        <li><a href="pages/legal/legal-notices.html">Legal Notices</a></li>
        <li><a href="pages/legal/data-protection.html">Data Protection</a></li>
      </ul>
    </div>
  </div>
  <div class="wf-footer-bottom">
    <span>© 2026 Marjan LLC. All rights reserved.</span>
    <span>Phase 2 · Wireframes</span>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Verify.** Open `http://localhost:5500/`. Hero reads "Extending the Marjan Story". No wireframe-meta phrasing remains. Cards render with new tokens.

---

## Task 5: Rebuild `pages/hospitality/hard-rock.html` (anchor reference, mirror Wynn structure)

**Files:**
- Modify (full rewrite): `pages/hospitality/hard-rock.html`

The rewritten page mirrors the structure of marjan.ae's Wynn Al Marjan Island page exactly: hero → "Redefining…" intro → key facts grid → 3 thematic sections (entertainment, responsibility, growth) → closing "new era" block → related properties → footer.

- [ ] **Step 1: Read the current file to capture any existing breadcrumb/nav structure to keep.**

Run: `head -80 "/mnt/d/Code Files/al-marjan/pages/hospitality/hard-rock.html"` and confirm head structure. The new file uses the same `<head>` linking pattern.

- [ ] **Step 2: Replace the entire file with the version below.**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Hard Rock Hotel Al Marjan Island — Marjan</title>
  <link rel="stylesheet" href="../../styles/wireframe.css" />
</head>
<body>

<header class="wf-header">
  <div class="wf-header-inner">
    <a class="wf-logo" href="../../index.html">MARJAN</a>
    <nav class="wf-nav">
      <a href="../development/future-developments.html">Development</a>
      <a href="../hospitality/hard-rock.html" class="is-current">Hospitality</a>
      <a href="../investment/overview.html">Investment</a>
      <a href="../news-media/latest-news.html">News &amp; Media</a>
      <a href="../careers/working-at-marjan.html">Careers</a>
      <a href="../resources/faqs.html">Resources</a>
      <a href="../legal/legal-notices.html">Legal</a>
    </nav>
    <a class="wf-header-cta" href="#enquire">Enquire</a>
  </div>
</header>

<nav class="wf-breadcrumb">
  <a href="../../index.html">Home</a><span class="sep">/</span>
  <a href="hard-rock.html">Hospitality</a><span class="sep">/</span>
  <span>Hard Rock Hotel Al Marjan Island</span>
</nav>

<section class="wf-hero">
  <span class="wf-hero-tag">Hospitality · Under Development</span>
  <h1>Hard Rock Hotel Al Marjan Island</h1>
  <p class="lead">A landmark music-led resort on Al Marjan Island, bringing one of the world's most recognised entertainment brands to the Arabian Gulf coastline.</p>
  <div class="wf-cta-row">
    <a class="wf-cta" href="#facts">Read the Facts</a>
    <a class="wf-cta wf-cta--light" href="#enquire">Operator &amp; Investor Enquiries</a>
  </div>
  <div class="wf-hero-meta">
    <div class="item"><span>Operator</span><strong>Hard Rock International</strong></div>
    <div class="item"><span>Location</span><strong>Al Marjan Island, RAK</strong></div>
    <div class="item"><span>Status</span><strong>Under Development</strong></div>
    <div class="item"><span>Targeted Opening</span><strong>2027</strong></div>
  </div>
</section>

<section class="wf-shell">
  <div class="wf-main">

    <section class="wf-block wf-anim wf-anim-1">
      <div class="wf-chapter"><span class="num">01</span><span class="rule"></span><span class="label">Resort Concept</span></div>
      <h2>Redefining Music-Led Hospitality on the Arabian Gulf</h2>
      <p class="large">Hard Rock Hotel Al Marjan Island brings the brand's celebrated approach to design, music and entertainment to one of the region's most exciting coastal settings. Designed to feel both intimate and iconic, the resort will become a defining destination within Marjan's hospitality portfolio.</p>
      <p>The masterplan integrates the resort with the wider Al Marjan Island programme — connected to the beach district, to mobility networks, and to the cluster of partners reshaping Ras Al Khaimah as a year-round leisure capital.</p>
    </section>

    <section id="facts" class="wf-block">
      <div class="wf-chapter"><span class="num">02</span><span class="rule"></span><span class="label">Key Facts</span></div>
      <h2>Resort at a Glance</h2>
      <div class="wf-grid wf-grid--3" style="margin-top:48px;">
        <div class="wf-stat"><span class="num">600+</span><span class="label">Rooms &amp; Suites</span></div>
        <div class="wf-stat"><span class="num">8</span><span class="label">Signature Dining Venues</span></div>
        <div class="wf-stat"><span class="num">2,500</span><span class="label">Capacity Live Entertainment Venue</span></div>
        <div class="wf-stat"><span class="num">45,000</span><span class="label">Sq ft Spa &amp; Wellness</span></div>
        <div class="wf-stat"><span class="num">1,200+</span><span class="label">Projected New Jobs</span></div>
        <div class="wf-stat"><span class="num">2027</span><span class="label">Targeted Opening</span></div>
      </div>
    </section>

    <section class="wf-block">
      <div class="wf-chapter"><span class="num">03</span><span class="rule"></span><span class="label">Entertainment &amp; Culture</span></div>
      <div class="wf-editorial wf-editorial--5-7">
        <div>
          <div class="wf-img wf-img--night wf-img--tall">
            <span class="wf-img-caption">Live Venue · <span class="frame-num">F.03</span></span>
          </div>
        </div>
        <div>
          <h2>A New Destination for Music &amp; Experience</h2>
          <p>The resort is being built around purpose-designed performance spaces and a year-round programme of live music, residencies and curated events. From the lobby vibe to the main hall, Hard Rock's signature culture is engineered into the architecture rather than layered on top.</p>
          <p>Guest experience extends across themed restaurants, retail concepts, beach club programming and a memorabilia-rich interior that anchors Hard Rock's identity inside an unmistakably coastal setting.</p>
        </div>
      </div>
    </section>

    <section class="wf-block">
      <div class="wf-chapter"><span class="num">04</span><span class="rule"></span><span class="label">Responsibility</span></div>
      <h2>Setting Operational Standards from Day One</h2>
      <p>Hard Rock Hotel Al Marjan Island is being developed under the same regulatory and sustainability framework as Marjan's wider hospitality portfolio. Robust governance, transparent reporting and EarthCheck-aligned operational targets are embedded into the resort's pre-opening plan.</p>
      <ul class="bullets">
        <li>Low-impact construction practices aligned with RAK's net-zero pathway.</li>
        <li>Workforce policies that mirror Marjan's wellbeing &amp; CSR commitments.</li>
        <li>Cultural sensitivity built into programming, retail and food &amp; beverage concepts.</li>
      </ul>
    </section>

    <section class="wf-pullquote">
      Hard Rock joins a hospitality lineup that is repositioning Ras Al Khaimah as one of the most ambitious leisure destinations in the Middle East.
      <cite>Marjan Hospitality Brief · 2026</cite>
    </section>

    <section class="wf-block">
      <div class="wf-chapter"><span class="num">05</span><span class="rule"></span><span class="label">Economic Catalyst</span></div>
      <h2>A Driver of Growth for Ras Al Khaimah</h2>
      <p>The project is forecast to deliver more than 1,200 direct and indirect jobs, attract an estimated 700,000 additional annual visitors to the emirate, and contribute to the broader investment story that is making Ras Al Khaimah one of the region's fastest-growing tourism economies.</p>
      <div class="wf-cta-row">
        <a class="wf-cta" href="../investment/hospitality.html">Hospitality Investment Case</a>
        <a class="wf-cta wf-cta--ghost" href="../investment/overview.html">Investment Overview</a>
      </div>
    </section>

  </div>
</section>

<section class="wf-dark-section">
  <div class="wf-block">
    <div class="wf-chapter"><span class="num">06</span><span class="rule"></span><span class="label">A New Era</span></div>
    <h2>Setting a New Benchmark for Al Marjan Island</h2>
    <p>With Hard Rock on track to open in 2027, the resort joins Wynn Al Marjan Island, Ritz Carlton Al Wadi and the wider hospitality programme in reshaping expectations of what is possible in Ras Al Khaimah. Together, these properties form one of the most ambitious operator clusters in the region.</p>
    <div class="wf-grid wf-grid--3" style="margin-top:64px;">
      <div class="wf-stat"><span class="num">700K</span><span class="label">Additional Annual Visitors Projected</span></div>
      <div class="wf-stat"><span class="num">8</span><span class="label">Global Hospitality Partners on Island</span></div>
      <div class="wf-stat"><span class="num">2030</span><span class="label">RAK Vision Alignment</span></div>
    </div>
  </div>
</section>

<section id="enquire" class="wf-related">
  <div class="wf-chapter"><span class="num">07</span><span class="rule"></span><span class="label">Related</span></div>
  <h2 style="font-family:var(--font-display);font-size:36px;font-weight:500;color:var(--ink);letter-spacing:-0.02em;margin-bottom:48px;">Explore the Wider Programme</h2>
  <div class="wf-grid wf-grid--3">
    <article class="wf-card">
      <div class="wf-img wf-img--sea wf-img--tall"><span class="wf-img-caption">Branded Residences · <span class="frame-num">F.08</span></span></div>
      <h4>Branded Residences</h4>
      <p>The next generation of branded residential product across Al Marjan Island and the wider portfolio.</p>
      <a href="branded-residences.html">View Residences →</a>
    </article>
    <article class="wf-card">
      <div class="wf-img wf-img--dawn wf-img--tall"><span class="wf-img-caption">Operators · <span class="frame-num">F.09</span></span></div>
      <h4>For Hospitality Operators</h4>
      <p>How Marjan partners with global operators across the development lifecycle.</p>
      <a href="for-operators.html">Partnership Brief →</a>
    </article>
    <article class="wf-card">
      <div class="wf-img wf-img--mono wf-img--tall"><span class="wf-img-caption">Market Insights · <span class="frame-num">F.10</span></span></div>
      <h4>Hospitality Market Insights</h4>
      <p>Demand, occupancy and pipeline data shaping the Ras Al Khaimah hospitality outlook.</p>
      <a href="market-insights.html">Read the Insights →</a>
    </article>
  </div>
</section>

<footer class="wf-footer">
  <div class="wf-footer-inner">
    <div>
      <div class="wf-footer-brand">Marjan — Master Developer of Ras Al Khaimah.</div>
      <p class="wf-footer-meta">Aligned with RAK Vision 2030. Designed for life, defining the future of the emirate.</p>
    </div>
    <div>
      <h5>Hospitality</h5>
      <ul>
        <li><a href="hard-rock.html">Hard Rock</a></li>
        <li><a href="branded-residences.html">Branded Residences</a></li>
        <li><a href="for-operators.html">For Operators</a></li>
        <li><a href="market-insights.html">Market Insights</a></li>
      </ul>
    </div>
    <div>
      <h5>Invest</h5>
      <ul>
        <li><a href="../investment/overview.html">Overview</a></li>
        <li><a href="../investment/hospitality.html">Hospitality</a></li>
        <li><a href="../investment/process.html">Process</a></li>
      </ul>
    </div>
    <div>
      <h5>News</h5>
      <ul>
        <li><a href="../news-media/latest-news.html">Latest News</a></li>
        <li><a href="../news-media/media-centre.html">Media Centre</a></li>
      </ul>
    </div>
    <div>
      <h5>Resources</h5>
      <ul>
        <li><a href="../resources/faqs.html">FAQs</a></li>
        <li><a href="../resources/downloads.html">Downloads</a></li>
      </ul>
    </div>
  </div>
  <div class="wf-footer-bottom">
    <span>© 2026 Marjan LLC. All rights reserved.</span>
    <span>info@marjan.ae · +971 (7) 203 5000</span>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 3: Verify.** Open `http://localhost:5500/pages/hospitality/hard-rock.html`. Hero shows the new headline, key facts grid renders, dark section is near-black with navy glow, no console errors.

---

## Task 6: Rebuild `pages/development/future-developments.html`

**Files:**
- Modify (full rewrite): `pages/development/future-developments.html`

- [ ] **Step 1: Replace the file with the version below.** Structure mirrors marjan.ae's `/development/our-approach` page (hero → philosophy → planning methodology → design principles → infrastructure → CTA).

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Future Developments — Marjan</title>
  <link rel="stylesheet" href="../../styles/wireframe.css" />
</head>
<body>

<header class="wf-header">
  <div class="wf-header-inner">
    <a class="wf-logo" href="../../index.html">MARJAN</a>
    <nav class="wf-nav">
      <a href="future-developments.html" class="is-current">Development</a>
      <a href="../hospitality/hard-rock.html">Hospitality</a>
      <a href="../investment/overview.html">Investment</a>
      <a href="../news-media/latest-news.html">News &amp; Media</a>
      <a href="../careers/working-at-marjan.html">Careers</a>
      <a href="../resources/faqs.html">Resources</a>
      <a href="../legal/legal-notices.html">Legal</a>
    </nav>
    <a class="wf-header-cta" href="#enquire">Enquire</a>
  </div>
</header>

<nav class="wf-breadcrumb">
  <a href="../../index.html">Home</a><span class="sep">/</span>
  <a href="future-developments.html">Development</a><span class="sep">/</span>
  <span>Future Developments</span>
</nav>

<section class="wf-hero">
  <span class="wf-hero-tag">Development · Pipeline</span>
  <h1>Building What Comes Next for Ras Al Khaimah</h1>
  <p class="lead">A disciplined pipeline of master planned destinations, mixed-use districts and infrastructure programmes that will define the next decade of the emirate.</p>
  <div class="wf-cta-row">
    <a class="wf-cta" href="#pipeline">View the Pipeline</a>
    <a class="wf-cta wf-cta--light" href="../investment/overview.html">Investment Overview</a>
  </div>
  <div class="wf-hero-meta">
    <div class="item"><span>Active Programmes</span><strong>14</strong></div>
    <div class="item"><span>Masterplanned Land</span><strong>120M sq ft</strong></div>
    <div class="item"><span>Investment Pipeline</span><strong>US$13B+</strong></div>
    <div class="item"><span>Coastline Developed</span><strong>4.5 km</strong></div>
  </div>
</section>

<section class="wf-shell">
  <div class="wf-main">

    <section class="wf-block">
      <div class="wf-chapter"><span class="num">01</span><span class="rule"></span><span class="label">Philosophy</span></div>
      <h2>A Vision Grounded in Purpose</h2>
      <p class="large">Marjan's development philosophy reflects a clear, long-term vision for Ras Al Khaimah — one that balances sustainability, economic diversification and quality of life across every district we plan and deliver.</p>
      <div style="margin-top:48px;">
        <h4>Integrated, People-Centred Planning</h4>
        <p>Every community we build is shaped around how people will live today and how they will live tomorrow. Connectivity, accessibility and quality of life inform every planning decision, from land use to streetscape detail.</p>
        <h4 style="margin-top:32px;">Long-Term Value Creation</h4>
        <p>Our master planned developments are designed to create meaningful, sustained value for residents, investors, institutions and the businesses that choose to grow with Ras Al Khaimah.</p>
      </div>
    </section>

    <section id="pipeline" class="wf-block">
      <div class="wf-chapter"><span class="num">02</span><span class="rule"></span><span class="label">Pipeline</span></div>
      <h2>The Next Generation of Destinations</h2>
      <div class="wf-grid wf-grid--2" style="margin-top:48px;">
        <article class="wf-card">
          <div class="wf-img wf-img--sea wf-img--tall"><span class="wf-img-caption">Phase Next · <span class="frame-num">F.11</span></span></div>
          <h4>Al Marjan Island — Phase Next</h4>
          <p class="meta">2026 → 2030</p>
          <p>Extending the island's beachfront programme with the next wave of hospitality, branded residential and integrated entertainment product.</p>
          <a href="#">Detail Brief →</a>
        </article>
        <article class="wf-card">
          <div class="wf-img wf-img--dawn wf-img--tall"><span class="wf-img-caption">Beach District · <span class="frame-num">F.12</span></span></div>
          <h4>Marjan Beach District</h4>
          <p class="meta">In Planning</p>
          <p>A waterfront mixed-use community designed around a continuous public promenade, anchored by lifestyle retail and family-led F&amp;B.</p>
          <a href="#">Detail Brief →</a>
        </article>
        <article class="wf-card">
          <div class="wf-img wf-img--night wf-img--tall"><span class="wf-img-caption">RAK Central · <span class="frame-num">F.13</span></span></div>
          <h4>RAK Central</h4>
          <p class="meta">Phased Delivery</p>
          <p>A new commercial and civic core for the emirate, integrating government, business and residential anchors into a single connected district.</p>
          <a href="#">Detail Brief →</a>
        </article>
        <article class="wf-card">
          <div class="wf-img wf-img--mono wf-img--tall"><span class="wf-img-caption">Infrastructure · <span class="frame-num">F.14</span></span></div>
          <h4>Infrastructure Programmes</h4>
          <p class="meta">2026 → 2032</p>
          <p>The mobility, utilities and public realm investments that underpin every Marjan masterplan and connect them into a coherent regional fabric.</p>
          <a href="#">Detail Brief →</a>
        </article>
      </div>
    </section>

    <section class="wf-block">
      <div class="wf-chapter"><span class="num">03</span><span class="rule"></span><span class="label">Planning Methodology</span></div>
      <div class="wf-editorial wf-editorial--5-7">
        <div>
          <h2>Clarity in Land Use &amp; Zoning</h2>
        </div>
        <div>
          <p>Each masterplan begins with detailed, data-driven land analysis. Zoning is purposeful — calibrating residential density, hospitality capacity, commercial mix and public realm into an integrated whole.</p>
          <h4 style="margin-top:28px;">Connectivity at the Core</h4>
          <p>Transport links, mobility options and pedestrian networks are planned from the outset to ensure seamless movement within and between districts.</p>
          <h4 style="margin-top:28px;">Resilience and Future-Readiness</h4>
          <p>Every masterplan is designed with the future in mind. Flexibility is embedded into each design so districts can evolve with their populations and economies.</p>
        </div>
      </div>
    </section>

  </div>
</section>

<section class="wf-dark-section" id="enquire">
  <div class="wf-block">
    <div class="wf-chapter"><span class="num">04</span><span class="rule"></span><span class="label">Partnerships</span></div>
    <h2>Working With Us</h2>
    <p>From institutional capital partners to global operators and specialist consultants, Marjan's development pipeline is built through long-term partnerships. If your organisation is exploring Ras Al Khaimah, we'd like to hear from you.</p>
    <div class="wf-cta-row">
      <a class="wf-cta wf-cta--light" href="../investment/process.html">Investment Process</a>
      <a class="wf-cta wf-cta--ghost" style="color:var(--paper);border-color:var(--paper);" href="../hospitality/for-operators.html">For Operators</a>
    </div>
  </div>
</section>

<footer class="wf-footer">
  <div class="wf-footer-inner">
    <div>
      <div class="wf-footer-brand">Marjan — Master Developer of Ras Al Khaimah.</div>
      <p class="wf-footer-meta">Aligned with RAK Vision 2030. Designed for life, defining the future of the emirate.</p>
    </div>
    <div>
      <h5>Development</h5>
      <ul><li><a href="future-developments.html">Future Developments</a></li></ul>
    </div>
    <div>
      <h5>Hospitality</h5>
      <ul>
        <li><a href="../hospitality/hard-rock.html">Hard Rock</a></li>
        <li><a href="../hospitality/branded-residences.html">Branded Residences</a></li>
      </ul>
    </div>
    <div>
      <h5>Invest</h5>
      <ul>
        <li><a href="../investment/overview.html">Overview</a></li>
        <li><a href="../investment/process.html">Process</a></li>
      </ul>
    </div>
    <div>
      <h5>Resources</h5>
      <ul>
        <li><a href="../resources/faqs.html">FAQs</a></li>
        <li><a href="../legal/legal-notices.html">Legal Notices</a></li>
      </ul>
    </div>
  </div>
  <div class="wf-footer-bottom">
    <span>© 2026 Marjan LLC. All rights reserved.</span>
    <span>info@marjan.ae · +971 (7) 203 5000</span>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Verify.** Open `http://localhost:5500/pages/development/future-developments.html`. Hero, pipeline cards (4), methodology editorial, and dark partnerships band render cleanly.

- [ ] **Step 3: Commit anchor phase.**

```bash
git add index.html pages/hospitality/hard-rock.html pages/development/future-developments.html
git commit -m "html: rebuild index + hard-rock + future-developments to marjan brand"
```

---

## Task 7: Rebuild remaining Hospitality pages (3 files)

**Files:**
- Modify (full rewrite): `pages/hospitality/branded-residences.html`
- Modify (full rewrite): `pages/hospitality/for-operators.html`
- Modify (full rewrite): `pages/hospitality/market-insights.html`

**Pattern for all three:** Same header + breadcrumb + footer scaffold as Task 5/6. Each page uses: hero → 2-3 editorial blocks → portfolio grid OR stats strip → dark CTA → footer.

- [ ] **Step 1: Rewrite `branded-residences.html`.**

Hero copy:
- Tag: `Hospitality · Residences`
- H1: `Branded Residences for a New Era of Coastal Living`
- Lead: `From beachfront flagships to mountain retreats, branded residences across Marjan's portfolio bring world-class operator service into the home — and into one of the region's most exciting investment categories.`
- Meta items: Operators (8 global brands), Locations (Al Marjan Island, Al Wadi, RAK Central), Status (Mixed — Now Open / Under Development), Targeted Delivery (2025–2029).

Sections (3 chapters):
1. **Overview** — "The Branded Residence Proposition" — paragraph on operator service, design standards, hold value.
2. **Portfolio** — 4-card grid: Ritz Carlton Residences Al Wadi (Under Development), Wynn Residences Al Marjan Island (Coming 2027), Marjan Beach Residences (In Planning), Branded Residences — Phase Next (TBA). Use `wf-img--sea`, `wf-img--dawn`, `wf-img--cream`, `wf-img--night`.
3. **Why Ras Al Khaimah** — 3 stat cells: 12% projected residential capital growth ('25–'30), 4.5km developed coastline, 8 global hospitality brands present. Closing CTA pair: "Investment Case" → `../investment/residential.html`, "Speak to the Team" → `#enquire`.

Dark closing band: "A Category Built for the Long Term" + paragraph + CTA to `../investment/overview.html`.

Use the same header/breadcrumb/footer scaffold from Task 5.

- [ ] **Step 2: Rewrite `for-operators.html`.**

Hero:
- Tag: `Hospitality · For Operators`
- H1: `A Partner-Led Platform for World-Class Operators`
- Lead: `Marjan partners with global hotel, lifestyle and integrated resort operators across the full development lifecycle — from site selection and feasibility through construction, opening and ongoing asset stewardship.`
- Meta: Properties on platform (8+), Operator partners (Wynn, Ritz Carlton, Pullman, Movenpick, Hilton, Hard Rock, Rixos, Rove), Pipeline keys (4,500+), Asset under development (US$11B+).

Sections:
1. **Why Marjan** — three short blocks: Land bank & masterplan integration / Capital partners & investor pipeline / Operational backbone (utilities, mobility, public realm).
2. **The Operator Engagement Model** — 4-step vertical process (`wf-process-v`): Discovery & Fit / Commercial Structuring / Design & Pre-Opening / Operations & Asset Stewardship. Each step has 2-sentence body and an indicative timing.
3. **Partner Tier** — table (`wf-list`) with 8 operator rows: name | property | category | status.

Dark band: "Start the Conversation" with two CTAs (enquiry email + calendar).

- [ ] **Step 3: Rewrite `market-insights.html`.**

Hero:
- Tag: `Hospitality · Market Insights`
- H1: `Reading Ras Al Khaimah's Hospitality Growth Story`
- Lead: `A working view of the demand, supply, pricing and visitor trends shaping the Ras Al Khaimah hospitality market — published by Marjan's research team.`
- Meta: Visitor arrivals YoY (+27%), Average daily rate trend (+18%), New keys 2025–2027 (4,500+), Source mix (UK, Russia, India, GCC).

Sections:
1. **Macro Picture** — editorial split with 3 stat tiles (visitors, ADR, occupancy).
2. **Demand Composition** — 3-card grid: International leisure / Regional weekenders / MICE & events. Each card has stat + 2-sentence narrative.
3. **Outlook 2026–2030** — pull quote: "Ras Al Khaimah's hospitality pipeline is unmatched in the GCC outside the established Dubai cluster, with new keys outpacing peer destinations through the end of the decade." — `cite`: Marjan Hospitality Research · 2026.
4. **Reports** — `wf-files` grid with 4 downloadable briefs (filename + PDF · size · date).

Dark band: "Subscribe to the Brief" with email field + CTA.

- [ ] **Step 4: Verify all three.** Cycle through `http://localhost:5500/pages/hospitality/{branded-residences,for-operators,market-insights}.html` — same visual rhythm as Hard Rock, no console errors.

---

## Task 8: Rebuild Investment pages (7 files)

**Files:**
- Modify (full rewrite): `pages/investment/overview.html`
- Modify (full rewrite): `pages/investment/by-sector.html`
- Modify (full rewrite): `pages/investment/residential.html`
- Modify (full rewrite): `pages/investment/hospitality.html`
- Modify (full rewrite): `pages/investment/commercial.html`
- Modify (full rewrite): `pages/investment/staff-accommodation.html`
- Modify (full rewrite): `pages/investment/process.html`

- [ ] **Step 1: Rewrite `overview.html`.**

Hero — Tag: `Investment · Overview` — H1: `Investing in Ras Al Khaimah's Defining Decade` — Lead: `Marjan offers institutional, corporate and qualified private investors structured access to one of the most ambitious development programmes in the Middle East.` — Meta: Pipeline (US$13B+), Active sectors (4), Operating partners (8), Targeted delivery window (2025–2032).

Sections:
1. **The Investment Thesis** — large p + 3 sub-blocks (Economic alignment with RAK Vision 2030 / Diversified sector exposure / Long-term hold horizon).
2. **By Sector at a Glance** — 4-card grid linking to Residential / Hospitality / Commercial / Staff Accommodation.
3. **Stats strip** — 6 tiles (Pipeline value, Land bank, Coastline, Visitor growth, Hotel keys delivered, Hotel keys in pipeline).

Dark band: "Speak to Investor Relations" → CTAs to `process.html` + email.

- [ ] **Step 2: Rewrite `by-sector.html`.**

Hero — Tag: `Investment · By Sector` — H1: `Capital Strategies Across Marjan's Sectors` — Lead: `Each of Marjan's four sectors carries a distinct risk-return profile, capital structure and partnership model. Read the dedicated sector briefs below.`

Body: 4 large editorial cards (one per sector) with: sector name (h3 Montserrat), 2-sentence positioning, 3 bullet KPIs (e.g. "Asset class: Branded residential, beachfront / Indicative hold: 7–10 years / Co-investment threshold: US$25M+"), CTA to sector page.

Use `wf-editorial` blocks alternating left/right.

- [ ] **Step 3: Rewrite `residential.html`.**

Hero — Tag: `Investment · Residential` — H1: `Long-Term Value in Coastal Residential` — Lead: `Branded residences, beachfront apartments and integrated community housing across one of the GCC's fastest-appreciating coastal markets.`

Sections:
1. **The Case** — large p + 3 sub-blocks (Demand drivers / Supply discipline / Operator-backed yields).
2. **Active Products** — 3-card portfolio grid (Ritz Carlton Residences Al Wadi / Wynn Residences / Marjan Beach Residences).
3. **Investor Metrics** — 4 stats (Indicative gross yield, Price growth ('25–'30), Hold horizon, Currency exposure).
4. **Documents** — `wf-files` with 3 sector briefs.

Dark closing: "Co-Investment Inquiries" + CTAs.

- [ ] **Step 4: Rewrite `hospitality.html`.**

Hero — Tag: `Investment · Hospitality` — H1: `Hospitality Investment in a Globally Ascendant Destination` — Lead: `Marjan's hospitality investment programme spans landmark integrated resorts, branded city hotels and nature-led retreats — anchored by the operator partnerships reshaping the emirate's tourism economy.`

Sections mirror residential.html structure:
1. The Case (3 sub-blocks: Visitor growth / Operator pipeline / Land bank availability).
2. Active Programmes — 3-card grid (Wynn / Hard Rock / Pullman Beach).
3. Stats — 4 (ADR trend, Occupancy outlook, Keys in pipeline, Pipeline value).
4. Documents — `wf-files` with 3 briefs.

Dark band: CTAs to `../hospitality/for-operators.html` + `process.html`.

- [ ] **Step 5: Rewrite `commercial.html`.**

Hero — Tag: `Investment · Commercial` — H1: `Commercial Real Estate at RAK's Inflection Point` — Lead: `Office, retail and mixed-use product across RAK Central and the wider Marjan portfolio — designed for the next decade of corporate, civic and lifestyle activity in the emirate.`

Same 4-section pattern.

- [ ] **Step 6: Rewrite `staff-accommodation.html`.**

Hero — Tag: `Investment · Staff Accommodation` — H1: `Purpose-Built Workforce Housing at Scale` — Lead: `As Ras Al Khaimah's hospitality, construction and operations workforce grows, Marjan delivers compliant, well-located, well-amenitised staff accommodation as a discrete investment category.`

Same 4-section pattern, adjusted KPIs (Bed count pipeline, Operator demand, Yield range, Hold horizon).

- [ ] **Step 7: Rewrite `process.html`.**

Hero — Tag: `Investment · Process` — H1: `A Clear, Disciplined Path from Inquiry to Handover` — Lead: `A four-stage process refined across Marjan's institutional investor base — predictable, transparent, and built around long-term partnership.`

Body: `wf-process-v` with 4 steps:
1. **Discovery & Mandate Fit** — 2-sentence body — timing "Weeks 1–2".
2. **Diligence & Structuring** — 2-sentence body — timing "Weeks 3–8".
3. **Commitment & Documentation** — 2-sentence body — timing "Weeks 9–14".
4. **Deployment & Handover** — 2-sentence body — timing "Quarter following close".

Then `wf-note`: callout on bespoke structures for institutional capital.

Dark band: CTAs to email + book a call.

- [ ] **Step 8: Verify all seven.** Cycle through each URL under `http://localhost:5500/pages/investment/` and check rendering.

---

## Task 9: Rebuild News & Media pages (4 files)

**Files:**
- Modify (full rewrite): `pages/news-media/latest-news.html`
- Modify (full rewrite): `pages/news-media/media-centre.html`
- Modify (full rewrite): `pages/news-media/publications.html`
- Modify (full rewrite): `pages/news-media/in-the-media.html`

- [ ] **Step 1: Rewrite `latest-news.html`.**

Hero (compact: `wf-hero--compact`) — Tag: `News & Media · Latest` — H1: `Marjan in the News` — Lead: `Press releases and official statements from Marjan, Master Developer of Ras Al Khaimah.`

Body:
1. **Featured story** — `wf-feature` with one lead release (date, category meta, headline, 2-sentence dek, "Read the Release →").
2. **Toolbar** — `wf-toolbar` with chips (All / Hospitality / Investment / Development / Sustainability / Leadership) and a count.
3. **News rows** — 8 entries of `wf-news-row` with date / category meta / headline / 1-sentence dek / `arrow`.

Dark band: "Subscribe to Press Releases" + email field.

- [ ] **Step 2: Rewrite `media-centre.html`.**

Hero (compact) — Tag: `News & Media · Media Centre` — H1: `A Working Resource for the Press` — Lead: `Logos, fact sheets, image library access and interview-request contact for journalists covering Ras Al Khaimah's development story.`

Body:
1. **Quick links grid** — `wf-grid wf-grid--3` of `wf-card`: Logo & brand kit / Fact sheets / Image library / Spokesperson directory / Interview requests / Subscribe to press.
2. **Recent coverage** — `wf-news-row` x 4.

Closing dark band: "Press Office Contact" with email + phone.

- [ ] **Step 3: Rewrite `publications.html`.**

Hero (compact) — Tag: `News & Media · Publications` — H1: `Reports, Reviews, Briefings` — Lead: `Marjan's published view of Ras Al Khaimah's economy, hospitality market, sustainability programme and development pipeline.`

Body:
1. **Featured publication** — `wf-feature` (Annual Review 2025).
2. **All publications** — `wf-files` grid of 8 documents (filename + PDF · size · date).

- [ ] **Step 4: Rewrite `in-the-media.html`.**

Hero (compact) — Tag: `News & Media · In the Media` — H1: `Marjan, As Seen Elsewhere` — Lead: `External coverage of Marjan's projects, leadership and the wider Ras Al Khaimah story.`

Body:
1. **Toolbar** — `wf-chips`: All / Hospitality / Investment / Sustainability / Leadership; outlet filter.
2. **Coverage list** — 12 `wf-news-row` entries with outlet (in meta), date, headline, dek, external link arrow.

- [ ] **Step 5: Verify all four.** Cycle through each URL.

---

## Task 10: Rebuild Careers pages (3 files)

**Files:**
- Modify (full rewrite): `pages/careers/working-at-marjan.html`
- Modify (full rewrite): `pages/careers/current-openings.html`
- Modify (full rewrite): `pages/careers/life-at-marjan.html`

- [ ] **Step 1: Rewrite `working-at-marjan.html`.**

Hero — Tag: `Careers · Working at Marjan` — H1: `Working at Marjan — Building the Emirate's Next Chapter` — Lead: `Join the team delivering the master planned destinations, hospitality programmes and infrastructure shaping Ras Al Khaimah for the next decade.`

Sections:
1. **What We Do** — editorial split with photo placeholder.
2. **How We Work** — 4 sub-blocks of values (Ambition, Discipline, Ownership, Stewardship).
3. **Career Tracks** — `wf-grid wf-grid--3` cards: Development & Planning / Hospitality & Operations / Investment & Capital / Corporate Functions.
4. **CTA strip** — `wf-cta` to `current-openings.html`.

- [ ] **Step 2: Rewrite `current-openings.html`.**

Hero (compact) — Tag: `Careers · Openings` — H1: `Current Openings` — Lead: `Live roles across Marjan's development, hospitality, investment and corporate teams.`

Body:
1. **Toolbar** — `wf-toolbar` with chips (Function / Location / Type) + count.
2. **Job rows** — `wf-jobs` with 8 `wf-job` entries: num / role+desc / function pill / location pill / type pill / Apply CTA.

Dark band: "Submit Open Application" with link to email.

- [ ] **Step 3: Rewrite `life-at-marjan.html`.**

Hero — Tag: `Careers · Life at Marjan` — H1: `Life at Marjan` — Lead: `An honest look at the people, the place and the pace of work at one of the region's most ambitious master developers.`

Body: `wf-essay` with 4 alternating `wf-essay-row` blocks:
1. (image-left, text-right) — "Working on a place still being built"
2. (text-left, image-right) — "A small team, an outsized brief"
3. (image-left, text-right) — "Living in Ras Al Khaimah"
4. (text-left, image-right) — "Wellbeing, belonging, growth"

Each row has h3, 2 paragraphs, and a `by` line.

Dark band closing: CTA to `current-openings.html`.

- [ ] **Step 4: Verify all three.**

- [ ] **Step 5: Commit bulk phase.**

```bash
git add pages/hospitality/branded-residences.html \
        pages/hospitality/for-operators.html \
        pages/hospitality/market-insights.html \
        pages/investment/overview.html \
        pages/investment/by-sector.html \
        pages/investment/residential.html \
        pages/investment/hospitality.html \
        pages/investment/commercial.html \
        pages/investment/staff-accommodation.html \
        pages/investment/process.html \
        pages/news-media/latest-news.html \
        pages/news-media/media-centre.html \
        pages/news-media/publications.html \
        pages/news-media/in-the-media.html \
        pages/careers/working-at-marjan.html \
        pages/careers/current-openings.html \
        pages/careers/life-at-marjan.html
git commit -m "html: rebuild hospitality (3), investment (7), news (4), careers (3) to marjan brand"
```

---

## Task 11: Rebuild Resources pages (4 files)

**Files:**
- Modify (full rewrite): `pages/resources/downloads.html`
- Modify (full rewrite): `pages/resources/faqs.html`
- Modify (full rewrite): `pages/resources/glossary.html`
- Modify (full rewrite): `pages/resources/investment-calculator.html`

- [ ] **Step 1: Rewrite `downloads.html`.**

Hero (compact) — Tag: `Resources · Downloads` — H1: `Documents, Brochures, Specifications` — Lead: `Brochures, fact sheets, investment briefs and technical specifications across Marjan's portfolio.`

Body:
1. `wf-toolbar` with category chips (All / Hospitality / Investment / Development / Sustainability / Press).
2. `wf-cat-head` + `wf-files` grid for each of the 5 categories (3–4 files per category — total ~18 files).

- [ ] **Step 2: Rewrite `faqs.html`.**

Hero (compact) — Tag: `Resources · FAQs` — H1: `Frequently Asked` — Lead: `Common questions about Marjan's developments, investment process, hospitality partnerships and Ras Al Khaimah.`

Body: 3 `wf-cat-head` sections — Investment / Development / Working with Marjan — each followed by `wf-accordion` with 4–6 `details` items per section.

- [ ] **Step 3: Rewrite `glossary.html`.**

Hero (compact) — Tag: `Resources · Glossary` — H1: `Glossary of Terms` — Lead: `Plain definitions for the development, hospitality and investment terms that recur across Marjan's documentation.`

Body:
1. `wf-az-nav` with A–Z chips (some marked `is-empty` where no terms exist).
2. `wf-glossary` with 6 `letter-block` sections (A, C, H, M, R, S — pick representative letters). Each block has 3–5 terms in `dl` / `dt` / `dd`. Include `tag` chips like INVESTMENT, HOSPITALITY, DEVELOPMENT on relevant entries.

Example entries: ADR (HOSPITALITY), Capex (INVESTMENT), Hold horizon (INVESTMENT), Masterplan (DEVELOPMENT), RevPAR (HOSPITALITY), Stewardship (CORPORATE).

- [ ] **Step 4: Rewrite `investment-calculator.html`.**

Hero (compact) — Tag: `Resources · Calculator` — H1: `Modelling Your Investment` — Lead: `An indicative tool for sizing returns across Marjan's investment categories. For illustrative purposes only — not investment advice.`

Body: `wf-tool` split:
- **Left (sticky inputs `wf-tool-inputs`)** — 6 fields (Asset class, Capital commitment, Hold horizon, Currency, Leverage, Operator structure) — each as `field` with label + `val` value (static for wireframe).
- **Right (`wf-tool-outputs`)** — h3 + `wf-result-grid` with 4 result cells (Projected gross yield, Net yield post-fees, Total return, IRR). Then a `wf-note` with regulatory disclaimer below.

Dark band: "Validate Your Scenario with Investor Relations" CTA.

- [ ] **Step 5: Verify all four.**

---

## Task 12: Rebuild Legal pages (4 files)

**Files:**
- Modify (full rewrite): `pages/legal/legal-notices.html`
- Modify (full rewrite): `pages/legal/regulatory.html`
- Modify (full rewrite): `pages/legal/anti-corruption.html`
- Modify (full rewrite): `pages/legal/data-protection.html`

**Pattern (all four):** Hero (compact) → `wf-doc-meta` strip (Effective / Last reviewed / Jurisdiction / Document ref) → `wf-doc` layout with `wf-doc-body` (multiple `article` blocks) + sticky `wf-toc` listing each article.

Voice is formal — match UAE corporate norms. No marketing voice on these pages.

- [ ] **Step 1: Rewrite `legal-notices.html`.**

Hero — Tag: `Legal · Notices` — H1: `Legal Notices` — Lead: `Important legal information regarding the use of this site, intellectual property, and Marjan's published materials.`

`wf-doc-meta`: Effective Date / Last Reviewed / Jurisdiction (Ras Al Khaimah, UAE) / Document Ref (MJN-LEG-001).

`wf-doc-body` with 6 articles:
1. Acceptance of Terms
2. Intellectual Property
3. Use of Site Content
4. Disclaimer & Limitation of Liability
5. Third-Party Links
6. Governing Law & Jurisdiction

Each article: `article-num` (Article 01..06), h2, 2–3 paragraphs of formal legal language.

Sticky `wf-toc` with same numbering.

- [ ] **Step 2: Rewrite `regulatory.html`.**

Hero — Tag: `Legal · Regulatory` — H1: `Regulatory Information` — Lead: `Details of the regulatory frameworks under which Marjan operates and the entities responsible for oversight of its developments.`

`wf-doc-meta`: Effective Date / Last Reviewed / Regulator / Document Ref.

5 articles: Entity & Registration / Regulatory Bodies / Compliance Programme / Reporting Obligations / Investor Disclosures.

- [ ] **Step 3: Rewrite `anti-corruption.html`.**

Hero — Tag: `Legal · Policy` — H1: `Anti-Corruption Policy` — Lead: `Marjan's commitment to operating with integrity, in line with UAE federal law and international anti-corruption standards.`

`wf-doc-meta`: Effective Date / Last Reviewed / Policy Owner / Document Ref.

7 articles: Purpose & Scope / Prohibited Conduct / Gifts & Hospitality / Facilitation Payments / Third-Party Diligence / Reporting & Whistleblowing / Sanctions for Breach.

- [ ] **Step 4: Rewrite `data-protection.html`.**

Hero — Tag: `Legal · Policy` — H1: `Data Protection` — Lead: `How Marjan collects, uses, stores and protects personal data, in line with UAE data protection law.`

`wf-doc-meta`: Effective Date / Last Reviewed / DPO Contact / Document Ref.

8 articles: Scope / Data We Collect / Legal Basis / How We Use Data / Retention / Your Rights / International Transfers / Contacting the DPO.

- [ ] **Step 5: Verify all four.** Open each `http://localhost:5500/pages/legal/*` URL. TOC sticks, articles read formally, no marketing voice.

- [ ] **Step 6: Commit utility phase.**

```bash
git add pages/resources/downloads.html \
        pages/resources/faqs.html \
        pages/resources/glossary.html \
        pages/resources/investment-calculator.html \
        pages/legal/legal-notices.html \
        pages/legal/regulatory.html \
        pages/legal/anti-corruption.html \
        pages/legal/data-protection.html
git commit -m "html: rebuild resources (4) and legal (4) pages to marjan brand"
```

---

## Task 13: Final pass — visual QA and definition of done

**Files:**
- Read (no edits expected): all 28 HTML files + `styles/wireframe.css`

- [ ] **Step 1: Cycle every URL.** Start at `http://localhost:5500/` and click through every link from the sitemap navigator and each page's nav/footer. Note any broken link or visible regression in a scratchpad.

- [ ] **Step 2: Grep for leftover artifacts.**

Run:

```bash
cd "/mnt/d/Code Files/al-marjan"
grep -rn --include="*.html" --include="*.css" -E "Fraunces|Manrope|cream|bronze|sand|--bronze|--cream|--sand|--font-display: 'Fraunces|wireframe · structural|mid-fidelity|low-fi|Hard Rock \(pipeline\)" . | grep -v -E "^./(docs|node_modules|\.claude|\.git)/"
```

Expected: zero matches. Anything that returns is a leftover from the old design language — fix and re-grep.

- [ ] **Step 3: Grep for required brand markers.**

```bash
grep -rn --include="*.html" "Master Developer of Ras Al Khaimah" . | grep -v -E "^./(docs|node_modules|\.claude|\.git)/" | wc -l
```

Expected: ≥ 28 (the footer brand line appears on every page).

- [ ] **Step 4: Console check.** Open DevTools on three random pages, confirm no 404s or CSS errors.

- [ ] **Step 5: Update memory.** Update the Al Marjan design preferences memory file to reflect the new state — the Hard Rock page is no longer the design reference; the whole site is now under the marjan.ae brand. Don't write the memory file in this plan — handle in the conversation after execution completes.

- [ ] **Step 6: Final summary commit (optional).**

If any fixes came up during Step 1–3, commit them with a clear message. Otherwise no commit needed.

---

## Self-Review

**1. Spec coverage:** Walked through each spec section.
- §1 brand foundations → Task 1 covers tokens + base, Task 4 (index) & Task 5 (hard-rock) prove voice/visual together.
- §1.4 image treatment → Task 2 step 3 covers gradient variants.
- §2 voice rules + per-page table → Tasks 4–12 cover all 28 pages with H1s matching the spec table.
- §3 component patterns → Task 1 (header/footer/shell), Task 2 (hero/editorial/stats/cards/CTAs/dark/related), Task 3 (specialist patterns + index + responsive).
- §4 implementation order → exact phase boundaries with commits at Task 3, Task 6, Task 10, Task 12.
- §5 out of scope → no JavaScript, no real photos, no IA changes — confirmed throughout.
- §6 definition of done → Task 13 verification grep + cycle.

**2. Placeholder scan:** Every "rewrite page X" task lists explicit hero copy, sections, and patterns to use. Where copy is extrapolated (e.g. investment sectors), I gave specific section structure and stat categories, not "fill in".

**3. Type consistency:** All selectors used in HTML tasks match selectors defined in CSS tasks (`.wf-hero`, `.wf-hero-tag`, `.wf-hero-meta`, `.wf-block`, `.wf-chapter`, `.wf-cta`, `.wf-stat .num`, `.wf-process-v`, `.wf-tool`, `.wf-doc`, `.wf-toc`, `.wf-accordion`, `.wf-az-nav`, `.wf-glossary`, `.wf-files`, `.wf-jobs`, `.wf-essay`, `.wf-feature`, `.wf-news-row`, `.wf-toolbar`, `.wf-cat-head`, `.wf-doc-meta`). Token names consistent throughout (`--ink`, `--ink-deep`, `--navy`, `--navy-soft`, `--mist`, `--paper`, `--surface`, `--surface-2`, `--line`, `--line-soft`, `--muted`, `--text`, `--font-display`, `--font-sans`).

**4. Known soft spots:** Tasks 7–12 abbreviate the HTML content (give structure + copy directives rather than full HTML per page) — this is deliberate, since spelling out 25 full pages would balloon the plan. The pattern is fully demonstrated in Tasks 4–6; later tasks reuse it. An executor working from this plan should be comfortable extrapolating once the anchor pages are built.
