# Hallmark footers reference catalog

This is a lossless concatenation of the original individual Hallmark component reference files; refer to the heading for the selected archetype.


---

<a id="original-ft1-mast-headed"></a>

## Original reference: `ft1-mast-headed.md`


### Ft1 · Mast-headed
A wordmark and tagline anchor a single horizontal band. Two or three small links beside, address or licence below.
*Use when:* the page has heavy content; the footer should be quiet and singular.
*Don't confuse with:* Ft2 Inline-rule (which is even more reduced).

```html
<footer class="foot-mast">
  <p class="wordmark">Studio Name</p>
  <p class="tagline muted">Designs that don't look generated.</p>
  <p class="links muted">Imprint · Privacy · Contact</p>
</footer>
```


---

<a id="original-ft2-inline-rule-single-line"></a>

## Original reference: `ft2-inline-rule-single-line.md`

### Ft2 · Inline-rule single line
A single horizontal line of credits, address, copyright. Hairline rule above. No columns.
*Use when:* the page is editorial and the footer is afterthought.
*Don't confuse with:* Ft4 Dense typographic (which packs more in).

```html
<footer class="foot-line">
  <p>© 2026 · 137 Marlow Street · MIT licensed</p>
</footer>
```


---

<a id="original-ft3-index-style-category-list"></a>

## Original reference: `ft3-index-style-category-list.md`

### Ft3 · Index-style category list
Three or four short columns, each headed by a category in small caps, holding 4–6 links each.
*Use when:* the page is a hub or a documentation root.
*Don't confuse with:* Ft4 Dense typographic (which is one big block, not columns).

```html
<footer class="foot-index">
  <div><p class="caps">Product</p><ul>…</ul></div>
  <div><p class="caps">Company</p><ul>…</ul></div>
  <div><p class="caps">Resources</p><ul>…</ul></div>
</footer>
```


---

<a id="original-ft4-dense-typographic"></a>

## Original reference: `ft4-dense-typographic.md`

### Ft4 · Dense typographic
One large block of text — credits, references, licence, address — in a small monospace font, fully justified or ragged-right. Editorial colophon energy.
*Use when:* the brand is editorial and a colophon-style sign-off fits.
*Don't confuse with:* Ft3 Index (which navigates).

```html
<footer class="foot-dense mono">
  <p>Hallmark v0.2.0. Built with The Future, Fraunces, IBM Plex Mono. MIT licensed. Powered by Together AI. 137 Marlow Street, 2026.</p>
</footer>
```


---

<a id="original-ft5-statement"></a>

## Original reference: `ft5-statement.md`

### Ft5 · Statement
One large display sentence dominates the footer — a closing line, not a sitemap. Wordmark, minimal links, copyright sit beneath in muted small type. Stripe (older), Mailchimp pre-rebrand, agency portfolio closers.
*Use when:* the page wants a *closing line* — editorial, manifesto, atmospheric. The sentence pairs with the page's argument.
*Don't confuse with:* Ft1 Mast-headed (which leads with the wordmark, not a sentence).

```html
<footer class="foot-stmt">
  <p class="foot-stmt__line">Build something they'll remember.</p>
  <div class="foot-stmt__meta">
    <span class="wordmark">Studio</span>
    <span class="muted">© 2026 · MIT</span>
  </div>
</footer>
```
```css
.foot-stmt { padding: var(--space-2xl) var(--page-gutter) var(--space-xl); display: grid; gap: var(--space-lg); }
.foot-stmt__line { font-family: var(--font-display); font-size: clamp(1.75rem, 5vw, 3.25rem); line-height: 1.0; letter-spacing: -0.02em; max-width: 28ch; margin: 0; }
.foot-stmt__meta { display: flex; justify-content: space-between; align-items: baseline; padding-block-start: var(--space-sm); border-top: var(--rule-hair) solid var(--color-rule); }
```

*Anti-pattern:* using a Statement footer on a docs root or hub. The sentence reads as marketing fluff there; default Ft3 instead.


---

<a id="original-ft6-letter-close"></a>

## Original reference: `ft6-letter-close.md`

### Ft6 · Letter close
Closes the page like a letter — `Yours, the team. 2026.` Optional postscript line beneath. Sets the page as a piece of writing rather than a product.
*Use when:* the page voice is warm, hand-written, editorial-quiet — Garden, Atelier, personal sites.
*Don't confuse with:* Ft1 Mast-headed (which is a wordmark anchor, not a signoff).

