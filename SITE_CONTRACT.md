# Site Contract
### 3 AM in Accra — Static Site
*Version 3.0*

---

## 1. Page Structure

| # | Section | Purpose |
|---|---------|---------|
| 0 | **Document Metadata** | Supply browser tab text and social sharing previews — no visual render position. |
| 1 | **Hero** | Establish the full atmospheric world on first load: time stamp, editorial headline, status bar, vertical Twi column. |
| — | *Reflection strip* | Single-pixel neon gradient rule separating each section — a pavement puddle between pools of light. |
| 2 | **The Street** | Deepen the world with editorial prose and a neon sign card; the visitor settles in. |
| — | *Reflection strip* | |
| 3 | **Three Pillars** | Articulate the emotional logic of the hour in three named, iconed, colour-coded ideas. |
| — | *Reflection strip* | |
| 4 | **Manifesto** | A single centred quote that names what the whole site is about — the pause between versions of the city. |
| — | *Reflection strip* | |
| 5 | **Contact** | Provide the one means of reaching the site owner without leaving the page. |
| 6 | **Footer** | Close with a Twi logotype, four navigation links, and a copyright line. |

---

## 2. Content Inventory

### 2.0 Document Metadata
| Field | Description | Constraints |
|-------|-------------|-------------|
| `page_title` | HTML `<title>` and `og:title`. | Max 60 characters. Evocative tone. |
| `meta_description` | `<meta name="description">` and social preview copy. | Max 155 characters. One sentence. Caption register, not pitch register. |

### 2.1 Hero — Stamp
| Field | Description | Constraints |
|-------|-------------|-------------|
| `stamp_time` | Large time display top-left. | Format `HH:MM`. Hard-coded or JS-replaced. Carries a blurred pink glow duplicate via `::after`. |
| `stamp_location` | Sub-label below time. | Plain text. Preceded by a short cyan rule via `::before`. |

### 2.2 Hero — Main Copy
| Field | Description | Constraints |
|-------|-------------|-------------|
| `eyebrow` | Micro-label above headline. | Prefixed `//`. Pink neon. All-caps via CSS. |
| `headline` | Primary editorial statement. | Noto Serif weight 300. Key word `here` rendered as outlined cyan text using `-webkit-text-stroke`. Max 2 lines at desktop. |
| `sub_copy` | Supporting prose. | Max 3 sentences. Left-bordered with a faint pink rule. Font-style italic via CSS. |
| `cta_primary_label` | Primary CTA link text. | 3–6 words. Quiet imperative. Pink border button with fill-on-hover. |
| `cta_secondary_label` | Secondary CTA link text. | 2–4 words. Ghost style. Arrow appended via `::after`, translates right on hover. |

### 2.3 Hero — Script Column
| Field | Description | Constraints |
|-------|-------------|-------------|
| `script_main` | Large vertical Twi word. | Noto Serif weight 200. `writing-mode: vertical-rl`. Ghost colour. `aria-hidden="true"`. Hidden below 900 px. |
| `script_sub` | Small horizontal sub-label. | Ghost colour, wide tracking. `aria-hidden="true"`. |

### 2.4 Hero — Status Bar
| Field | Description | Constraints |
|-------|-------------|-------------|
| `status_last_trotro` | Departure time of the last trotro. | Plain text with a ghost label above. |
| `status_next_trotro` | Expected departure of the next trotro. | Plain text with a ghost label above. |
| `status_current` | Live status indicator. | Cyan colour. Preceded by a pulsing dot (CSS `@keyframes livePulse`). |
| `status_temp` | Current temperature. | Plain text with a ghost label above. |

### 2.5 The Street — Text Column
| Field | Description | Constraints |
|-------|-------------|-------------|
| `heading_line_1` | First line of section heading. | Noto Serif weight 200. Large display size. |
| `heading_line_2` | Second line, accent treatment. | Same size. Amber neon colour with glow. Italic. Block element. |
| `body_1` | First prose paragraph. | Max 4 sentences. |
| `body_2` | Second prose paragraph. | Max 3 sentences. |

### 2.6 The Street — Neon Sign Card
| Field | Description | Constraints |
|-------|-------------|-------------|
| `sign_name` | Name of the drinking spot in Twi. | Noto Serif, pink neon glow, flicker animation (`@keyframes signFlicker`). |
| `sign_meta` | Type of venue and hours. | Two lines, ghost colour, all-caps via CSS, wide tracking. |

### 2.7 Three Pillars
Three instances of the same field set:

| Field | Description | Constraints |
|-------|-------------|-------------|
| `number` | Ordinal label (e.g. `— 01`). | Ghost colour, wide tracking. |
| `icon` | Inline SVG geometric mark. | 32 × 32 px viewBox. Strokes only, no fills except a single centre point on pillar 01. `aria-hidden="true"`. Each pillar uses its accent colour. |
| `heading` | Two-line pillar title. | Noto Serif weight 300. Pillar's accent colour. Line break after first word. |
| `body` | Supporting paragraph. | Max 3 sentences. Dim colour. Small size, line-height 2. |

### 2.8 Manifesto
| Field | Description | Constraints |
|-------|-------------|-------------|
| `quote` | Central display quote. | Noto Serif weight 200. Large fluid size. Flanked by `“ ”` CSS pseudo-elements at ghost opacity. |
| `attribution` | Source label. | Ghost colour. All-caps via CSS. Prefixed `//`. Wide tracking. |

### 2.9 Contact
| Field | Description | Constraints |
|-------|-------------|-------------|
| `heading` | Section heading. | Noto Serif weight 300. Max 2 lines. |
| `body` | Prose framing the contact action. | Max 3 sentences. Atmospheric register. |
| `contact_href` | `mailto:` URI. | **Must be filled before build.** No form handler, no backend. |
| `contact_link_label` | Visible contact link text. | Email address or short label. Renders as `<a href="mailto:…">`. |

> The HTML reference includes styled `<input>` fields (email, city) and a button. These may be retained as decorative visual elements. They must not submit data anywhere — no `action`, no fetch, no serverless function — unless the PRD is revised to permit it.

### 2.10 Footer
| Field | Description | Constraints |
|-------|-------------|-------------|
| `logo` | Twi logotype. | Noto Serif weight 300. Ghost colour. `aria-hidden="true"` if purely decorative. |
| `links` | Four navigation anchors. | All-caps via CSS. Ghost colour default, pink on hover. Destinations are page anchors or placeholders. |
| `copyright` | Copyright line. | Small, ghost colour, wide tracking. Year may be JS-generated. |

---

## 3. Behaviour Spec

All behaviour is vanilla HTML, CSS, and JavaScript. No frameworks. No backend calls. All content visible and all links functional with JavaScript disabled.

---

### 3.1 Global: Fixed Layers (z-index stack, back to front)

| Layer | Element | z-index |
|-------|---------|---------|
| 1 | Canvas rain (`#rain-canvas`) | 1 |
| 2 | Noise grain (`body::before`) | 2 |
| 3 | Puddle reflection (`body::after`) | 2 |
| 4 | Page content (`.page`) | 3 |
| 5 | Custom cursor | 9998–9999 |

### 3.2 Custom Cursor

- The native cursor is hidden (`cursor: none` on `body`).
- A 6 × 6 px cyan dot (`#cursor`) follows the mouse exactly.
- A 28 × 28 px ring (`#cursorRing`) follows with lag: each frame, the ring position moves 12% of the distance toward the dot (`rx += (mx - rx) * 0.12`). Uses `requestAnimationFrame`.
- On `mouseenter` of any `a`, `button`, or `input`: ring expands to 48 × 48 px and border colour shifts to pink at 60% opacity. Transition: `width`, `height`, `border-color` 0.2s ease.
- On `mouseleave`: ring returns to 28 × 28 px, cyan border at 40% opacity.
- Fallback: if JS is disabled, the native cursor is visible (the `cursor: none` declaration is applied via JS, not CSS, is acceptable — or apply it in CSS knowing native cursor returns without JS).

### 3.3 Navigation Behaviour

- No persistent navigation bar.
- `cta_primary` scrolls to its target section via `href="#id"` and `scroll-behavior: smooth` on `<html>`.
- `cta_secondary` scrolls to `#contact`.
- Footer links are page anchors or placeholder `href="#"` until destinations are confirmed.
- No hash routing, no back-button interception.

### 3.4 Scroll Behaviour

- `scroll-behavior: smooth` on `<html>` via CSS.
- No scroll-jacking. Native scroll speed is never overridden.
- Scroll-reveal: all sections carry the class `.reveal`. An `IntersectionObserver` (threshold 0.12) adds `.visible` when a section enters the viewport. Transition: `opacity 0.9s ease`, `transform 0.9s ease` from `translateY(30px)` to `translateY(0)`. The hero does not use `.reveal` — it animates on page load.

### 3.5 Hover States

