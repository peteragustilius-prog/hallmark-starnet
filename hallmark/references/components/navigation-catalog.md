# Hallmark navigation reference catalog

This is a lossless concatenation of the original individual Hallmark component reference files; refer to the heading for the selected archetype.


---

<a id="original-n1-wordmark-2-links"></a>

## Original reference: `n1-wordmark-2-links.md`


### N1 · Wordmark + 2 links
Top-of-page bar: wordmark on the left, two text links on the right ("Pricing" / "Sign in"). No logo image, no menu icon.
*Use when:* the page has very few destinations.
*Don't confuse with:* N3 Side-rail (which is vertical).

```html
<nav class="nav-min">
  <a class="wordmark">Studio</a>
  <ul><li><a>Pricing</a></li><li><a>Sign in</a></li></ul>
</nav>
```


---

<a id="original-n10-floating-on-scroll-morph"></a>

## Original reference: `n10-floating-on-scroll-morph.md`

### N10 · Floating-on-scroll morph
A sticky bar at the top that **morphs into a floating pill** as the user scrolls past a threshold. Two visual modes share one DOM — `.nav` (outer) owns the bar look, `.nav__inner` (inner) owns the pill look. Cross-faded on a single class toggle (`.is-floating`) with one timing curve. Active layer feels seamless; AI defaults always botch this.
*Use when:* atmospheric / modern-minimal pages where the kinetic micro-moment earns its place. Adds a single tasteful surprise; resists novelty.
*Don't confuse with:* N5 Floating pill (always-on, no scroll behaviour). N10 is N5 plus a default-bar state that morphs *into* it.

```html
<header class="nav">
  <div class="nav__inner">
    <a class="wordmark">Hallmark</a>
    <ul class="nav__links">…</ul>
  </div>
</header>
```

The full recipe — the four laws (height-constant, transform-for-offset, cross-fade-everything, single-curve), the property-morph table, the scroll-handler script, and the eight anti-patterns Hallmark refuses — lives in [`floating-nav.md`](../floating-nav.md). Reach for that file *before* building this archetype. Skipping the four laws is what makes 90% of attempts read as broken.

*Anti-pattern (one of eight in floating-nav.md):* swapping two `<header>` elements via opacity instead of cross-fading one DOM. Doubles markup, fights focus order, desyncs content.

---


---

<a id="original-n11-mega-menu"></a>

## Original reference: `n11-mega-menu.md`

### N11 · Mega-menu panel
A standard top bar whose triggers open a **full-width multi-column panel** — icon · title · description per item, grouped under column headers, often with a promoted feature card on one side. The page dims behind a scrim. Vercel "Products", Figma "Products", Notion "Resources".
*Use when:* the brand has many destinations that need grouping + explanation (a platform with 6+ products, or docs/resources hubs). The payload is the design problem, not the bar.
*Don't confuse with:* N1b (small single-column dropdowns); N1a (no dropdowns at all).

```html
<header class="nav">
  <div class="nav__inner">
    <a class="nav__brand">Northwind</a>
    <nav class="nav__center">
      <div class="mega" data-mega="products"><button class="nav__link" aria-controls="mega-products" aria-expanded="false">Products <span class="nav__caret"></span></button></div>
    </nav>
    <div class="nav__right"><a class="btn btn--accent">Get started</a></div>
  </div>
  <div class="mega-panel" id="mega-products" data-panel="products">
    <div class="mega-panel__inner">
      <div class="mega-col"><p class="mega-col__head">Move money</p><a class="mega-link"><span class="mega-link__ico"></span><span><b>Payments</b><i>cards, ACH, wires</i></span></a></div>
      <a class="mega-feature"><p class="mega-feature__title">Vault</p><p class="mega-feature__desc">stablecoin settlement</p></a>
    </div>
  </div>
</header>
<div class="nav-scrim" id="scrim"></div>
```
```css
.mega-panel { position: absolute; top: 100%; left: 0; right: 0; opacity: 0; visibility: hidden; transform: translateY(-10px);
  background: color-mix(in oklch, var(--color-paper) 96%, transparent); backdrop-filter: blur(20px) saturate(160%);
  border-bottom: 1px solid var(--color-rule); box-shadow: 0 30px 60px -28px oklch(0% 0 0 / 0.35);
  transition: opacity 240ms, transform 280ms var(--ease-spring), visibility 240ms; }
.mega-panel.is-open { opacity: 1; visibility: visible; transform: none; }
.mega-panel__inner { max-width: var(--page-max); margin: 0 auto; padding: 2rem var(--page-gutter);
  display: grid; grid-template-columns: repeat(3, 1fr) 1.1fr; gap: 2rem; }
.nav-scrim { position: fixed; inset: 0; z-index: 400; background: oklch(18% 0.01 250 / 0.28); backdrop-filter: blur(2px);
  opacity: 0; visibility: hidden; transition: opacity 260ms, visibility 260ms; }
.nav-scrim.is-active { opacity: 1; visibility: visible; }
```
*JS:* hover opens (with a ~140ms close-grace timer so the pointer can travel into the panel), click toggles, Esc closes, only one panel open at a time, scrim + `aria-expanded` follow state.

