# Handoff: Daylith — Coming Soon Page

## Overview

A single-page **"Coming Soon"** landing for **Daylith**, a mindfulness / morning-routine app. The page is calm, editorial, and minimal: brand lockup near the top, a centered "Coming Soon" headline with body copy, and a layered abstract hill landscape fixed to the bottom of the viewport. Soft warm cream background, deep forest green typography, peach accent.

The intended deployment target is **Vite + React, hosted on GitHub Pages**, but any static-friendly frontend stack is fine — the page has no backend, no auth, no forms.

---

## About the Design Files

The files in this bundle are **design references created in HTML** — a working prototype showing the intended look and behavior, **not production code to copy directly**.

Your task is to **recreate this design in the target codebase's environment** (Vite + React per the original brief, or whatever framework the project standardizes on) using its established patterns and component conventions. The HTML file inlines a Tweaks panel for design exploration — **drop the Tweaks panel entirely** in production; it is a design tool, not a feature.

---

## Fidelity

**High-fidelity (hifi).** Final colors, typography, spacing, and the brand lockup are pixel-targeted. Recreate as accurately as your stack allows. The layout, hill geometry, and color values below are authoritative.

---

## Screens / Views

There is exactly one view.

### `ComingSoon`

- **Purpose:** Communicate that Daylith is launching, set the brand tone.
- **Viewport:** Full viewport height (`100vh` / `100svh`), no horizontal scroll.
- **Layout:**
  - Outer `<main>` is a flex column, centered horizontally, with `min-height: 100vh`.
  - Inner stage (`max-width: 720px`) is a flex column with `align-items: center`, `text-align: center`.
  - Stage `padding-top`: `clamp(32px, 6vh, 80px)`.
  - Stage `padding-bottom`: `clamp(180px, 26vh, 320px)` — reserves space for the fixed hills so content never collides with them.
  - Hills are absolutely positioned (`position: fixed; bottom: 0; left: 0; right: 0;`) and span the full viewport width.

- **Content stack (top → bottom):**
  1. Brand lockup image (`assets/daylith-logo-full.png` — sun mark + "Daylith" wordmark + "YOUR MORNING, ELEVATED." tagline as a single PNG).
  2. `<h1>Coming Soon</h1>`
  3. Thin horizontal rule (`<hr class="divider">`)
  4. Body paragraph: `We're crafting a mindful experience` `<br>` `to elevate your every day.`

- **Components:**

  | Element | Spec |
  |---|---|
  | **Logo image** | `width: clamp(320px, 38vw, 500px)`, mobile `280px`. `margin-bottom: 64–72px` desktop, `48px` mobile. PNG with transparency. |
  | **`<h1>` "Coming Soon"** | font-family: Playfair Display; weight: 400; size: `clamp(42px, 6vw, 68px)`; line-height: 1.05; letter-spacing: -0.012em; color: `#0F2A23`; margin: `0 0 28px`. |
  | **Divider** | `width: 56px; height: 1px;` background: `#8E9B83`; opacity: 0.55; margin: `8px auto 28px`. |
  | **Body copy** | font-family: Inter; weight: 300; size: `clamp(16px, 1.4vw, 19px)`; line-height: 1.65; color: `#44524C`; max-width: 460px. Uses an explicit `<br>` for the line break. |
  | **Hill landscape** | Inline SVG, 6 layered paths, `viewBox="0 0 1440 320"`, `preserveAspectRatio="none"`. Container height: `26vh` (min `200px`) desktop, `20vh` (min `160px`) ≤ 700px. |

  **Hill SVG paths** (in z-order, back → front):

  ```svg
  <svg viewBox="0 0 1440 320" preserveAspectRatio="none">
    <!-- back: pale sand -->
    <path fill="#E7DCCB" d="M0,180 C160,120 280,120 420,170 C560,220 680,220 820,180 C960,140 1120,140 1280,180 C1360,200 1410,210 1440,205 L1440,320 L0,320 Z" />
    <!-- mid-back: light sage -->
    <path fill="#B7BCA9" opacity="0.95" d="M0,220 C140,180 260,200 400,230 C540,260 680,240 820,220 C960,200 1120,210 1260,240 C1340,256 1400,260 1440,255 L1440,320 L0,320 Z" />
    <!-- mid: muted sage -->
    <path fill="#8E9B83" d="M0,250 C120,230 240,260 380,265 C520,270 640,250 780,255 C920,260 1060,290 1200,280 C1300,273 1380,268 1440,272 L1440,320 L0,320 Z" />
    <!-- front-left forest hill -->
    <path fill="#1A3A34" d="M0,260 C80,238 180,250 280,270 C360,286 420,294 460,300 L460,320 L0,320 Z" />
    <!-- front-right forest hill -->
    <path fill="#1A3A34" d="M820,295 C940,272 1060,260 1180,270 C1300,280 1380,290 1440,288 L1440,320 L820,320 Z" />
    <!-- deepest forest base -->
    <path fill="#0F2A23" d="M0,295 C160,278 320,288 480,298 C640,308 800,304 960,300 C1120,296 1280,300 1440,304 L1440,320 L0,320 Z" />
  </svg>
  ```

