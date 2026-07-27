# Editing the Blossom Duo Landing Page (Quick Guide)

Everything is in **one file: `index.html`** (all styles + scripts inline). Images live in `images/`. No build step.

## How to publish an edit
- **Easiest (in browser):** open the repo on GitHub → `index.html` → pencil icon → edit → *Commit changes*. Live site updates ~1 min later.
  - Power version: press the **`.`** key on the repo page → full VS Code in browser.
- **Locally:** edit the file in any editor → then run:
  ```
  git add -A
  git commit -m "copy edits"
  git push
  ```
- After it deploys, **hard-refresh** the page: `Ctrl+Shift+R` (Windows) / `Cmd+Shift+R` (Mac).

## Where things are (Ctrl+F for these markers)
| Marker | Section |
|---|---|
| `<!-- PROMO BAR -->` | Top black offer strip |
| `<!-- HERO -->` | Headline, price, CTA, image carousel |
| `<!-- PROBLEM -->` | "Why 80% of Women Fake It" |
| `<!-- REVIEWS -->` | UGC photos + 6 review cards (`rcard` blocks) |
| `<!-- OFFER -->` | Countdown + price box |
| `<!-- FAQ -->` | Accordion items (`faq-item` blocks) |
| `<!-- STICKY BAR -->` | Bottom buy bar |

## Fixing "weirdly cut" or ugly-wrapping text
1. **Force a line break where YOU want it:** insert `<br/>` in the headline.
   `Real People.<br/>Real Climaxes.` → always two lines.
2. **Keep two words together** (never split across lines): replace the space with `&nbsp;`.
   `Fake&nbsp;It` can never break between "Fake" and "It".
3. **Make a headline smaller on phones:** near the bottom of the `<style>` block, inside `@media(max-width:560px){ ... }`, find:
   ```css
   h2.sect{font-size:clamp(24px,7.2vw,34px);line-height:1}
   .hero h1{font-size:clamp(34px,10vw,48px)}
   ```
   Lower the **last number** (max size) to shrink section headlines on mobile. First number = minimum, middle = scaling rate.
4. Long words/lines can always wrap safely — `overflow-wrap:break-word` is already set on all headings as insurance.

## Gotchas
- **Prices appear in 4 places** (promo bar, hero, offer box, sticky bar). If you change `$44.99` / `$104.99` / `57%`, Ctrl+F the old value and update every hit.
- **Countdown length:** in the `<script>` at the bottom — `DURATION=15*60*1000` (minutes × 60 × 1000).
- **Swap a photo without touching code:** overwrite the file in `images/` keeping the exact same filename (e.g. replace `ugc_sarah.jpg`).
- **Mobile styles** live in two media queries at the end of the `<style>` block: `@media(max-width:860px)` (tablet) and `@media(max-width:560px)` (phones). Phone-specific fixes go in the 560px one.
- Test your edit at phone width: open DevTools (`F12`) → device toolbar (`Ctrl+Shift+M`) → pick iPhone.