**Knobs** — *Columns:* 2 · 3 · 4 · *Feature cell:* none · promo card · code sample · *Scrim:* dim+blur (default) · dim only · none · *Open on:* hover+click (default) · click only.
*Anti-pattern:* never more than ~4 columns; never a panel taller than ~60vh; never open on hover with no close-grace timer (the menu flickers when the pointer crosses the gap). Items must carry a one-line description — a bare link grid is just N1b in disguise.
*Mobile:* collapse the whole thing to a drawer; the columns stack as accordion groups.


---

<a id="original-n12-banner-retract"></a>

## Original reference: `n12-banner-retract.md`

### N12 · Announcement banner + retracting nav
A coloured promo **banner** stacked above one real nav. On scroll-down the banner slides up and retracts, leaving a single clean nav docked to the top; on scroll-up it slides back. A dismiss × removes the banner for good (its height zeroes so no gap is left). Apple-style coupled bars, but the top tier is a *banner*, not a second nav — the colour contrast is what stops it reading as "two navs".
*Use when:* there's a genuine, time-bound announcement (a launch, a sale, free shipping) worth a persistent strip, over a product/marketing page. Great for stat-led or commerce pages.
*Don't confuse with:* a static announcement bar that never moves (fine, but not N12); N1b (single bar, no banner).

```html
<header class="nav" id="nav">
  <div class="nav__banner" id="banner">
    <p class="nav__banner-text"><span class="nav__banner-spark"></span> New — <b>shared habits</b>. <a class="nav__banner-link">Try it →</a></p>
    <button class="nav__banner-x" id="banner-x" aria-label="Dismiss"><span></span></button>
  </div>
  <div class="nav__bar"><div class="nav__bar-inner">
    <a class="nav__brand">Tally</a>
    <nav class="nav__links">…</nav>
    <a class="btn btn--accent">Start</a>
  </div></div>
</header>
```
```css
:root { --banner-h: 42px; --bar-h: 64px; }
.nav { position: fixed; inset: 0 0 auto; z-index: 500; transform: translateY(0); transition: transform 320ms var(--ease-out); }
.nav.is-compact   { transform: translateY(calc(var(--banner-h) * -1)); }  /* banner hides, bar docks to top */
.nav.is-dismissed { transform: none; }
.nav.is-dismissed .nav__banner { display: none; }
.nav__banner { height: var(--banner-h); display: flex; align-items: center; justify-content: center;
  background: linear-gradient(100deg, var(--color-accent), var(--color-accent-deep)); color: var(--color-paper); }
/* content clears both at rest; zero --banner-h on dismiss so calc() reflows with no gap */
.demo-hero { padding-top: calc(var(--banner-h) + var(--bar-h) + 4rem); }
```
*JS:* track scroll direction — past ~48px going down → `.is-compact`; going up → remove it; near top → always show. Dismiss × sets `--banner-h: 0px` (via `documentElement.style`) and adds `.is-dismissed`.

**Knobs** — *Banner fill:* solid accent · gradient (default) · tint+ink · *Dismiss:* yes (default) · none · *Bar scroll:* sticky (default) · also-frosts · *Banner content:* promo · status · countdown.
*Anti-pattern:* never make the top tier a second set of nav links — that's the "two nav bars" smell the banner exists to avoid. Keep the banner one line, one link, one dismiss. Don't animate banner height directly (janky); translate the whole `.nav` and zero the height only on dismiss.
*Mobile:* banner text truncates / drops the leading glyph; nav links collapse; the Buy/primary CTA stays.


---

