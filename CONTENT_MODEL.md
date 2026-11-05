# Content Model
### 3 AM in Accra — Static Site
*Version 3.0 — Accra adaptation*

---

## Page Sections (in order)

---

### 0. Document Metadata

| Field | Value | Constraints |
|-------|-------|-------------|
| `page_title` | Trotro a ɛtwa to — Last Trotro | Max 60 characters. Evocative, not descriptive. |
| `meta_description` | 3 AM in Accra: the last trotro gone, neon on wet tar, a site that lives in the interval. | Max 155 characters. One sentence. Reads like a caption. |

---

### 1. Hero

Two-column layout. Left column: time stamp, headline, sub-copy, dual CTAs. Right column: large vertical Twi word. Bottom: status bar.

#### Stamp (top-left)
| Field | Value | Constraints |
|-------|-------|-------------|
| `stamp_time` | 03:17 | 5-character time string. Hard-coded or JS-replaced with visitor's local time. |
| `stamp_location` | Kwame Nkrumah Circle, Accra | Plain text. Displayed with a cyan rule prefix. |

#### Main copy (left column)
| Field | Value | Constraints |
|-------|-------|-------------|
| `eyebrow` | // nkran anadwo — last trotro gone | Micro-label. Pink neon colour. All caps via CSS. Meaning of the Twi: *Accra, night*. |
| `headline` | You are somewhere between here and where you meant to be. | Noto Serif, weight 300. `here` rendered as outlined cyan text. Max 2 lines. |
| `sub_copy` | Rain has been falling for an hour and the station is empty, the mates gone home hoarse. Every sign still lit is brighter now, burning into water, into nothing. This is the city at its most honest. | Max 3 sentences. Tone: cinematic, observational. Displayed with a left pink border. |
| `cta_primary_label` | Stay in this moment | 3–6 words. Quiet imperative. Scrolls to `#manifesto` or functions as thematic anchor. |
| `cta_secondary_label` | Find your way | 2–4 words. Ghost style. Scrolls to `#contact`. |

#### Script column (right column, hidden mobile)
| Field | Value | Constraints |
|-------|-------|-------------|
| `script_main` | Anadwo | Meaning: *night*. Rendered vertically in Noto Serif weight 200. Visual texture only — `aria-hidden="true"`. |
| `script_sub` | Nkran — 03:17 | Meaning: *Accra, 3:17 AM*. Small, widely tracked, ghost opacity. `aria-hidden="true"`. |

#### Status bar (full-width, bottom of hero)
| Field | Value | Constraints |
|-------|-------|-------------|
| `status_last_trotro` | 23:40 — to Madina | Plain text. Label: *Last trotro*. |
| `status_next_trotro` | 04:30 — once it fills | Plain text. Label: *Next trotro*. |
| `status_current` | Waiting | Displayed with a pulsing cyan dot. Label: *Status*. |
| `status_temp` | 24°C / rain | Plain text. Label: *Temp*. |

---

### 2. The Street

Two-column layout: editorial prose left, neon sign card right.

#### Text column
| Field | Value | Constraints |
|-------|-------|-------------|
| `heading_line_1` | The city never stops. | Noto Serif weight 200. |
| `heading_line_2` | It just changes audience. | Same size, amber neon colour with glow. Italic. |
| `body_1` | After midnight, Accra belongs to the stragglers, the night watchmen, the young couples counting cedis for a taxi. The generators hum and highlife thins out from a spot you cannot see. A food seller's bulb throws warm orange light across the wet tar and no one notices because everyone is somewhere else in their mind. | Max 4 sentences. Tone: observational, unhurried. |
| `body_2` | There is a particular loneliness to being awake in a city where, by daylight, nobody is ever left alone. Not painful loneliness — the kind that makes you feel specific, real, briefly unlike everyone you know. | Max 3 sentences. Tone: reflective. |

#### Neon sign card
| Field | Value | Constraints |
|-------|-------|-------------|
| `sign_name` | Nyame Bɛkyerɛ | Meaning: *God will show the way*, an everyday shop and trotro slogan used here as the name of a fictional drinking spot. Rendered in Noto Serif, pink neon glow, flicker animation. |
| `sign_meta` | drinking spot — est. 1978 / open until 5am | Two lines. Small, ghost colour, all-caps via CSS. |

---

### 3. Three Pillars

Three-column grid. Each pillar has a number, SVG icon, heading, and body copy.

| Pillar | `number` | `heading` | `body` | Accent colour |
|--------|----------|-----------|--------|---------------|
| 01 | — 01 | Solitude as signal | By day this city will not let you be alone: someone is always calling you over, selling you something, asking after your mother. The quiet between yourself and others is where you hear what you actually think. | Pink (`--neon-pink`) |
| 02 | — 02 | Reflection as truth | A sign in a puddle doesn't lie the way it does on the wall. The reflection strips away the slogan and gives you only light — only colour — only shape. | Cyan (`--neon-cyan`) |
| 03 | — 03 | Waiting as practice | Every missed trotro is a rehearsal for the larger delays. This city teaches patience: nothing here leaves until it is full. There is always a next one, and the question is what you do with the interval. | Amber (`--neon-amber`) |

Each pillar's SVG icon is a minimal geometric mark in its accent colour. Icons are decorative — `aria-hidden="true"`.

---

### 4. Manifesto

Centred, full-width quote section.

| Field | Value | Constraints |
|-------|-------|-------------|
| `quote` | Accra at 3am is not sleeping. It is simply between versions of itself — the one it was and the one it will be by morning. | Noto Serif weight 200. Large display size. Flanked by quotation marks “ ” as CSS pseudo-elements. |
| `attribution` | // nkran anadwo — intermezzo of the city | Ghost colour. All-caps via CSS. Small, wide tracking. |

---

### 5. Contact

Two-column layout: heading and prose left, `mailto:` link right. No form submission to a backend.

| Field | Value | Constraints |
|-------|-------|-------------|
| `heading` | Let us find you when morning comes. | Noto Serif weight 300. Max 2 lines. |
| `body` | Leave your signal in the rain. We'll know where to look. Dispatches from this hour, sent before the city wakes — sometimes a map, sometimes just a frequency. | Max 3 sentences. Tone: atmospheric, not transactional. |
| `contact_link_label` | hello@[yourdomain] | Visible email address or label such as *Send a message*. Renders as `mailto:` link. |
| `contact_href` | `mailto:hello@[yourdomain]` | Valid `mailto:` URI. No form handler. **Must be filled before build.** |

> **Note:** The HTML reference includes form inputs (email, city) and a submit button. These are retained as visual elements for atmosphere but must not submit to a backend. If a functional email capture is required, this constraint must be revisited and the PRD updated.

---

### 6. Footer

| Field | Value | Constraints |
|-------|-------|-------------|
| `logo` | Nkran Anadwo | Meaning: *Accra, night*. Noto Serif weight 300. Ghost colour. `aria-hidden="true"` if purely decorative. |
| `links` | Archive / About / Dispatch / Contact | Four anchor links. All-caps via CSS. Ghost colour, pink on hover. Destinations TBD or anchor links within page. |
| `copyright` | © 2026 — 03:17 | Small, ghost colour, widely tracked. Year may be JS-generated. |
