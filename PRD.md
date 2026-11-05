# Product Requirements Document
### 3 AM in Tokyo — Static Site
*Version 2.0*
 
---
 
## 1. Vision
 
Deliver a single-page editorial site that places the visitor on a wet Tokyo street at 3 AM — the last train gone, neon bleeding into rain-soaked pavement, the city indifferent and beautiful. This is not a portfolio or a product page; it is an atmospheric experience first, with content that deepens the world rather than describing it. Every section earns its place by advancing that feeling.
 
---
 
## 2. User Personas
 
**The Nocturnal Drifter**
A design-aware individual who browses at odd hours seeking aesthetic experiences. They judge a site within seconds on mood, not utility, and share compelling discoveries on social platforms.
 
**The Hiring Manager / Client**
A creative director or potential collaborator evaluating taste and craft. They are looking for evidence of intentionality — that design decisions were made, not defaulted to. The depth of editorial content signals that this is not a template.
 
---
 
## 3. Feature List
 
### Must-Have *(static site constraints apply)*
- Single HTML file deployable to any static host (GitHub Pages, Netlify, Vercel) with zero build step.
- Five-section page: Hero, The Street, Three Pillars, Manifesto, Contact — in that order.
- Two-column hero with a large time stamp, a vertical kanji column, prose headline, sub-copy, dual CTAs, and a status bar (last train, next train, status, temperature).
- Canvas rain animation fixed behind all content.
- Custom cursor: a small cyan dot with a lagging ring that expands on interactive elements.
- Noise grain overlay via inline SVG filter at low opacity.
- Neon gradient bleed (pink from lower-left, cyan from upper-right) on the hero.
- Scroll-reveal: all sections below the hero fade and translate up on intersection.
- Reflection strips between sections: single-pixel horizontal rules with a neon gradient.
- Fully responsive layout; kanji column hidden below 900 px, grids collapse to single column.
- Performance baseline: Lighthouse score ≥ 90 on mobile.
- All assets self-contained or loaded from Google Fonts CDN; no auth required.
### Should-Have
- Neon sign card in The Street section with a flicker animation and reflection gradient.
- Pillar hover states: bottom border animates in from left using each pillar's accent colour.
- Photographic background layer in the hero (dark-overlaid, treated as atmosphere not content).
- Favicon matching the site palette.
### Nice-to-Have
- Time-aware stamp: JS reads the visitor's local clock and replaces the hard-coded time.
- Ambient audio toggle (looped rain + distant train sounds), off by default.
- A CSS-only parallax depth effect on background gradient layers.
---
 
## 4. Technical Constraints
 
- No backend, no database, no server-side rendering, no authentication layer.
- No Node.js build pipeline; output is a single `.html` file with embedded `<style>` and `<script>`.
- No client-side frameworks; vanilla HTML, CSS, and JavaScript only.
- All network requests must be to public CDNs or same-origin assets; no private API calls.
- Must render correctly without JavaScript enabled — all content visible, CTAs functional.
- Maximum total page weight: 500 KB uncompressed (excluding optional audio assets and photography).
---
 
## 5. Design Standard Summary
 
The visual language is urban nocturne: near-black backgrounds with pink, cyan, violet, and amber neon accents used as the only light sources — signs in the distance, not foreground decoration. Typography pairs Noto Serif JP (editorial weight, headlines and body) with Space Mono (monospaced precision, labels and UI copy). Motion is slow and deliberate — everything eases out, nothing snaps — and rain falls continuously behind every section. See `design-standard.md` for the complete specification.
 
---
 
## 6. Success Criteria
 
- A first-time visitor describes the emotional experience before describing the content.
- The page deploys from a single drag-and-drop to Netlify with no configuration or build errors.
- Lighthouse Performance ≥ 90 and Accessibility ≥ 80 on a simulated mid-range mobile device.
- Colour contrast on all body text meets WCAG AA (4.5:1) despite the dark palette.
- The design reads as intentional and cohesive on screens from 375 px to 1920 px wide.
- No external dependencies require an account, API key, or server-side request.