<a id="original-n13-inline-cmdk-pill"></a>

## Original reference: `n13-inline-cmdk-pill.md`

### N13 · Inline ⌘K search pill
A **visible** search pill sits inline in the bar — placeholder text plus a `⌘K` kbd hint — alongside (not replacing) the links. Click it, or press ⌘K / Ctrl K, to open a spotlight modal with grouped, keyboard-navigable results. The opposite of N4 (which *hides* nav behind the shortcut): here the affordance is on the surface for newcomers, with the shortcut for power users. Tailwind, Linear, Raycast, docs sites.
*Use when:* the product is search-heavy or docs-heavy and search is a primary action (dev tools, music/library apps, large content sites).
*Don't confuse with:* N4 (no visible nav, ⌘K only); a plain search icon that just focuses an input in place.

```html
<header class="nav" id="nav"><div class="nav__inner">
  <a class="nav__brand">Crank</a>
  <button class="searchpill" id="searchpill" aria-label="Search (⌘K)">
    <span class="searchpill__ico"></span><span class="searchpill__text">Search docs…</span>
    <span class="searchpill__kbd"><kbd>⌘</kbd><kbd>K</kbd></span>
  </button>
  <nav class="nav__right"><a class="nav__link">Docs</a><a class="btn btn--accent">Start</a></nav>
</div></header>
<div class="cmdk" id="cmdk" aria-hidden="true">
  <div class="cmdk__backdrop" data-close></div>
  <div class="cmdk__panel" role="dialog" aria-modal="true">
    <div class="cmdk__field"><span class="cmdk__field-ico"></span><input id="cmdk-input" placeholder="Search docs…"><kbd>esc</kbd></div>
    <div class="cmdk__results"><p class="cmdk__group">Suggested</p><button class="cmdk__item is-active">…</button></div>
    <div class="cmdk__foot"><span><kbd>↑</kbd><kbd>↓</kbd> navigate</span><span><kbd>↵</kbd> open</span><span><kbd>esc</kbd> close</span></div>
  </div>
</div>
```
```css
.searchpill { display: flex; align-items: center; gap: 0.6rem; height: 40px; padding: 0 0.55rem 0 0.85rem;
  background: var(--color-paper-2); border: 1px solid var(--color-rule); border-radius: 999px; color: var(--color-muted);
  transition: border-color 200ms, box-shadow 200ms; }
.searchpill:hover { border-color: var(--color-rule-2); box-shadow: 0 4px 16px -10px oklch(0% 0 0 / 0.3); }
.cmdk { position: fixed; inset: 0; z-index: 700; opacity: 0; visibility: hidden; transition: opacity 200ms, visibility 200ms; }
.cmdk.is-open { opacity: 1; visibility: visible; }
.cmdk__panel { position: absolute; top: 14vh; left: 50%; transform: translateX(-50%) translateY(-8px) scale(0.98);
  width: min(560px, calc(100vw - 2rem)); transition: transform 240ms var(--ease-spring); }
.cmdk.is-open .cmdk__panel { transform: translateX(-50%) translateY(0) scale(1); }
```
*JS:* ⌘K / Ctrl K toggles, Esc closes, backdrop-click closes, ↑/↓ move the active item, Enter selects, focus the input on open and lock body scroll.

