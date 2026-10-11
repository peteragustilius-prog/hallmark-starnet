# Hallmark heroes reference catalog

This is a lossless concatenation of the original individual Hallmark component reference files; refer to the heading for the selected archetype.


---

<a id="original-h1-marquee"></a>

## Original reference: `h1-marquee.md`


### H1 · Marquee
A single statement fills the fold. No subhead, no CTA in view.
*Use when:* the brand or person *is* the message.
*Don't confuse with:* H4 Stat-Led (which is a number, not a statement).

```html
<section class="hero-marquee">
  <h1 class="display-xxl">A statement.</h1>
</section>
```
```css
.hero-marquee { min-height: 80dvh; display: grid; align-content: end; padding: 0 var(--page-gutter) var(--space-2xl); }
.display-xxl { font-size: clamp(4rem, 12vw, 12rem); line-height: 0.92; }
```


---

<a id="original-h2-split-diptych"></a>

## Original reference: `h2-split-diptych.md`

### H2 · Split Diptych
Headline + lede on one side, image or product capture on the other. 6/6 or 7/5 columns.
*Use when:* you can pair every claim with a visual proof.
*Don't confuse with:* H6 Photographic (which puts the image full-bleed, not paired).

```html
<section class="hero-split">
  <div><h1>…</h1><p>…</p><a class="cta-outline">…</a></div>
  <figure><img src="" /></figure>
</section>
```
```css
.hero-split { display: grid; grid-template-columns: 7fr 5fr; gap: var(--space-2xl); align-items: center; }
@media (max-width: 56rem) { .hero-split { grid-template-columns: 1fr; } }
```


---

<a id="original-h3-quote-led"></a>

## Original reference: `h3-quote-led.md`

### H3 · Quote-Led
A pull-quote with attribution is the hero. Your headline is borrowed credibility.
*Use when:* you have a real testimonial that earns the front page.
*Don't confuse with:* T3 Single huge quote (which lives mid-page, not in the hero slot).

```html
<section class="hero-quote">
  <blockquote class="display-italic">"…"</blockquote>
  <p class="attribution">— Name, Role, Company</p>
</section>
```


---

<a id="original-h4-stat-led"></a>

## Original reference: `h4-stat-led.md`

### H4 · Stat-Led
A giant number or metric is the hero. A small qualifier line below.
*Use when:* you have one defensible, externally-verifiable number.
*Don't confuse with:* T4 Numbered stat strip (which is several stats in a row, not one focal).

```html
<section class="hero-stat">
  <p class="figure tnum">99.97<span class="unit">%</span></p>
  <p class="qualifier">…</p>
</section>
```
```css
.figure { font-size: clamp(6rem, 18vw, 16rem); font-variant-numeric: tabular-nums; line-height: 0.85; }
```


---

<a id="original-h5-letter-hero"></a>

## Original reference: `h5-letter-hero.md`

### H5 · Letter Hero
First-person opening — "Dear reader,". No buttons in fold. Reads as personal correspondence.
*Use when:* the founder's voice is the brand.
*Don't confuse with:* H1 Marquee (which is impersonal declaration).

```html
<section class="hero-letter">
  <p class="salutation"><em>Dear reader,</em></p>
  <p class="lede">…</p>
</section>
```


---

<a id="original-h6-photographic-fold"></a>

## Original reference: `h6-photographic-fold.md`

### H6 · Photographic Fold
Single full-bleed image fills the viewport. Caption sits in a corner.
*Use when:* you have real photography that earns full-bleed.
*Don't confuse with:* H2 Split (which pairs image with text in a grid).

```html
<section class="hero-photo">
  <img class="bleed" src="" alt="" />
  <p class="caption">Spring, 2026.</p>
</section>
```
```css
.hero-photo { position: relative; height: 80dvh; }
.hero-photo .bleed { width: 100%; height: 100%; object-fit: cover; }
.hero-photo .caption { position: absolute; bottom: var(--space-md); right: var(--space-md); }
```


---

<a id="original-h7-demo-video-clipped-by-viewport-edge"></a>

## Original reference: `h7-demo-video-clipped-by-viewport-edge.md`

### H7 · Demo Video — Clipped-by-viewport-edge
Display headline left, demo video right, the rightmost ~10–20 % extending past the viewport so it's intentionally cut off. The clip *is* the design — implies "there's more product than fits the screen". Pioneered by Linear, refined by Vercel / Resend / Cursor.
*Use when:* the brief is SaaS / dev-tool / dashboard / platform AND you have real footage of the product (or a hand-built CSS-art mockup of it).
*Don't confuse with:* H4 Stat-Led (number-led, no video) or H8 Mockup Split (still screenshot, not video).

