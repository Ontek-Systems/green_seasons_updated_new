# Green Seasons - Project Context & Rules

## 1. Business Overview
- **Brand:** Green Seasons
- **Description:** A second-generation, owner-led garden and grounds maintenance business run by Tim Harris. Based in Oxfordshire, UK. Fully insured, 5-Star Google rated.
- **Owner:** Tim Harris — second-generation gardener born and raised in Oxford. Always on site.
- **Services:**
  - Lawn Care & Renovation (Seasonal Fertiliser, Weed & Moss Control, Aeration & Scarification, Full Lawn Renovations)
  - Grounds Maintenance (Routine Grass Cutting, Strimming & Edging, Site Presentation)
  - Hedge & Shrub Care (Regular Trimming, Expert Shaping, Plant Health Care)
  - Planting & Design (Plant Supply & Sourcing, Custom Planting Schemes, Bespoke Border Design)
  - Specialist Treatments (Wetting Agents, Slow-Release Nutrition, Soil Resilience)
  - Site Clearance & Recovery (Initial Reset Visits, Full Site Clearance, Overgrown Recovery)
  - Weed Control (Certified Herbicide, Lawn Weed Management, Hard Surface Treatment)
- **Clients:** Private homeowners, private estates, residential developments, commercial sites, public/community spaces
- **Locations / Service Areas:** Oxford, Abingdon, Didcot, Wantage, Witney, plus 20 location pages covering: Botley, Burford, Carterton, Chalgrove, Chipping Norton, Eynsham, Faringdon, Grove, Highworth, Kidlington, Lechlade, Swindon, Wallingford, Woodstock, Yarnton — all across Oxfordshire
- **Contact:** Phone 07545 285408 | Email green-seasons@hotmail.com | 9 Morris Drive, Oxfordshire OX13 5GW
- **Domain:** https://www.green-seasons.co.uk/

---

## 2. Tech Stack & Architecture
- **Framework:** Static HTML — no build step, no React, no Next.js, no npm
- **Styling:** Tailwind CSS v4 via CDN browser build (`unpkg.com/@tailwindcss/browser@4.3.0`) + custom `style.css`
- **JavaScript:** Vanilla JS only (`global.js` — component loading, nav, scroll animations)
- **Key Dependencies:** None (no package.json). External: Google Fonts (DM Sans), Tailwind CDN
- **Fonts:** Self-hosted Marcus Traianus OTF family (`/assets/fonts/`) + Google Fonts DM Sans
- **Folder Structure:**
  - `/` — `index.html`, `style.css`, `global.js`, `CLAUDE.md`, `404.html`, config files
  - `/components/` — `header.html`, `footer.html` (async-loaded client-side by global.js)
  - `/pages/` — subpages: `about.html`, `services.html`, `contact.html`, `gallery.html`, `testimonials.html`, `commercial.html`, `where-we-serve.html`, etc.
  - `/pages/services/` — 23 individual service detail pages
  - `/pages/locations/` — 20 location/SEO landing pages
  - `/assets/fonts/` — Marcus Traianus OTF files (regular, bold, extra-bold, italic)
  - `/assets/imgs/` — All images: `hero_slider/`, `service_imgs/`, `location_imgs/`, logos

---

## 3. Design System

### Colors
| Name | Hex | Use |
|---|---|---|
| Forest Green | `#668e78` | Primary brand, nav, buttons, accents |
| Dark Green | `#1a3528` | Body text, footer bg, dark sections |
| Gold / Bronze | `#db9f1b` | Hover states, CTA highlights, accent |
| White | `#ffffff` | Page backgrounds, light panels |
| Forest Light | `#82ab97` | Subtle tints |
| Forest Dark | `#4e7060` | Scrolled header bg |

**CSS Variables (`:root`):**
- `--midnight`, `--ocean`: `#668e78`
- `--ocean-light`: `#82ab97` | `--ocean-dark`: `#4e7060`
- `--bronze`: `#db9f1b` | `--alice`: `#ffffff`