**Knobs** — *Pill placement:* centred (default) · right-of-brand · *Result groups:* flat · grouped (default) · *Footer hints:* shown (default) · hidden · *Open trigger:* pill+⌘K (default) · ⌘K only (→ that's N4, not N13).
*Anti-pattern:* don't fake the modal with a `<div>` that traps no focus and ignores Esc — if you ship the pill you ship the keyboard model. The pill must look like search (icon + placeholder), not a generic button.
*Mobile:* the pill collapses to a search icon; the modal goes full-height sheet.


---

<a id="original-n1b-saas-three-section"></a>

## Original reference: `n1b-saas-three-section.md`

### N1b · Canonical SaaS three-section
Wordmark hard-left · a centred cluster of 4–6 links (some opening hover dropdowns) · a sign-in text link + filled CTA hard-right. The dominant marketing-nav of 2024–26 (Stripe, Linear, Vercel, Figma, Notion, PostHog). The structural opposite of N1's *minimal* two-link variant — this one is dense and balanced.
*Use when:* a SaaS / product / dev-tool page with several real destinations and a clear primary action. The default reach for modern-minimal and (Hum-styled) playful product pages.
*Don't confuse with:* N1a (wordmark + 2 links, no centre cluster); N5 (detached pill); N11 (mega-menu panels, not small dropdowns).

```html
<header class="nav"><div class="nav__inner">
  <a class="nav__brand">Conduit</a>
  <nav class="nav__center">
    <div class="nav__item nav__item--menu">
      <button class="nav__link" aria-expanded="false">Product <span class="nav__caret"></span></button>
      <div class="nav__dropdown"><a class="nav__dropitem"><b>Gateway</b><i>one endpoint</i></a></div>
    </div>
    <a class="nav__link">Docs</a><a class="nav__link">Pricing</a>
  </nav>
  <div class="nav__right"><a class="btn btn--text">Sign in</a><a class="btn btn--accent">Start</a></div>
</div></header>
```
```css
.nav { position: fixed; inset: 0 0 auto; z-index: 500; background: transparent; border-bottom: 1px solid transparent;
  transition: background 240ms, border-color 240ms, box-shadow 240ms; }
.nav.is-scrolled { background: color-mix(in oklch, var(--color-paper) 72%, transparent);
  backdrop-filter: blur(18px) saturate(160%); border-bottom-color: var(--color-rule); box-shadow: 0 8px 28px -18px oklch(0% 0 0 / 0.4); }
.nav__inner { max-width: var(--page-max); margin: 0 auto; padding-inline: var(--page-gutter); height: 64px;
  display: grid; grid-template-columns: 1fr auto 1fr; align-items: center; }
.nav__brand { justify-self: start; } .nav__center { justify-self: center; display: flex; gap: 0.35rem; } .nav__right { justify-self: end; }
.nav__dropdown { position: absolute; opacity: 0; visibility: hidden; transform: translateY(-6px) scale(0.98);
  transition: opacity 200ms, transform 220ms var(--ease-spring), visibility 200ms; }
.nav__item--menu:hover .nav__dropdown, .nav__item--menu:focus-within .nav__dropdown { opacity: 1; visibility: visible; transform: none; }
```

**Knobs** — *Centre links:* 3 · 4 · 5–6 · *Dropdowns:* none · 1 · 2 · *Scroll state:* frost-on-scroll (default) · always-solid · transparent-fixed · *CTA pair:* sign-in + fill · fill only.
*Scroll behaviour (default):* transparent at rest over the hero, frosts (blur backdrop + hairline border + soft shadow) past ~24px, and tightens height ~8px. Always rAF-throttle the scroll handler.
*Anti-pattern:* don't let the centre cluster collide with brand/CTA — if it can't sit centred with breathing room, drop to 3 links or route to N1a. Never ship a dropdown that opens on click only with no hover/focus affordance.
*Mobile:* hide `.nav__center` below ~900px; brand + CTA (or hamburger) remain.


---

<a id="original-n2-floating-chip"></a>

## Original reference: `n2-floating-chip.md`

### N2 · Floating chip
A small fixed chip in a corner — wordmark + a single action ("Try it"). Doesn't sit in document flow.
*Use when:* the page is fold-heavy and traditional nav would fight the content.
*Don't confuse with:* C4 Sticky bottom bar (which is full-width).

```html
<aside class="nav-chip">
  <a class="wordmark">Studio</a>
  <a class="cta-outline">Try →</a>
</aside>
```
```css
.nav-chip { position: fixed; top: var(--space-md); right: var(--space-md); display: inline-flex; gap: var(--space-md); padding: 0.5rem 0.75rem; background: var(--color-paper); border: 1px solid var(--color-rule); }
```


---

<a id="original-n3-side-rail"></a>

## Original reference: `n3-side-rail.md`

### N3 · Side-rail
A thin vertical strip on the left edge — wordmark rotated, plus 2–3 dot-indicators for sections. Editorial / portfolio energy.
*Use when:* the page is long and section-numbered.
*Don't confuse with:* N1 Top wordmark (which is horizontal).

```html
<nav class="nav-rail">
  <p class="wordmark vertical">Studio</p>
  <ul class="dots"><li></li><li></li><li></li></ul>
</nav>
```
```css
.nav-rail { position: fixed; left: 0; top: 0; bottom: 0; width: 3rem; padding: var(--space-md); writing-mode: vertical-rl; }
```


---

<a id="original-n4-hidden-behind-k"></a>

## Original reference: `n4-hidden-behind-k.md`

### N4 · Hidden behind ⌘K
No visible nav. The user opens a command palette via `⌘K` to get anywhere. Designed for keyboard-first audiences.
*Use when:* the page is for technical users who expect this affordance.
*Don't confuse with:* N2 Floating chip (which is visible always).

```html
<button class="kbd-hint">⌘ K</button>
<dialog class="palette">…</dialog>
```


---

<a id="original-n5-floating-pill"></a>

## Original reference: `n5-floating-pill.md`

### N5 · Floating pill
A rounded full-pill nav, *visibly detached* from the page edges, sitting ~`var(--space-md)` from the top, soft blur backdrop, soft shadow. Reads as contemporary modern-minimal — Vercel, Linear, Framer, Raycast.
*Use when:* the page is modern-minimal / atmospheric and the hero has a distinct surface or imagery beneath the pill that the blur can sit over.
*Don't confuse with:* N1 Wordmark + 2 links (which is full-width); N2 Floating chip (which is corner-anchored).

```html
<nav class="nav-pill" aria-label="Primary">
  <a class="wordmark">Studio</a>
  <ul class="nav-pill__links"><li><a>Catalog</a></li><li><a>Voice</a></li></ul>
  <a class="cta-fill">Get →</a>
</nav>
```
```css
.nav-pill {
  position: fixed; inset: var(--space-md) auto auto 50%;
  transform: translateX(-50%);
  display: inline-flex; align-items: center; gap: var(--space-md);
  padding: 0.5rem 0.875rem;
  background: color-mix(in oklch, var(--color-paper) 78%, transparent);
  backdrop-filter: blur(14px) saturate(120%);
  border: var(--rule-hair) solid var(--color-rule);
  border-radius: 999px;
  box-shadow: 0 8px 24px -12px oklch(0% 0 0 / 0.18);
  z-index: 20;
}
```

*Anti-pattern:* a "pill" that's ~95 % viewport-wide is just a full-width nav with rounded ends — defeats the point. The pill must be visibly detached and content-sized; if your link list pushes it past ~720 px, drop a link or switch to N1.


---

<a id="original-n6-newspaper-masthead"></a>

## Original reference: `n6-newspaper-masthead.md`

### N6 · Newspaper masthead
Full-width header, large centred wordmark on the top row, thin issue/date line above or below in serif small caps, optional inline link row beneath, double-rule below the whole thing. Reads as editorial, broadsheet — NYT, FT, Vogue.
*Use when:* the page is editorial, magazine-shaped, or framed as an issue / edition.
*Don't confuse with:* N1 Wordmark + 2 links (which is asymmetric and small).

```html
<header class="nav-mast">
  <p class="mast-line muted">No 22 · Spring 2026 · Studio</p>
  <h1 class="mast-name">STUDIO</h1>
  <nav class="mast-nav" aria-label="Primary">
    <ul><li><a>Catalog</a></li><li><a>Voice</a></li><li><a>Letters</a></li></ul>
  </nav>
  <hr class="mast-rule double" aria-hidden="true">
</header>
```
```css
.nav-mast { display: grid; gap: var(--space-2xs); padding: var(--space-md) var(--page-gutter) 0; text-align: center; }
.mast-name { font-family: var(--font-display); font-size: clamp(2.25rem, 5vw, 3.75rem); letter-spacing: -0.01em; line-height: 0.95; margin: 0; }
.mast-line { font-variant: small-caps; letter-spacing: 0.08em; font-size: var(--text-xs); }
.mast-nav ul { display: inline-flex; gap: var(--space-md); list-style: none; padding: 0; margin: var(--space-2xs) 0 0; }
.mast-rule.double { border: 0; border-top: var(--rule-hair) solid var(--color-rule); border-bottom: var(--rule-hair) solid var(--color-rule); height: 4px; margin: var(--space-sm) 0 0; }
```

*Anti-pattern:* using N6 on a SaaS dashboard or a developer-tool product page. The masthead vocabulary belongs to long-form / editorial sites; on a B2B product, it reads as costume.


---

<a id="original-n7-brutal-slab"></a>

## Original reference: `n7-brutal-slab.md`

### N7 · Brutal slab
A heavy, full-width nav with a 2 px solid border-bottom, all-caps wordmark and tracked uppercase link row, dense rhythm, no shadow, no rounded corners. Reads as Pentagram project pages, Liquid Death, brutalist-leaning agencies.
*Use when:* the genre is playful (Brutal, Manifesto, Sport) or the brand voice is heavy / declarative.
*Don't confuse with:* N1 Wordmark + 2 links (which is small and quiet).

```html
<header class="nav-slab">
  <a class="slab-mark">STUDIO</a>
  <nav class="slab-nav" aria-label="Primary">
    <ul><li><a>CATALOG</a></li><li><a>VOICE</a></li><li><a>WORK</a></li></ul>
  </nav>
  <a class="cta-fill cta-fill--slab">GET</a>
</header>
```
```css
.nav-slab { display: flex; align-items: center; gap: var(--space-md); padding: var(--space-sm) var(--page-gutter); border-bottom: 2px solid var(--color-ink); background: var(--color-paper); }
.slab-mark { font-family: var(--font-display); font-weight: 800; letter-spacing: 0.04em; }
.slab-nav ul { display: flex; gap: var(--space-md); list-style: none; padding: 0; margin: 0 0 0 auto; }
.slab-nav a { text-transform: uppercase; letter-spacing: 0.08em; font-size: var(--text-sm); font-weight: 600; }
```

*Anti-pattern:* combining N7 with rounded corners, soft shadows, or backdrop-blur — those vocabularies fight. If you reach for blur, drop to N5; if you reach for round, drop to N1.


---

<a id="original-n8-terminal-command"></a>

## Original reference: `n8-terminal-command.md`

### N8 · Terminal command
A nav formatted as a CLI prompt: `> studio --catalog --voice --get▮`. The "links" are command flags. The blinking cursor (`▮`) is allowed *only here* (it has purpose — signals "you'd type next"); never standalone elsewhere on the page. Reads as Vercel CLI docs landing, Charm, Mitchell Hashimoto's site.
*Use when:* the page is a CLI tool, dev-tool docs, or carries the Terminal theme.
*Don't confuse with:* N4 ⌘K-only (which is a palette, not a visible bar).

```html
<header class="nav-term">
  <pre class="nav-term__line"><span class="prompt">&gt;</span> studio <a href="#catalog">--catalog</a> <a href="#voice">--voice</a> <a href="#get">--get</a><span class="caret" aria-hidden="true">▮</span></pre>
</header>
```
```css
.nav-term { padding: var(--space-sm) var(--page-gutter); border-bottom: var(--rule-hair) solid var(--color-rule); }
.nav-term__line { font-family: var(--font-outlier, ui-monospace, "JetBrains Mono", monospace); font-size: var(--text-sm); margin: 0; }
.nav-term__line .prompt { color: var(--color-accent); padding-right: 0.4ch; }
.nav-term__line a { color: var(--color-ink); text-decoration: underline; text-underline-offset: 2px; }
.caret { display: inline-block; width: 1ch; animation: blink 1.05s steps(2) infinite; color: var(--color-accent); }
@keyframes blink { 50% { opacity: 0; } }
@media (prefers-reduced-motion: reduce) { .caret { animation: none; opacity: 1; } }
```

*Anti-pattern:* using `>` prompt vocabulary on a non-developer site (a wedding photographer's portfolio with a `> view --gallery` nav reads as set decoration). N8 belongs to genuine terminal / CLI brands only.


---

<a id="original-n9-edge-aligned-minimal"></a>

## Original reference: `n9-edge-aligned-minimal.md`

### N9 · Edge-aligned minimal
Wordmark hard-left, single CTA hard-right, vast empty space between, no link row at all. The *absence* is the design — Apple product pages, Carl Hauser, luxury sites.
*Use when:* the page is luxury / quiet / Atelier / Garden and the brand earns the silence.
*Don't confuse with:* N1 Wordmark + 2 links (which fills the middle).

```html
<header class="nav-edge">
  <a class="wordmark">Studio</a>
  <a class="cta-outline">Get →</a>
</header>
```
```css
.nav-edge { display: flex; justify-content: space-between; align-items: center; padding: var(--space-md) var(--page-gutter); }
.nav-edge .wordmark { font-family: var(--font-display); font-size: var(--text-md); }
```

*Anti-pattern:* adding 4 inline links between the wordmark and CTA "to fill the space". The space *is* the design; if you fill it, you've made N1 with extra steps.