See [`hero-enrichment.md`](../hero-enrichment.md) for the full E1 recipe (codec chain, autoplay rules, `prefers-reduced-motion` fallback, mobile collapse). The cookbook entry below is the structural sketch.

```html
<section class="hero hero--clipped">
  <div class="hero__copy">
    <h1>Plan, build, ship.</h1>
    <p>The project tracker your engineering team won't ignore.</p>
  </div>
  <figure class="hero__media">
    <video autoplay muted loop playsinline preload="metadata"
           poster="/hero-poster.webp" fetchpriority="high">
      <source src="/hero.av1.mp4" type='video/mp4; codecs="av01.0.05M.08"'>
      <source src="/hero.h264.mp4" type="video/mp4">
    </video>
  </figure>
</section>
```
```css
.hero--clipped { display: grid; grid-template-columns: 1fr 1.4fr; gap: var(--space-2xl); overflow: visible; }
.hero__media   { width: calc(100% + 12vw); aspect-ratio: 16 / 10; border-radius: 12px; overflow: hidden; }
@media (max-width: 60rem) { .hero--clipped { grid-template-columns: 1fr; } .hero__media { width: 100%; } }
```


---

<a id="original-h8-mockup-split-browser-framed"></a>

## Original reference: `h8-mockup-split-browser-framed.md`

### H8 · Mockup Split (browser-framed)
Headline left, browser-frame mockup right, the mockup tilted 1–3° for life. Frame can be browser chrome, macOS toolbar, minimal hairline, or floating no-frame.
*Use when:* you're selling a web app and you have a clean, well-lit screenshot.
*Don't confuse with:* H7 Clipped-Edge (which extends past the viewport) or H2 Split Diptych (which uses photography or proof column, not a product mockup).

```html
<section class="hero-mock">
  <div>
    <h1>The studio's new mute button.</h1>
    <p>Press <kbd>⌘ M</kbd> from anywhere.</p>
  </div>
  <figure class="mock">
    <header class="mock__chrome"><span></span><span></span><span></span></header>
    <div class="mock__body"><!-- screenshot or CSS-art mockup --></div>
  </figure>
</section>
```
```css
.hero-mock  { display: grid; grid-template-columns: 1fr 1.2fr; gap: var(--space-2xl); align-items: center; }
.mock       { transform: rotate(1.5deg); border-radius: 12px; overflow: hidden; box-shadow: 0 24px 60px -20px oklch(20% 0.02 60 / 0.18); }
.mock__chrome { display: flex; gap: 6px; padding: 10px 12px; background: var(--color-paper-2); border-block-end: var(--rule-hair) solid var(--color-rule); }
.mock__chrome span { width: 10px; height: 10px; border-radius: 50%; background: var(--color-rule-2); }
```


---

<a id="original-h9-custom-illustration-centerpiece"></a>

## Original reference: `h9-custom-illustration-centerpiece.md`

### H9 · Custom Illustration Centerpiece
A single hand-built SVG (Tier B in the enrichment hierarchy — or pure CSS at Tier A for simpler shapes) sitting on the hero as one illustrative element. The bakery loaf, the studio's mascot, the workflow diagram.
*Use when:* the brand has a *thing* that benefits from being drawn — a craft, a character, a process.
*Don't confuse with:* H6 Photographic (real photography) or H8 Mockup (a product screenshot, not artwork).

The illustration itself is *built*, not picked from Storyset / Humaaans / unDraw / Lottie. See [`custom-craft.md`](../custom-craft.md) for full recipes (CSS art, hand-built SVG, declarative animation). The cookbook entry below is the page-level structural sketch.

```html
<section class="hero-art">
  <div>
    <p class="eyebrow">Maple Street Bread · est. 2026</p>
    <h1>Sourdough, every morning.</h1>
    <p>Slow-fermented overnight, baked on stone, before you wake.</p>
  </div>
  <svg viewBox="0 0 200 100" class="loaf" aria-label="A loaf of bread">
    <path class="loaf__body" d="M 20 70 Q 100 10 180 70 L 180 90 L 20 90 Z" />
    <path class="loaf__score" d="M 60 50 L 90 30 M 100 45 L 130 25 M 140 50 L 165 35" />
  </svg>
</section>
```
```css
.hero-art   { display: grid; grid-template-columns: 1fr 1fr; gap: var(--space-2xl); align-items: center; }
.loaf__body { fill: oklch(72% 0.14 50); }
.loaf__score{ stroke: oklch(38% 0.10 35); stroke-width: 2; fill: none; stroke-linecap: round; }
```

---