| Element | Default | Hover | Transition |
|---------|---------|-------|------------|
| `.btn-primary` | Transparent fill, pink border, pink text | Fill slides in from left via `::before translateX(-101% → 0)`, text becomes near-black | `transform` 0.3s ease; `color` 0.3s ease |
| `.btn-primary` glow | No shadow | `box-shadow: 0 0 30px rgba(255,45,107,0.4)` | 0.3s ease |
| `.btn-ghost` | Dim text, arrow via `::after` | Text becomes cyan, arrow translates `+4px` right | `color` 0.3s ease; `transform` 0.3s ease |
| `.pillar` | `--void` background, no bottom border | Background becomes `--wet-stone`; bottom border (2 px, pillar accent colour, with glow) scales in from left | `background` 0.4s ease; `transform` 0.4s ease |
| Footer links | Ghost colour | Pink | `color` 0.3s ease |
| Contact `mailto:` link | Cyan colour, no underline | Steps up toward white, underline appears | `color` 0.15s ease |

### 3.6 Hero Load Animations

All use CSS `animation` with `animation-fill-mode: both` and `animation-delay`. Keyframes: `fadeUp` (opacity 0→1, translateY 24px→0), `fadeLeft` (opacity 0→1, translateX 24px→0).

| Element | Keyframe | Delay |
|---------|----------|-------|
| `.stamp` | `fadeUp` | 0.2s |
| `.script-col` | `fadeLeft` | 0.5s |
| `.hero-main` | `fadeUp` | 0.6s |
| `.hero-footer` (status bar) | `fadeUp` | 1.0s |

### 3.7 Ongoing Ambient Animations

| Animation | Element | Spec |
|-----------|---------|------|
| `bleedPulse` | Hero neon gradient bleed (pseudo-elements) | `opacity 0.6→1`, `scale 1→1.08`. 8s and 11s durations, `alternate` / `alternate-reverse`. Runs `infinite`. |
| `flicker` | `stamp-time::after` (blurred pink glow duplicate) | `opacity` stutters at 45–46% and 90–92% of the 6s cycle. `infinite`. |
| `signFlicker` | `.neon-sign` | `opacity` drops to 0.4 at 93% and 0.7 at 96% of the 8s cycle. `infinite`. |
| `livePulse` | `.live-dot` | `opacity 1→0.4`, `scale 1→0.6` at 50%. 2s, `infinite`. |
| `scrollDrop` | `.scroll-line` | ScaleY grows from top, then shrinks from bottom. 2s, `infinite`. |
| Canvas rain | `#rain-canvas` | 180 drops, length 6–24 px, speed 2–5 px/frame, opacity 0.05–0.30, slight diagonal. `requestAnimationFrame` loop. Canvas opacity: 0.35. |

### 3.8 Mobile Layout (max-width: 900 px)

| Element | Desktop | Mobile |
|---------|---------|--------|
| Hero | 2-column grid | Single column |
| `.script-col` | Visible | `display: none` |
| `.hero-rule` | `grid-column: 1 / -1` | `grid-column: 1` |
| `.hero-footer` | Horizontal flex | Column flex, items left-aligned, `gap: 2rem` |
| `.section-street` | 2-column grid (3fr / 2fr) | Single column, `gap: 3rem` |
| `.section-cta` | 2-column grid (1fr / 1fr) | Single column, `gap: 3rem` |
| `.pillars-grid` | 3-column grid | Single column |
| `.pillar` | Right border between columns | No right border; bottom border between rows; last child has no border |
| Manifesto `“ ”` | Visible CSS pseudo-elements | `display: none` |
| All touch targets | N/A | Minimum 44 × 44 px (WCAG 2.5.5) |

### 3.9 Accessibility

| Requirement | Implementation |
|-------------|----------------|
| Body text contrast (WCAG AA, 4.5:1) | `--text-primary` (`rgba(220,230,245,0.92)`) on `--void` (`#06080f`) passes. |
| Secondary text contrast | `--text-dim` (`rgba(180,200,230,0.45)`) on `--void` — verify with a contrast checker; adjust opacity upward if needed. |
| Decorative elements | All script column text, icons, SVGs, and the neon sign carry `aria-hidden="true"`. |
| Language | Visible Twi strings carry `lang="tw"` so assistive technology does not read them as English. |
| Flash rate (WCAG 2.3.1) | No animation flashes more than 3 times per second. `signFlicker` fires twice in 8 seconds. `flicker` fires twice in 6 seconds. Both compliant. |
| Reduced motion | `@media (prefers-reduced-motion: reduce)` sets all `animation-duration` and `transition-duration` to `0.01ms`. Canvas rain stops (check `matchMedia` before starting the loop). |
| Custom cursor fallback | If JS is disabled or `prefers-reduced-motion` is active, native cursor is restored. |

---

*End of Site Contract*
