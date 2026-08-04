# Navigation setup

Shopify menus (`main-menu`, `footer`) are configured in **Online Store → Navigation** in
Admin, not in theme code, so they need to be created there. The header section is
already wired to the `main-menu` handle and the footer's `link_list` blocks point at
the `footer` handle (see `sections/header-group.json` and `sections/footer-group.json`).

## Main menu (`main-menu`)

**Shop**
- All Products → `/collections/all`
- Dermocosmetics → collection
- Exosome Solutions → collection
- Microneedling → collection
- NAD+ → collection
- Post-Procedure Care → collection
- New Arrivals → collection
- Best Sellers → collection

**Skin Concerns**
- Acne and Congestion
- Pigmentation and Uneven Tone
- Sensitivity and Redness
- Dryness and Barrier Support
- Fine Lines and Skin Ageing
- Dullness and Uneven Texture
- Post-Procedure Recovery

**Learn**
- Skin Journal → `/blogs/news`
- Ingredient Library → `/pages/ingredients`
- Procedure Guides
- Product Guides
- Frequently Asked Questions → `/pages/faq`

**Professionals**
- Professional Products
- Treatment Protocols
- Professional-Use Notices
- Trade Enquiry → `/pages/contact`

**About**
- Our Approach → `/pages/about-c-aesthetics`
- Curative Pte Ltd → `/pages/who-we-are`
- Contact → `/pages/contact`

## Footer menu (`footer`)

Keep this shorter than the main menu — footer link lists render as flat single-level
lists. Suggested split across the two footer `link_list` blocks already added
(`Shop` and `Learn`):

- Shop all products, Skin concerns, SkinClinic, About C-Aesthetics, Who We Are, Contact
- Skin Journal, Ingredient Library, FAQ, SkinClinic FAQ, Professional-Use Policy

Add Shipping Policy, Returns Policy, Privacy Policy and Terms of Service through
**Settings → Policies** — Dawn's footer renders these automatically via the
`show_policy` setting (already enabled) once they're published there, so they don't
need to be duplicated into the `footer` menu.

## Pages already built and ready to link

| Page | Template | URL |
|---|---|---|
| About C-Aesthetics | `page.about-c-aesthetics` | `/pages/about-c-aesthetics` |
| Who We Are (Curative Pte Ltd) | `page.who-we-are` | `/pages/who-we-are` |
| About SkinClinic | `page.skinclinic` | `/pages/skinclinic` |
| SkinClinic FAQ | `page.skinclinic-faq` | `/pages/skinclinic-faq` |
| Ingredient Library | `page.ingredients` | `/pages/ingredients` |
| Site FAQ | `page.faq` | `/pages/faq` |
| Contact | `page.contact` | `/pages/contact` |

When creating each page in Admin, set its handle to match the URL above and choose the
matching template from the **Template** dropdown in the page editor.