**Semantic Tokens (light mode default, overridden by `.section-dark`):**
- `--gs-fg`: `#1a3528` | `--gs-fg-muted`: `rgba(26,53,40,0.80)` | `--gs-fg-subtle`: `rgba(26,53,40,0.60)`
- `--gs-bg`: `#ffffff` | `--gs-accent`: `#db9f1b` | `--gs-accent-alt`: `#668e78`
- `--gs-btn-bg`: `#db9f1b` | `--gs-btn-fg`: `#ffffff`

### Typography
- **Headings:** `'Marcus Traianus', 'Cinzel', Georgia, serif` (self-hosted OTF, weights 400/700/800/italic)
- **Body:** `'DM Sans', sans-serif` (Google Fonts, weights 300/400/500/600)
- `font-display: swap` on all custom fonts

### Breakpoints
Tailwind v4 defaults (mobile-first):
- `sm`: 640px | `md`: 768px | `lg`: 1024px | `xl`: 1280px | `2xl`: 1536px
- Mobile overrides at `max-width: 768px` in `style.css`

### UI Components (Token Classes — always use these, never hardcode colours)
| Class | Purpose |
|---|---|
| `.gs-tagline` | Eyebrow/label text — uppercase, letter-spaced, 1.25rem |
| `.gs-heading` | Section h2 — Marcus Traianus, fluid clamp(2.25rem→3rem), weight 900 |
| `.gs-body` | Paragraph text — DM Sans, fluid clamp(1rem→1.125rem), line-height 1.75 |
| `.gs-stat-label` | Stats captions — uppercase, 0.75rem, weight 700 |
| `.btn-adaptive` | Smart button — gold on light sections, ghost outline on dark sections |
| `.btn-primary` | Solid gold button — light backgrounds only |
| `.btn-ghost` | Outline white button — dark backgrounds only |
| `.btn-green-cta` | Solid green button |
| `.section-dark` | Add to `<section>` to flip all tokens to dark mode |
| `.reveal`, `.reveal-up`, `.reveal-left`, `.reveal-right`, `.reveal-scale` | Scroll-triggered reveal animations (managed by global.js IntersectionObserver) |
| `.delay-100` … `.delay-600` | Stagger delay classes for reveal animations |

---

## 4. Coding Conventions & Best Practices
1. **Use token classes, never hardcode.** Always use `.gs-heading`, `.gs-body`, `.btn-adaptive`, etc. for typography and buttons. Never write raw hex values in HTML attributes or inline styles for brand colours.
2. **Add `.section-dark` to flip a section dark** — all tokens (text, bg, buttons) adapt automatically. No manual colour overrides needed.
3. **Components load async.** `header.html` and `footer.html` are fetched and injected by `global.js`. Never duplicate nav/footer markup in page files.
4. **Scroll reveal is automatic.** Add `class="reveal reveal-up"` (+ optional `delay-*`) to any element; `global.js` handles the IntersectionObserver. No inline JS needed.
5. **Mobile-first layout.** Write base styles for mobile, override at `md:` / `lg:` Tailwind breakpoints. Check `style.css` mobile overrides (max-width: 768px) before adding new breakpoint overrides.
6. **No frameworks, no build.** All changes are live immediately — just save and reload in browser. Do not add npm packages, import statements, or module syntax.
7. **Page depth paths.** Pages in `/pages/` subdirectories reference assets with `../../` prefix. Do not change how `loadComponents()` in `global.js` resolves paths.

---

## 5. Working Rules

- Talk to me in plain English. Match effort to what I'm asking — no over-engineering.
- Act fast. Pick the obvious approach and go. Ask one short question if genuinely unsure.
- Smallest change that does the job. Don't refactor or improve things I didn't mention.
- After an edit, one line on what changed and where. That's it.
- Don't explain how HTML or CSS works unless I ask.
- Don't re-read files already read this session unless I say something changed.
- If I name a section, class, file, or ID — go straight there.

---

## 6. Current Development Goal
- **Task:** Create a new page and update existing components.
- **Status:** Planning phase.
