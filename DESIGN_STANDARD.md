# Design Standard
### 3 AM in Accra — Static Site
*Version 3.0*

---

## Governing Principle

Every visual decision should answer one question: *does this belong on a wet Accra street at 3 AM?* The aesthetic is not cyberpunk maximalism — it is quieter and more melancholy. Accra is not a city of neon towers: its light comes from LED-strip shop signs, a lit church cross, a filling station forecourt, a food seller's single bulb. Colour exists as a smear on black tar, not a loud foreground element. The world is nearly empty. Light is scarce. What little there is glows, flickers, and bleeds into water. Photography, when used, is a layer of atmosphere — dark-treated, never clinical.

---

## 1. Colour Palette

All colours are CSS custom properties on `:root`. No colour value is hardcoded in component styles.

```css
:root {
  /* Backgrounds — three steps from void to surface */
  --void:      #06080f;   /* Primary page background. Deepest near-black. */
  --asphalt:   #0d1117;   /* Mid-layer background. Used in section alternation. */
  --wet-stone: #141820;   /* Lifted surface for cards and hover states. */

  /* Atmospheric overlays */
  --fog:   rgba(180, 200, 230, 0.06);   /* Section dividers, card borders. */
  --mist:  rgba(180, 200, 230, 0.12);   /* Stronger border on interactive elements. */
  --rain:  rgba(180, 200, 230, 0.03);   /* Canvas rain base colour. */

  /* Text — three levels of presence */
  --text-primary: rgba(220, 230, 245, 0.92);   /* Headlines, body text. Cool off-white. */
  --text-dim:     rgba(180, 200, 230, 0.45);   /* Sub-copy, supporting prose. */
  --text-ghost:   rgba(180, 200, 230, 0.18);   /* Labels, metadata, decorative Twi. */

  /* Neon accents — four signs, each with a role */
  --neon-pink:   #ff2d6b;   /* Primary accent. CTAs, key word highlights, The Street heading accent. */
  --neon-cyan:   #00e5ff;   /* Secondary accent. Cursor, focus states, Pillar 02, secondary links. */
  --neon-amber:  #ffaa00;   /* Tertiary accent. The Street h2 line 2, Pillar 03. Warm distance. */
  --neon-violet: #c44dff;   /* Structural accent. Neon sign card top border. Not used on text. */

  /* Reflections — accents at very low opacity for glow and bg effects */
  --reflection-pink: rgba(255, 45, 107, 0.15);
  --reflection-cyan: rgba(0, 229, 255, 0.10);
}
```

### Colour usage rules

- **Backgrounds step in one direction only.** `--void` → `--asphalt` → `--wet-stone`. Cards and hover states use `--wet-stone`. Never introduce a background lighter than `--wet-stone`.
- **Accents are light sources, not brand colours.** Ask where each light is in the scene. Pink is the closest — the LED sign of the spot across the road, on the CTA, bleeding into the hero. Cyan is farther away — a lit church cross, governing the cursor and focus states. Amber is a sodium streetlight in the distance. Violet is a single LED strip above a doorway (the neon card border only).
- **Never use two accents on the same element.** Each element picks one sign to stand near.
- **Text never uses an accent colour except in hover states and the `here` headline treatment.** Neon text at full saturation reads decorative, not communicative.
- **`--text-dim` on `--void` must be verified** with a contrast checker before shipping. It sits close to the WCAG AA floor; do not reduce its opacity further.

---

## 2. Typography

### Font families

```css
:root {
  --font-serif: 'Noto Serif', serif;        /* Editorial weight. Headlines, body prose, the neon sign, the manifesto. */
  --font-mono:  'Space Mono', monospace;    /* UI precision. Labels, eyebrows, CTAs, status bar, footer links. */
  --font-sans:  'Noto Sans', sans-serif;    /* Script sub-label only. Thin and architectural. */
}
```

Google Fonts import order: `Noto Serif` (upright 200, 300, 400; italic 200, 300) → `Space Mono` (400 regular, 400 italic, 700 bold) → `Noto Sans` (weights 200, 300). Load with `rel="preconnect"` to `fonts.googleapis.com` before the stylesheet link.

### Weight assignments

| Use | Font | Weight |
|-----|------|--------|
| Hero time stamp | Space Mono | 700 |
| Hero headline | Noto Serif | 300 |
| Section headings (The Street, Contact) | Noto Serif | 200–300 |
| Manifesto quote | Noto Serif | 200 |
| Neon sign name | Noto Serif | 300 |
| Pillar headings | Noto Serif | 300 |
| Body prose (`--text-dim`) | Space Mono | 400 |
| All labels, eyebrows, CTA text | Space Mono | 400 |
| Script main (vertical column) | Noto Serif | 200 |
| Script sub-label | Noto Sans | 200 |

**Rule:** Noto Serif weight 200 is reserved for large decorative elements (the vertical Twi column, the manifesto). It is too delicate for body text at small sizes.

### Size scale

Base: 16 px. Fluid sizes use `clamp()`.