```html
<footer class="foot-letter">
  <p class="foot-letter__close">Yours,<br><span class="foot-letter__sign">— Studio</span></p>
  <p class="foot-letter__ps muted">P.S. — letters back welcome at <a href="mailto:hello@studio">hello@studio</a>.</p>
</footer>
```
```css
.foot-letter { padding: var(--space-2xl) var(--page-gutter); max-width: 60ch; }
.foot-letter__close { font-family: var(--font-display); font-style: italic; font-size: var(--text-lg); line-height: 1.4; }
.foot-letter__sign { font-style: normal; font-weight: 600; }
.foot-letter__ps { font-size: var(--text-sm); margin-top: var(--space-md); }
```

*Anti-pattern:* using Ft6 on a stat-led / B2B product page — voice mismatch reads as twee. Reserve for genuinely letter-shaped pages.


---

<a id="original-ft7-newsletter-first"></a>

## Original reference: `ft7-newsletter-first.md`

### Ft7 · Newsletter-first
The form (label + input + submit) is the *primary* element of the footer; everything else (wordmark, links, copyright) is set in 12 px muted type beneath. Stratechery, Substack-shaped sites, indie magazines.
*Use when:* the brand legitimately publishes — and the page above the fold has *already* offered a subscription. The footer is a final invitation, not an ambush.
*Don't confuse with:* Ft1 (which doesn't ask for anything).

```html
<footer class="foot-news">
  <form class="foot-news__form" action="/subscribe" method="post">
    <label for="foot-email">Letters from the studio · monthly</label>
    <div class="foot-news__row">
      <input id="foot-email" name="email" type="email" required placeholder="you@domain">
      <button type="submit" class="cta-fill">Subscribe</button>
    </div>
  </form>
  <p class="foot-news__meta muted">Studio · © 2026 · <a href="/imprint">Imprint</a></p>
</footer>
```
```css
.foot-news { padding: var(--space-2xl) var(--page-gutter); display: grid; gap: var(--space-lg); max-width: 56ch; }
.foot-news__form label { display: block; font-size: var(--text-sm); margin-block-end: var(--space-2xs); }
.foot-news__row { display: flex; gap: var(--space-2xs); }
.foot-news__row input { flex: 1; min-height: 44px; padding-inline: var(--space-sm); border: var(--rule-hair) solid var(--color-rule); border-radius: var(--radius-input); background: var(--color-paper); }
.foot-news__row input:focus-visible { outline: 2px solid var(--color-focus); outline-offset: 1px; }
.foot-news__meta { font-size: var(--text-xs); }
```

*Anti-pattern:* Ft7 when the page never said "subscribe" above the fold. The footer is an honest *conclusion*; if you didn't ask, don't ambush. Drop to Ft2 instead.


---

<a id="original-ft8-marquee-scroll"></a>

## Original reference: `ft8-marquee-scroll.md`

### Ft8 · Marquee scroll
A horizontal infinite-scroll line of repeating tagline + dot separator: `STUDIO · 2026 · STUDIO · 2026 · STUDIO · 2026 ·`. Sport-genre sites, fashion lookbooks, brand-forward agencies.
*Use when:* the brand voice is loud, kinetic, sport-or-manifesto.
*Don't confuse with:* Ft4 Dense colophon (which is static text).

```html
<footer class="foot-marquee" aria-label="Footer">
  <div class="foot-marquee__track" aria-hidden="true">
    <span>STUDIO · 2026 · STUDIO · 2026 · STUDIO · 2026 · STUDIO · 2026 ·</span>
    <span>STUDIO · 2026 · STUDIO · 2026 · STUDIO · 2026 · STUDIO · 2026 ·</span>
  </div>
  <p class="visually-hidden">Studio · 2026 · MIT licensed</p>
</footer>
```
```css
.foot-marquee { overflow: hidden; border-top: 2px solid var(--color-ink); }
.foot-marquee__track { display: flex; gap: var(--space-2xl); white-space: nowrap; padding-block: var(--space-md); animation: foot-marquee 32s linear infinite; }
.foot-marquee__track span { font-family: var(--font-display); font-weight: 700; letter-spacing: 0.08em; font-size: clamp(1rem, 2.5vw, 1.5rem); }
@keyframes foot-marquee { from { transform: translateX(0); } to { transform: translateX(-50%); } }
@media (prefers-reduced-motion: reduce) { .foot-marquee__track { animation: none; } }
```

*Anti-pattern:* using Ft8 on editorial / quiet contexts — the motion reads as loud. Pair only with playful / sport / manifesto voices, and always honour `prefers-reduced-motion: reduce`.

---

