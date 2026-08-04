# C-Aesthetics — Shopify Theme

A custom Shopify **Online Store 2.0** theme for **C-Aesthetics**, a dermatologist-informed
skincare and wellness brand. Built on top of [Dawn](https://github.com/Shopify/dawn),
Shopify's reference OS 2.0 architecture, with brand-specific styling, homepage sections,
and a custom testimonials component.

Design direction is inspired by [skinclinic.es](https://skinclinic.es/en/) — a clean,
product-led skincare storefront — reinterpreted with original C-Aesthetics branding,
copy, and color palette (no assets, text, or trademarks were copied from that site).

## Why Dawn as the base

Dawn is Shopify's own reference implementation of OS 2.0: JSON templates, section
groups, native section/block architecture, and code that already meets Shopify's
performance and accessibility bars (Lighthouse ~95+, WCAG 2.1 AA). Starting here —
rather than from scratch — means the store inherits a maintained, audited foundation
instead of reinventing infrastructure Shopify already solved well.

## What was customized

| Area | Change |
|---|---|
| `config/settings_data.json` | New color schemes (warm neutral / blush / charcoal / gold / sage), typography (Cormorant serif headings, Jost body), card & button styling |
| `config/settings_schema.json` | Theme name/author metadata |
| `sections/header-group.json` | Two-line rotating announcement bar |
| `sections/footer-group.json` | Dark footer with brand block, shop links, support links, contact block |
| `sections/testimonials.liquid` (new) | Custom OS 2.0 section: star ratings, responsive grid, fully theme-editor configurable |
| `assets/section-testimonials.css` (new) | Scoped styles for the testimonials section, using the theme's existing CSS custom properties |
| `templates/index.json` | Full homepage: hero, shop-by-category, brand story, best sellers, technology spotlight, "why choose us," testimonials, newsletter |
| `templates/page.about-us.json` (new) | Alternate page template for an About page |
| `templates/page.faq.json` (new) | Alternate page template with an FAQ accordion |
| `templates/page.contact.json` | Heading added to the built-in contact form |

Everything else (product page, cart, collection grid, search, accessibility behavior,
JS components) is unmodified Dawn — battle-tested and already compliant.

## Architecture (Online Store 2.0)

```
layout/            Theme wrapper (theme.liquid, password.liquid)
templates/          JSON templates (index, product, collection, page, cart, 404, etc.)
templates/customers/  Customer account templates
sections/           Reusable, theme-editor-configurable Liquid sections
sections/*-group.json  Section groups for header/footer (OS 2.0 static sections)
snippets/            Reusable Liquid partials
assets/             CSS, JS, SVG icons — no build step required
config/             settings_schema.json (theme editor options) + settings_data.json (saved values)
locales/            Storefront + schema translations (all Shopify-supported languages included)
```

No bundler, no compiled CSS/JS — this is intentional. Dawn (and this theme) ships
plain Liquid, CSS, and vanilla JS with native ES modules and web components, which is
why it hits high Lighthouse scores out of the box.

## Getting started

### Prerequisites
- A Shopify store (any plan that supports custom themes)
- [Shopify CLI](https://shopify.dev/docs/api/shopify-cli) (`npm install -g @shopify/cli`)

### Local development
```bash
shopify theme dev --store your-store.myshopify.com
```
This serves the theme locally with hot reload against your store's data.

### Push to a store (without publishing)
```bash
shopify theme push --store your-store.myshopify.com --unpublished --json
```

### Pull settings made in the Theme Editor back into this repo
```bash
shopify theme pull --store your-store.myshopify.com
```

## Required store setup

The theme references content that lives in the Shopify Admin, not in this repo.
Before the homepage looks complete, create:

**Collections** (handles used in `templates/index.json`):
- `facial-care`
- `body-care`
- `anti-aging`
- `supplements`
- `best-sellers`

**Navigation menus** (Admin → Content → Menus): `main-menu` and `footer` are created
by default on new stores — populate them with your pages/collections.

**Pages**: create an "About Us" page and assign it the `page.about-us` template, and
an "FAQ" page assigned the `page.faq` template (Theme template picker, in the page editor).

**Images**: the hero banner, category tiles, and technology spotlight ship with no
image selected (by design — no stock/placeholder imagery was invented for a real brand).
Add real photography via the Theme Editor.

**Footer contact block**: update the placeholder email in `sections/footer-group.json`
(or directly in the Theme Editor) with your real contact details before launch.

See `store-setup/README.md` for a fuller content checklist and a sample product CSV.

## Performance & accessibility

- Semantic HTML landmarks, skip-to-content link, visible focus states (inherited from Dawn)
- All interactive components (menus, cart drawer, accordions, modals) are keyboard-operable
- Images use responsive `srcset`/`sizes` and native lazy-loading
- No render-blocking JS: all scripts load with `defer` or as native ES modules
- New custom code (`testimonials.liquid`) follows the same scoped-CSS, `color_scheme`-token
  pattern as the rest of the theme, and was checked for WCAG AA contrast (all palette
  pairings verified ≥ 4.5:1, most ≥ 10:1)
- Linted with `shopify theme check` — 0 errors, 0 warnings on all new/modified files

Run the linter yourself any time with:
```bash
shopify theme check
```

## License

Derived from Shopify's Dawn theme (MIT-style license restricted to Shopify-integrating
themes — see `LICENSE.md`). Original C-Aesthetics content, copy, and section code are
provided as part of this project.