```css
/* Fluid display sizes */
--text-hero-time:   clamp(3.5rem, 8vw, 7rem);      /* Stamp time */
--text-hero-head:   clamp(1.8rem, 3.5vw, 3rem);    /* Hero headline */
--text-section-h2:  clamp(2rem, 4vw, 3.5rem);      /* Section headings */
--text-manifesto:   clamp(1.4rem, 3vw, 2.4rem);    /* Manifesto quote */
--text-script-main: clamp(5rem, 12vw, 10rem);      /* Vertical Twi column */

/* Fixed UI sizes */
--text-body:    0.75rem;   /* 12px — all prose paragraphs */
--text-label:   0.6rem;    /* ~10px — eyebrows, pillar numbers */
--text-micro:   0.55rem;   /* ~9px — status labels, footer copy */
--text-nano:    0.5rem;    /* 8px — ghost labels, metadata */
```

### Line height and letter spacing

```css
--leading-display:  0.9;    /* Hero time stamp. Monolithic. */
--leading-head:     1.2;    /* Section headings. */
--leading-serif:    1.35;   /* Hero headline. Noto Serif at mid size. */
--leading-body:     2.0;    /* All body prose. Open and readable despite small size. */
--leading-loose:    2.2;    /* Street section body. Slightly more air. */

--tracking-tight:   -0.04em;  /* Hero time stamp. */
--tracking-base:    0em;      /* Body text. */
--tracking-wide:    0.2em;    /* CTA labels, eyebrows. */
--tracking-wider:   0.25–0.35em;  /* Status labels, footer links, ghost labels. */
```

### Typographic rules

1. **The hero headline uses italic on a single word** (`here`) rendered as outlined cyan text via `-webkit-text-stroke: 1px rgba(0,229,255,0.6)` with `color: transparent` and a soft cyan `text-shadow`. No other headline word receives this treatment.
2. **The sub-copy in the hero is italic** (`font-style: italic`) with a left-side pink border (`border-left: 1px solid rgba(255,45,107,0.3); padding-left: 1.5rem`).
3. **All CTA and label text is uppercase** via `text-transform: uppercase` in CSS — never written in uppercase in the HTML source.
4. **The vertical Twi column uses `writing-mode: vertical-rl`** with `letter-spacing: 0.05em`. Latin letters rotate 90° and read top to bottom. It is a background texture element: `color: --text-ghost`, `user-select: none`, `aria-hidden="true"`.
5. **Section counter labels** (e.g. `002` in The Street) are positioned absolutely at ghost opacity using `--text-nano` size and `0.3em` tracking. They are not interactive.
6. **Twi strings containing `ɛ` or `ɔ` are never set in Space Mono.** Space Mono has no `ɛ`, `Ɛ` or `Ɔ` glyphs, so these letters would fall back to another font mid-word. Set them in Noto Serif or Noto Sans, which include all of them. Space Mono may carry Twi only where the string avoids those letters, such as `nkran anadwo`.

---

## 3. Spacing

### Base unit

8 px. All layout spacing is a multiple of 8. Half-steps (4 px) are permitted only for optical fine-tuning within a component.

```css
--space-1:   8px;
--space-2:  16px;
--space-3:  24px;
--space-4:  32px;
--space-6:  48px;
--space-8:  64px;
--space-10: 80px;
--space-12: 96px;
--space-16: 128px;
```

### Section rhythm

| Context | Value |
|---------|-------|
| Hero section padding | `0` — content has its own internal padding per sub-zone |
| Stamp padding | `3.5rem 4rem 0` |
| Hero main content padding | `4vh 4rem` |
| Hero status bar padding | `2rem 4rem` |
| Section padding (The Street, Pillars, Contact) | `10–12vh 4rem` |
| Manifesto padding | `14vh 4rem` — the widest vertical space on the page |
| Footer padding | `3rem 4rem` |
| Mobile horizontal padding | `1.5rem` each side |

### Grid gaps

| Grid | Gap |
|------|-----|
| Hero (2-column) | Implicit via column padding |
| The Street (3fr / 2fr) | `6rem` |
| Pillars (3-column) | `0` — borders create separation, not whitespace |
| Contact (1fr / 1fr) | `4rem` |

---

## 4. Texture and Atmosphere

### Background layer stack (back to front)

**Layer 1 — Base fill**
`background-color: var(--void)` on `<body>`.

**Layer 2 — Canvas rain** (`z-index: 1`)
180 drops rendered per frame via `requestAnimationFrame`. Each drop: length 6–24 px, diagonal offset `x-1.5px` per `y+len`, speed 2–5 px/frame, opacity 0.05–0.30, width 0.2–0.8 px. Colour: `rgba(180, 210, 255, opacity)` with a gradient from transparent at the head to full opacity at the tail. Canvas opacity: 0.35. The rain must be peripheral — if a visitor looks directly at it, it is too prominent.

**Layer 3 — Noise grain** (`z-index: 2`, `body::before`)
Inline SVG `feTurbulence` filter (`baseFrequency: 0.9`, `numOctaves: 4`, `stitchTiles: stitch`) rendered as `background-image`. `opacity: 0.6`, `mix-blend-mode: overlay`. This prevents the background from reading as a flat digital render.