- **Subtle paper grain** (optional but recommended): a fixed-position `::before` overlay with a 3px radial-dot background, ~5% opacity, `mix-blend-mode: multiply`. Adds depth without being noisy.

---

## Interactions & Behavior

- **No click interactions, no forms, no navigation.** Static page.
- **Entrance animation:**
  - Content (logo → heading → divider → body) fades in with `translateY(8px) → 0`, 700ms ease-out, staggered delays of ~120ms per item starting at 120ms.
  - Hill landscape fades in at 200ms, 1000ms ease-out (opacity only).
  - No bouncing, no parallax, no scroll triggers.
- **Responsive behavior:** all sizes use `clamp()` so the layout scales fluidly between 375px and 1440px+.
- **Reduced motion:** wrap all animations in `@media (prefers-reduced-motion: reduce)` and disable them.

---

## State Management

None. Static content.

---

## Design Tokens

### Colors

| Token | Hex | Usage |
|---|---|---|
| `--forest` | `#0F2A23` | Primary text (heading, wordmark in logo), deepest hill |
| `--forest-soft` | `#1A3A34` | Mid-front hills |
| `--peach` | `#DE9B73` | Accent — tagline color (in logo PNG) |
| `--sage` | `#8E9B83` | Mid hill, divider line |
| `--sage-light` | `#B7BCA9` | Mid-back hill |
| `--cream` | `#F4EFE6` | Page background |
| `--sand` | `#E7DCCB` | Back hill |
| `--text-muted` | `#44524C` | Body copy |
| `--theme-color` (meta) | `#0F2A23` | `<meta name="theme-color">` for mobile chrome |

### Typography

| Family | Weights | Source |
|---|---|---|
| **Playfair Display** | 400 (heading), 500 (wordmark — already baked into logo PNG) | Google Fonts |
| **Inter** | 300, 400, 500 | Google Fonts |

Preconnect + load via:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,500;0,600;1,400&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
```

Type scale used:

| Style | Family | Size | Weight | Color |
|---|---|---|---|---|
| H1 ("Coming Soon") | Playfair Display | `clamp(42px, 6vw, 68px)` | 400 | `#0F2A23` |
| Body | Inter | `clamp(16px, 1.4vw, 19px)` | 300 | `#44524C` |

### Spacing

- Logo bottom margin: `64–72px` desktop, `48px` mobile
- H1 bottom margin: `28px`
- Divider: `8px auto 28px`
- Body max-width: `460px`
- Stage horizontal padding: `24px`
- Stage padding-top: `clamp(32px, 6vh, 80px)`
- Stage padding-bottom: `clamp(180px, 26vh, 320px)`

### Other

- Border-radius: not used (no buttons, cards, or chips on this page)
- Shadows: none
- Body smoothing: `-webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; text-rendering: optimizeLegibility;`

---

## Meta / SEO

```html
<title>Daylith — Coming Soon</title>
<meta name="description" content="Daylith is a mindfulness app for calmer, more intentional mornings.">
<meta name="theme-color" content="#0F2A23">
<meta name="viewport" content="width=device-width, initial-scale=1">
```

---

## Assets

| File | Description |
|---|---|
| `assets/daylith-logo-full.png` | Brand lockup: sunrise mark + "Daylith" wordmark + "YOUR MORNING, ELEVATED." tagline. 1123×794, transparent PNG. **The tagline text is part of the image** — do not duplicate it as HTML below the logo. Sized via CSS `width`. |
| `reference-mockup.png` | Original reference mockup from the design brief. |

If shipping for retina displays, consider exporting the logo at 2× and using `srcset`, or replace with an SVG version when the brand team can supply one.

---

## Recommended Implementation (Vite + React)

```
src/
  main.jsx              # ReactDOM root
  App.jsx               # Single ComingSoon component
  App.css               # Page styles + tokens as :root vars
  components/
    Hills.jsx           # Inline SVG, props for theming
public/
  assets/
    daylith-logo-full.png
index.html              # Meta tags + Google Fonts link
vite.config.js          # base: './' for GitHub Pages
```

`vite.config.js`:

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
export default defineConfig({ plugins: [react()], base: './' })
```

`package.json` scripts:

```json
{
  "dev": "vite",
  "build": "vite build",
  "preview": "vite preview",
  "deploy": "gh-pages -d dist"
}
```

For a custom domain, add `public/CNAME` containing the bare domain (e.g. `daylith.com`).

---

## Files in This Handoff

- `Daylith Coming Soon.html` — the working HTML prototype. Open it in a browser to see the design rendered exactly as intended. **Reference, not production code.**
- `tweaks-panel.jsx` — design-time exploration tool. **Do not include in production.**
- `assets/daylith-logo-full.png` — brand lockup (use as-is).
- `reference-mockup.png` — original reference image.
- `README.md` — this file.

---

## Quality Bar

- No placeholder copy, no stock photos, no fake countdown, no newsletter form.
- No buttons or CTAs.
- Hills must stay pinned to the bottom of the viewport at all sizes.
- No horizontal scrollbar at any width ≥ 320px.
- Page must reach Lighthouse 100/100/100/100 trivially — it's static, one image, two fonts.
