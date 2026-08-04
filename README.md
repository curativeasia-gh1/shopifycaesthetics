# C-Aesthetics — Shopify Theme

A Shopify **Online Store 2.0** theme for **C-Aesthetics**, managed by **Curative Pte Ltd,
Singapore** — a clinical dermocosmetics and professional aesthetics storefront covering
pathology-focused skincare, exosome-based solutions, microneedling and NAD+ wellness
products.

Built on [Dawn](https://github.com/Shopify/dawn), Shopify's reference OS 2.0
architecture (JSON templates, section groups, native accessibility/performance
baseline), customized for C-Aesthetics per `C-AESTHETICS-SHOPIFY-INSTRUCTIONS.md` and
`C-AESTHETICS-CONTENT-PAGES.md`. Design direction takes conceptual cues from
[skinclinic.es](https://skinclinic.es/en/) — restrained clinical presentation, editorial
type, generous white space — reinterpreted with an original C-Aesthetics identity. No
text, imagery or layout was copied from any reference site.

## What was customized

| Area | Change |
|---|---|
| `config/settings_data.json`, `settings_schema.json` | Clinical color system (deep ink `#092238`, mineral blue `#114F77`, pale aqua `#DCEEF0`, clinical grey `#F4F7F6`), Playfair Display / Inter typography, new "Organization & compliance" settings group |
| `layout/theme.liquid` | Renders `organization-schema.liquid` for `Organization`/`WebSite` JSON-LD |
| `sections/breadcrumbs.liquid` + `snippets/breadcrumbs.liquid` | Accessible breadcrumb trail + `BreadcrumbList` JSON-LD, added to product/collection/page/article templates |
| `sections/trust-strip.liquid` | 4-point editable trust strip |
| `sections/concern-grid.liquid` | "Shop by skin concern" card grid |
| `sections/advanced-categories.liquid` | Exosome / Microneedling / NAD+ editorial cards |
| `sections/faq-accordion.liquid` | Visible FAQ accordion with matching `FAQPage` JSON-LD (schema only ever mirrors rendered content) |
| `sections/editorial-article.liquid` | Reusable long-form content section (heading/richtext/columns/notice/CTA blocks) used for all static editorial pages |
| `sections/product-metafield-tabs.liquid` | Product-info accordion sourced entirely from `custom.*` metafields; each row renders only when populated |
| `snippets/professional-badge.liquid` | "Professional use only" badge, wired into product cards and the PDP title block, driven by `custom.professional_only` |
| `templates/index.json` | Full homepage per the spec: hero → trust strip → shop-by-concern → featured products → advanced categories → "C-Aesthetics standard" → Skin Journal → FAQ → newsletter |
| `templates/page.about-c-aesthetics.json`, `page.who-we-are.json`, `page.skinclinic.json`, `page.ingredients.json`, `page.faq.json`, `page.skinclinic-faq.json` | The five content pages from `C-AESTHETICS-CONTENT-PAGES.md`, plus a general site FAQ |
| `sections/header-group.json`, `footer-group.json` | Announcement bar copy, footer brand/shop/learn link lists and professional-use notice block |

Everything else (cart, search, account templates, JS components, accessibility
behavior) is unmodified Dawn.

## Architecture (Online Store 2.0)

```
layout/     Theme wrapper (theme.liquid, password.liquid)
templates/  JSON templates — index, product, collection, page.*, article, cart, etc.
sections/   Reusable, theme-editor-configurable Liquid sections
snippets/   Reusable Liquid partials (breadcrumbs, professional-badge, organization-schema)
assets/     CSS/JS/SVG — no build step
config/     settings_schema.json (editor options) + settings_data.json (saved values)
locales/    Storefront + schema translations
store-setup/  Merchant-facing setup guides (see below) — not theme code, doesn't render
```

No bundler, no compiled CSS/JS — intentional, per the project's performance requirements.

## Before this goes live

Two things live outside theme code and have to be set up in Shopify Admin — guides for
both are in `store-setup/`:

1. **`store-setup/metafields-setup.md`** — the `custom.*` product metafield and
   metaobject definitions the theme reads (e.g. `professional_only`, `short_benefit`,
   `how_to_use`). Nothing breaks if these are left empty; the relevant UI rows just
   don't render.
2. **`store-setup/navigation-setup.md`** — the `main-menu` and `footer` menu structure,
   plus the exact page handles/templates to use when creating each content page in
   Admin.

Also still outstanding, called out explicitly in the source instructions rather than
guessed at here: final Curative Pte Ltd business details (address, UEN, contact
emails/phone), shipping/returns/privacy/terms policy text, product catalogue data,
and licensed photography — all placeholders until Curative confirms them.

## Verification run so far

- `python3 -m json.tool` across all templates/sections/config/locale JSON — valid
- `shopify theme check` — **0 errors**, 8 pre-existing Dawn warnings (none in files this
  project touched)
- Not yet done: Lighthouse pass (should be re-run once real imagery and apps are
  installed, per the project's own acceptance criteria)

## Deploying

This repo is prepared locally with `origin` set to
`https://github.com/curativeasia-gh1/shopifycaesthetics.git` but has **not** been
pushed — pushing requires your GitHub credentials, which aren't something this
assistant accepts pasted into chat. See the accompanying message for a one-command
push once you've downloaded the packaged repo.
