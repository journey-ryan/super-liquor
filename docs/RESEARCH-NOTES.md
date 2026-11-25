# Research Notes

A summary of the `00 Notes` page in the Figma file: how the live site was captured, what was assumed, and the UX problems found. Captured 20 Oct 2026 from superliquor.co.nz (nopCommerce) and store subdomains such as avondale.superliquor.co.nz.

## Library at a glance

- **01 Captures:** 27 page templates, 64 frames (desktop 1440 and mobile 390).
- **02 Components:** 57 local components (34 components or component sets plus 23 icons), 94 variants, auto layout, bound to variables.
- **03 Foundations:** 4 variable collections (Primitives 23, Color 29, Spacing 14, Radius 5), 22 Barlow text styles, 3 effect styles.

## Templates captured

Age gate, store selector, home (national and store), nav and mega-menu, category listing, specials listing, search (results and no results), product detail (in stock and out of stock), gift card, store finder, store page, cart, checkout (step 1 and billing), login, register, account (logged out), Cashpoints microsite, Premium Spirits Club, mailer, blog, CMS content, contact, 404 and maintenance (503).

## Gaps

- Captures are screenshots, not editable layers. The editable rebuild is the component library.
- Checkout steps 2 to 5 weren't reached (it needs real personal details). Logged-in states weren't captured.
- Hover, focus and disabled states weren't on the live CSS sample, so those are Journey proposals.
- Pagination was never seen live; it's built from nopCommerce markup.

## Assumptions

- Store-scoped pages use **Super Liquor Avondale** (Auckland).
- Viewports: desktop 1440 x 900, mobile 390 x 844.
- Token names and semantic mapping are an interpretation of computed values. Light mode only.
- Pixel-sampled (not computed) values: page-title gradient end `#5BA3E0`, nav "Open" overlay, breadcrumb size, Outline/Block button padding, store card padding, toast text size. The level-2 filter indent was rounded to 25px.
- Logo, product, store and Cashpoints images are crops; replace them with source assets.
- The Cashpoints purple/yellow sub-brand isn't tokenised.

## UX observations (opportunities)

**Stock visibility**
- Stock is only signalled negatively (OUT OF STOCK). There's no in-stock, low-stock or "available at other stores" cue.
- Out-of-stock items sit unsorted among available ones.
- Without a store selected, national listings still show prices and ADD, so it's unclear which price or stock applies.

**Store finding**
- "Pick a store" is two dropdowns (Region, then Store). There's no suburb search or geolocation, and the list isn't alphabetical.
- Picking a store moves to a subdomain and shows the age gate again.
- The store finder lists all 193 stores on one long page, with no hours, distance or "shop this store".

**Delivery vs pickup**
- Labels are inconsistent ("Pick up & Delivery" vs "Order & Pick Up").
- The cart shows "Shipping: $0.00" before a choice is made.
- Pickup vs delivery is only chosen at checkout step 2, after a full billing address.
- Add to cart gives only a toast: no mini-cart, no fulfilment choice.

**Cashpoints**
- Loyalty is invisible in the core journey (not in nav, PDP, cart or checkout), with no earn messaging or balance.

**Other**
- 404s soft-redirect. Listings have no pagination or result count.
- Some mobile pages overflow horizontally (398px document at 390px).
- A floating notification bell overlaps content on every page.
