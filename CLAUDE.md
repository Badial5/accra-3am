# CLAUDE.md
### 3 AM in Accra — Static Site

---

## Project Identity

This is a single-page editorial site built around one brief: *3 AM in Accra. You've just missed the last trotro. Neon reflections on wet pavement.* It is an atmospheric experience first — five sections of prose, imagery, and Twi typography that place the visitor in a specific moment in a specific city. Every technical and visual decision serves that feeling before anything else.

---

## Technical Stack

- **Output:** one `.html` file with embedded `<style>` and `<script>` blocks
- **Languages:** vanilla HTML, CSS, and JavaScript only
- **Fonts:** Noto Serif, Space Mono, Noto Sans — loaded via Google Fonts CDN
- **Constraints:** no frameworks, no npm, no build tools, no backend, no database, no authentication, no private API calls

---

## Supporting Documents

| Document | Description | Read when |
|----------|-------------|-----------|
| `design-standard.md` | Complete visual specification: colour tokens, typography scale and rules, spacing system, texture and layer stack, interaction timing and keyframes, accessibility floor. | Making any visual or CSS decision. |
| `site-contract.md` | Page structure in render order, full content inventory for all six sections, and behaviour spec covering the cursor, scroll, hover states, entrance and ambient animations, and mobile layout. | Before writing any HTML structure or JavaScript behaviour. |
| `content-model.md` | Every content field with its specified value and constraints, across all sections from document metadata to footer. | Filling in any text, label, href, Twi string, or metadata value. |
| `PRD.md` | Vision, personas, feature list (Must-Have / Should-Have / Nice-to-Have), technical constraints, and success criteria. | Resolving a scope question or deciding whether a feature belongs in this build. |