**Layer 4 — Puddle reflection** (`z-index: 2`, `body::after`)
Fixed to viewport bottom. Height: `35vh`. Gradient: pink at 0% (`rgba(255,45,107,0.06)`) → cyan at 30% (`rgba(0,229,255,0.04)`) → transparent at 100%. Simulates neon reflecting in standing water on the ground.

**Layer 5 — Page content** (`z-index: 3`, `.page`)

### Hero neon bleed

Two `::before` and `::after` radial gradients on `.hero`:
- Upper-right: pink-to-violet bleed, 60vw × 80vh ellipse, animates with `bleedPulse` (opacity and scale, 8s).
- Lower-left: cyan bleed, 50vw × 60vh ellipse, animates with `bleedPulse` at 11s reversed.
This simulates off-frame signs casting light into the scene.

### Reflection strips

Between every section: a single `<div class="reflection-strip">` — a 1 px full-width horizontal line. Background: a multi-stop gradient from transparent → cyan (8%) → pink (15%) → violet (12%) → cyan (8%) → transparent. Box-shadow: `0 0 40px rgba(255,45,107,0.06)`. Represents light catching a crack in wet pavement.

### Neon glow on text

```css
/* Time stamp glow (::after duplicate) */
.stamp-time::after {
  content: attr(data-time);
  position: absolute; inset: 0;
  color: var(--neon-pink);
  filter: blur(18px);
  opacity: 0.5;
}

/* Neon sign */
.neon-sign {
  text-shadow:
    0 0 10px var(--neon-pink),
    0 0 30px rgba(255,45,107,0.4),
    0 0 60px rgba(255,45,107,0.15);
}
```

Glow on interactive elements (CTA) uses `box-shadow`, not `filter`, to avoid layout impact.

---

## 5. Interactions

### Motion philosophy

Movement on this page is slow and deliberate — the city at 3 AM is not energetic. Easing is always `ease` on entrances and state changes. Nothing bounces. Nothing snaps. The one exception is the neon flicker, which uses `steps(1, end)` — a hard cut, because a sign on unsteady power does not dim smoothly.

### Timing tokens

```css
--duration-fast:   0.15s;   /* Colour changes on secondary links */
--duration-base:   0.3s;    /* Most hover transitions */
--duration-slow:   0.4s;    /* Pillar background, glow expansion */
--duration-reveal: 0.9s;    /* Scroll-reveal transition */
--duration-load:   1.2s;    /* Hero entrance animations */
```

### Hero entrance keyframes

```css
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}

@keyframes fadeLeft {
  from { opacity: 0; transform: translateX(24px); }
  to   { opacity: 1; transform: translateX(0); }
}
```

Stamp and hero main: `fadeUp`. Script column: `fadeLeft` (enters from the right edge). Status bar: `fadeUp` with 1s delay. All use `animation-fill-mode: both`.

### Scroll reveal

```css
.reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.9s ease, transform 0.9s ease;
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
```

`IntersectionObserver` threshold: 0.12. Once visible, the class is not removed — sections do not re-hide on scroll up.

### Flicker keyframes

```css
@keyframes flicker {
  /* Stamp time glow */
  0%, 44%, 47%, 89%, 92%, 100% { opacity: 0.5; }
  45%, 46%  { opacity: 0.2; }
  90%, 91%  { opacity: 0.3; }
}

@keyframes signFlicker {
  /* Neon sign card */
  0%, 91%, 94%, 96%, 100% { opacity: 1; }
  92%, 93% { opacity: 0.4; }
  95%      { opacity: 0.7; }
}
```

### `prefers-reduced-motion`

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration:   0.01ms !important;
    animation-delay:      0ms    !important;
    transition-duration:  0.01ms !important;
  }
}
```

Canvas rain should also check `window.matchMedia('(prefers-reduced-motion: reduce)').matches` before starting the animation loop.

---

## 6. Accessibility Floor

| Requirement | Target | Notes |
|-------------|--------|-------|
| Body text contrast | WCAG AA — 4.5:1 | `--text-primary` on `--void` passes comfortably. |
| Secondary text contrast | WCAG AA — 4.5:1 | `--text-dim` on `--void` is marginal — verify before shipping. Do not reduce opacity further. |
| CTA contrast | WCAG AA — 3:1 (UI components) | Pink border on void passes. Verify inverted text on filled hover state. |
| Touch targets | 44 × 44 px minimum | Apply to CTA buttons, contact link, and footer links on mobile. |
| Flash rate | WCAG 2.3.1 — below 3/second | All flicker animations are compliant (see Section 5). Do not increase flash frequency. |
| Decorative elements | `aria-hidden="true"` | All script column text, section counters, SVG icons, and the reflection strip. |
| Custom cursor | Native cursor restored without JS | Acceptable to set `cursor: none` in CSS; JS unavailability means cursor JS also fails, so the styled cursor elements are invisible and the native cursor is present. |

---

*End of Design Standard*
