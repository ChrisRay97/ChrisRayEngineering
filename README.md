# CR Engineering — Personal Website Template

A dark, minimal multi-page website template for consultants and engineers. Serves as a project database, product catalog, and resume in one cohesive site.

---

## Structure

```
/
├── index.html                    Home / landing page
├── about.html                    Resume, skills, experience, education
├── contact.html                  Contact form + social links
├── styles.css                    Shared design system — all CSS lives here
├── nav.js                        Hamburger menu toggle (shared by all pages)
├── catalog/
│   ├── index.html                Product catalog with search + filter
│   └── product-template.html    Single product detail page
└── projects/
    ├── index.html                Project archive with search + filter
    └── project-template.html    Single project detail page
```

For each new product or project, **duplicate the relevant template** and fill in your content. There is no build step — the site is plain HTML, CSS, and vanilla JS.

---

## Getting Started

1. Open `index.html` in a browser to preview the site locally (no server required).
2. Find every `[placeholder]` (surrounded by square brackets) and replace it with your content. A project-wide find-and-replace works well for recurring values like your name and brand.
3. Update navigation `href` links if you rename any files.
4. Point the contact form `action` attribute at your form handler (Formspree, Netlify Forms, etc.).

### Key placeholders to replace globally

| Placeholder | What to put there |
|---|---|
| `[Your Name / Brand]` | Your name or business name |
| `[Your Brand Name]` | Short brand label used in nav eyebrows |
| `[your@email.com]` | Your email address |
| `[City, State / Region]` | Your location |

---

## Pages

### `index.html` — Home
Hero section with headline, subtext, and two CTAs. Below it, a 3-card grid of featured projects pulled from your projects directory. Update the three `.project-card` elements to link to your real project pages.

### `about.html` — About / Resume
- **Bio statement** — one paragraph intro
- **Resume download** — link a PDF via the `href` on `.resume-btn`
- **Skills** — three columns, one per domain; add/remove columns and list items freely
- **Experience timeline** — one `.tl-entry` per role, most recent first
- **Education** — one `.edu-block`; duplicate if you have multiple entries
- **Certifications** — one `.cert-row` per cert; add/remove rows as needed

### `contact.html` — Contact
Left column: email, location, availability, and social links. Right column: a form with name, email, inquiry type, and message fields. Wire up the `<form action="">` to your backend or a form service.

### `catalog/index.html` — Catalog
Filterable product grid. Filters: Domain (Electrical / Mechanical / Software) and Tier (Hobbyist / Commercial). Search and sort (Newest / A–Z) are also wired up. Each `.pcard` needs four `data-` attributes — see the comments in the file.

### `catalog/product-template.html` — Product Detail
Duplicate this file for each product. Contains:
- Tier badge + domain tags
- Image gallery with thumbnail swap
- Description paragraphs
- Specs block (2-column grid)
- Downloads list
- Purchase section — use `.buy-strip` for hobbyist/storefront products, `.quote-strip` for commercial/quote-request products (swap via the HTML comment in the file)

### `projects/index.html` — Projects
Same filter/search system as the catalog. Filters: Domain and Status (Active / Complete). Each `.pcard` needs `data-domains`, `data-status`, `data-name`, `data-date`, and `data-updated` attributes.

