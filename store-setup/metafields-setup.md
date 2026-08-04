# Metafields & metaobjects setup

Shopify metafield **definitions** and **metaobject definitions** live in the store's data
layer (Settings → Custom data), not in theme code, so they can't ship inside this repo.
Create the following in Shopify Admin before populating products. The theme already
reads every one of these — sections/product-metafield-tabs.liquid and
snippets/professional-badge.liquid render them only when a value is present, and hide
the row entirely when it's blank.

## Product metafields (namespace: `custom`)

| Key | Type | Purpose |
|---|---|---|
| `short_benefit` | Single line text | Product-card and above-fold one-line summary |
| `who_its_for` | Rich text | Suitable customer or skin profile |
| `skin_concerns` | List of metaobject references (`skin_concern`) | Concern relationships and filtering |
| `key_benefits` | List of single-line text | Scannable benefit list |
| `key_ingredients` | List of metaobject references (`ingredient`) | Ingredient education and internal linking |
| `how_to_use` | Rich text | Application instructions |
| `routine_step` | Single line text | Cleanse, treat, moisturise, protect, etc. |
| `professional_only` | Boolean | Drives the "Professional use only" badge on cards and PDP |
| `professional_notice` | Rich text | Safety and professional-use information (falls back to the theme-setting default when blank) |
| `evidence_summary` | Rich text | Substantiated evidence summary |
| `full_ingredients` | Multi-line text | Full INCI / ingredient list |
| `faq_items` | List of metaobject references (`faq_item`) | Product-specific Q&A |

## Recommended metaobjects

- `skin_concern` — fields: `title` (single line text), `handle`/`url` if you want the pill to link out
- `ingredient` — fields: `title`, `url` (link to the Ingredient Library entry)
- `faq_item` — fields: `question` (single line text, referenced as `custom.question`), `answer` (rich text, referenced as `custom.answer`)
- `clinical_evidence`, `protocol_step`, `professional_notice` — optional, for future structured evidence/protocol content referenced from `evidence_summary` or product descriptions

## How to create these

1. Shopify Admin → **Settings → Custom data → Products → Add definition** for each row above, under namespace `custom`.
2. Shopify Admin → **Settings → Custom data → Metaobjects → Add definition** for `skin_concern`, `ingredient`, `faq_item` (and the optional ones) with the fields listed.
3. Populate values per product. Anything left blank simply doesn't render — there's no need to fill in every field for every product before launch.
4. For bulk population, export/import via a matching app (e.g. Matrixify) rather than hand-entering hundreds of rows.

## Where each metafield surfaces in the theme

- `snippets/card-product.liquid` — `short_benefit`, `professional_only` (via `professional-badge.liquid`)
- `sections/main-product.liquid` — `short_benefit`, `professional_only` in the title block
- `sections/product-metafield-tabs.liquid` — everything else, as accordion rows on the product page (added automatically to `templates/product.json`)

## Settings-driven compliance text (no metafields needed)

These live under **Theme editor → Theme settings → C-Aesthetics: Organization & compliance**
and are used as store-wide defaults/fallbacks:

- Legal operating company / country / "managed by" statement → used in `snippets/organization-schema.liquid`
- Business registration number → left blank until Curative confirms it; only added to structured data when populated
- Standard educational disclaimer → shown at the base of `sections/product-metafield-tabs.liquid` and available for reuse on any editorial page
- Professional-use badge label / notice → default text for `professional_only` products that don't have a product-specific `professional_notice`
