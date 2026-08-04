# Store setup checklist

This folder holds content that lives in **Shopify Admin data**, not in theme code —
it can't be pushed via `shopify theme push` and needs to be set up once per store.

## 1. Import sample products
`sample-products.csv` contains 10 example products across four categories, useful for
seeing the homepage and collection pages populated while you build out real catalog data.

**Admin → Products → Import → Upload `sample-products.csv`.**

Products ship with no images (none were invented for a real brand) — add real product
photography after import, or delete these and use them purely as a formatting reference
for your own CSV.

## 2. Create collections
The homepage (`templates/index.json`) references these collection handles. Create each
one under **Admin → Products → Collections**, matching the handle exactly so the theme
picks them up automatically:

| Handle | Suggested title | Suggested condition |
|---|---|---|
| `facial-care` | Facial Care | Product type is "Facial Care" |
| `body-care` | Body Care | Product type is "Body Care" |
| `anti-aging` | Anti-Aging | Product type is "Anti-Aging" |
| `supplements` | Supplements | Product type is "Supplements" |
| `best-sellers` | Best Sellers | Tagged "best-sellers" |

If you imported `sample-products.csv` first, these can all be automated (rule-based)
collections using the Type/Tag rules above.

## 3. Set up navigation
New Shopify stores come with `main-menu` and `footer` menus pre-created. Populate them
under **Admin → Content → Menus**:
- **Main menu**: Facial Care, Body Care, Anti-Aging, Supplements, About Us
- **Footer menu**: FAQ, Shipping & Returns, Refund Policy, Privacy Policy, Terms of Service

(Shopify auto-generates draft policy pages under **Settings → Policies** — link to those
from the footer menu once reviewed.)

## 4. Create pages with the right template
In **Admin → Content → Pages**, create:
- **About Us** — in the page editor's "Theme template" dropdown, choose `page.about-us`
- **FAQ** — choose `page.faq`
- **Contact** — create a page with the handle `contact`; Shopify automatically applies
  `page.contact.json` to a page with that handle

## 5. Update placeholder content before launch
- `sections/footer-group.json` → the "Contact" text block has a placeholder email
- Theme Editor → Theme settings → Social accounts (left blank; add your real profiles)
- Theme Editor → Logo (upload your real logo; `logo_width` is pre-set to 130px)
- Hero, category, and technology-spotlight images (none are set by default — see README)

## 6. Payments, shipping, taxes, domain
Standard Shopify Admin setup, outside the theme's scope — **Settings → Payments**,
**Settings → Shipping and delivery**, **Settings → Taxes**, **Settings → Domains**.