### `projects/project-template.html` — Project Detail
Duplicate this file for each project. Contains:
- Status badge + domain tags + meta row (created / updated / version)
- External links bar (GitHub, YouTube, Docs — remove any that don't apply)
- Freeform writeup with `<h3>` subheadings and optional inline images
- Image gallery (6-cell grid)
- Files & downloads list
- Changelog

---

## Adding Content

### New project
1. Duplicate `projects/project-template.html` and rename it (e.g. `projects/my-project.html`).
2. Fill in all `[placeholders]`.
3. Add a `.pcard` entry to `projects/index.html` pointing to the new file.
4. Optionally add a featured card on `index.html`.

### New product
1. Duplicate `catalog/product-template.html` and rename it (e.g. `catalog/my-product.html`).
2. Fill in all `[placeholders]`. Choose either `.buy-strip` or `.quote-strip` for the purchase section.
3. Add a `.pcard` entry to `catalog/index.html` pointing to the new file.

### Adding images
- **Product gallery**: replace the `.img-primary` placeholder content with `<img src="..." alt="...">` and populate each `.img-thumb`'s `data-src` attribute with the image path. The thumbnail click handler is already wired up.
- **Project gallery**: replace `.gallery-cell` placeholder content with `<img src="..." alt="...">`.
- **Inline writeup images**: place an `<img>` inside `.inline-img` and add a `.inline-img-caption` below it.

A suggested folder for images: `assets/img/[project-or-product-name]/`.

---

## Mobile & Responsive Design

The site is fully responsive with two breakpoints:

| Breakpoint | Behavior |
|---|---|
| ≤ 900px (tablet) | Card grids drop from 3 columns to 2 |
| ≤ 640px (mobile) | Card grids drop to 1 column; specs block, contact layout, and form rows stack vertically; image thumbs go to 2 columns |

### Navigation
On screens ≤ 640px the desktop nav links and Contact CTA are hidden and replaced by a hamburger button. Tapping it opens a full-width dropdown anchored below the sticky nav bar. Tapping the button again or anywhere outside closes it. The toggle logic lives in `nav.js`, which is included at the bottom of every page.

When adding a new page, copy the nav markup from any existing page and include `<script src="../nav.js"></script>` (or `nav.js` for root-level pages) before `</body>`.

### Hero headline
The hero headline uses `clamp()` for fluid typography — it stays at 54px on wide screens and scales down proportionally to always fill the available content width without wrapping:

```css
font-size: clamp(16px, calc((100vw - 80px) / 11), 54px);
```

---

## Design System

All styles are in `styles.css`. Do not add page-specific `<style>` blocks — put new classes in the shared file.

### Colors

| Token | Value | Use |
|---|---|---|
| Background | `#0F1012` | Page / body background |
| Surface | `#141618` | Cards, inputs, file rows |
| Surface raised | `#181A1C` | Specs block |
| Accent (gold) | `#C8922A` | Brand color, CTAs, section headings |
| Text primary | `#E8E6DF` | Headlines |
| Text secondary | `rgba(255,255,255,0.5)` | Body copy |
| Text muted | `rgba(255,255,255,0.28)` | Captions, notes |
| Border | `rgba(255,255,255,0.07)` | Card and row borders |

### Domain colors

| Domain | Color | Hex |
|---|---|---|
| Electrical | Green | `#8DB84A` |
| Mechanical | Orange | `#D95F2B` |
| Software | Teal | `#3DAFB8` |

Apply domain colors using the `.dtag-elec`, `.dtag-mech`, and `.dtag-soft` utility classes on `.dtag` elements.

### Typography

| Family | Weights | Use |
|---|---|---|
| IBM Plex Sans | 300, 400, 500 | Headlines, titles, roles |
| IBM Plex Mono | 400, 500 | Dates, versions, file names, meta values |
| Barlow | 300, 400, 500 | Body copy, descriptions, notes |
| Barlow Condensed | 400, 500, 600 | Labels, badges, tags, nav, buttons |

### Icons
Uses [Tabler Icons](https://tabler.io/icons) loaded via CDN. Find icon names at tabler.io/icons and use them as `<i class="ti ti-[name]">`.

---

## Dependencies

All loaded via CDN — no `npm install` required.

- [Google Fonts](https://fonts.google.com) — IBM Plex Sans, IBM Plex Mono, Barlow, Barlow Condensed
- [Tabler Icons](https://tabler.io/icons) — icon webfont (`@tabler/icons-webfont`)

For production, consider self-hosting these assets to avoid CDN availability risk.

---

## Deployment

The site is static HTML and can be hosted anywhere:

- **GitHub Pages** — push to a repo and enable Pages in repository settings
- **Netlify** — drag the project folder into the Netlify dashboard
- **Vercel** — connect repo or deploy via the Vercel CLI
- **Any static host** — upload files via FTP or your host's file manager

No build step, no framework, no dependencies to install.
