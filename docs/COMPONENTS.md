# Component Catalogue

Every component in the Figma library (`02 Components` page), with its variants, states and rules. Token names refer to [DESIGN.md](../DESIGN.md). "Proposal" marks Journey proposals pending client sign-off.

Naming: Figma uses `Group/Name` with properties `Property=Value`. In code, keep the same names (e.g. `Card/Product` becomes `CardProduct`, `Style=Primary` becomes `variant="primary"`).

---

## Brand

### Brand/Logo
148 x 38. Raster crop from the live site; swap for the source vector when available. Keep clear space of at least `spacing/10` around it.

### Icons
24 x 24 SVG, see DESIGN.md §8. Recolour via the glyph fill; default `--sl-color-brand-primary`.

---

## Actions & status

### Button
| Property | Values |
|---|---|
| Style | Primary, Promo, CTA, Outline, Block |
| State | Default, Hover, Pressed, Focus, Disabled, Loading |
| Icon | optional leading 20px icon |

| Style | Where it's used | Fill / border | Text |
|---|---|---|---|
| Primary | Listing ADD | `brand-primary` fill, 2px bottom border `action-primary-pressed`, `radius-sm`, padding 8/20 | Button/Default, inverse |
| Promo | PDP ADD | `promo` fill | Button/Default, inverse |
| CTA | Age gate Yes, Shop Now | `action-cta` fill, 4px bottom edge `action-cta-edge` | Button/Large, inverse |
| Outline | Cart secondary actions | 1px `border-brand`, transparent fill | brand blue |
| Block | Cart CHECKOUT | Full-width block | Button/Default |

- Default styling is **Live**. Hover, Pressed, Focus, Disabled and Loading are **Proposals** using `color/action/*`, `color/focus/*` and `color/text/disabled`.
- Interactions: Default to Hover while hovering; Default/Hover to Pressed while pressing. 150ms ease-out.
- Loading keeps the button width and disables clicks.

### Button/View Toggle
Grid / List icon toggle, 40 x 32. States: Active, Inactive (`bg-toggle`).

### Badge
| Type | Use |
|---|---|
| Multi-buy | 80 x 80 ribbon, top-left of a product card (e.g. "2 for $30"). Rebuilt with tokens from a live-site image. |
| Nav Specials | Red "Specials" pill in the nav. |
| Basket Count | 20 x 20 count bubble on the cart icon. |

### Price
| Size | Style |
|---|---|
| Card | Price/Large (SemiBold 24/36, -1px) in `text-price` |
| Cart | Smaller cart variant |

No was/now or strike-through pricing exists on the live site. Don't invent it without design sign-off.

### Stock Indicator
| Status | Look |
|---|---|
| Out of stock | Grey `bg-out-of-stock` block, Label/Status, replaces ADD |
| Store not selected | Inline message prompting the shopper to pick a store |

---

## Forms & search

### Form/Input
| Property | Values |
|---|---|
| Type | Text, Select |
| Content | Placeholder, Value |
| State | Default, Hover, Focus, Error, Disabled |
| Leading icon | optional: search, mailer, user, phone, pin, store |

320 x 38 default. Border `border-input` (`border-select` for selects), `radius-md`, padding `spacing-6`. Value text `text-input`; placeholder `text-placeholder`. Error uses `border-error`. Required and messages live on Form/Field, not the input.

### Form/Qty
60 x 39 quantity box beside ADD on product cards. 1px `border-strong`, Body/Default.

### Form/Field
| Property | Values |
|---|---|
| Layout | Stacked, Inline |
| Status | Default, Error |

Props: Label, Required (red `*`), Message, Helper text, Error text, nested Form/Input. Dev: `aria-required`, `aria-invalid`, `aria-describedby` pointing at the message.

### Search Bar
| Property | Values |
|---|---|
| Breakpoint | Desktop (402 wide), Mobile (360 wide) |
| State | Default, Focus, Filled |

### Search (combined) and Search/Panel
- **Search** states: Closed, Idle, Results, No results.
- **Search/Panel** (dropdown): Desktop Idle / Results / No results; Mobile Idle / Results. Elevation/Popover.
- **Search/Chip**: pill (`radius-full`) for "Top searched" terms. States: Default, Hover.
- **Search/Suggestion**: Type = Query, Recent, Category; State = Default, Hover.
- **Search/Product**: Type = Standard, Promo; State = Default, Hover. Shows store price.

Why it's categorised: most liquor searches are category intent ("gin", "rosé"), not a SKU. Categories route straight to a filtered listing, products sell with the store price, suggestions fix spelling. Recent and trending fill the empty state, so focus is never blank. Feed trending from live search analytics.

---

## Header & navigation

### Header/Desktop
1440 wide. Store = None | Selected. Three rows: utility bar (`bg-utility`, store status, phone), main (logo, search, store selector, header links), nav (Nav/Item row). Elevation/Header.

### Header/Mobile
390 wide. Store = None | Selected.

### Header/Link
Icon over label (Label/Header Icon), e.g. Account, Cart.

### Nav/Item
Type = Default, Dropdown, Open, Specials. Label/Nav. "Open" uses a darker overlay (pixel-sampled).

### Nav/Mega-menu
279 x 343 dropdown for "Our Range".

### Nav/Mobile Drawer
312 wide. `bg-drawer`, `border-drawer` dividers, Label/Drawer.

### Page Title
1440 wide. Breadcrumbs = True | False. Gradient band ending in `#5BA3E0` (pixel-sampled, not tokenised).

### Breadcrumbs
Path with chevron separators, 20px text (pixel-sampled).

### Footer
Breakpoint = Desktop (1440 x 360) | Mobile (390 x 430). `bg-footer`, H5/Footer headings.

---

## Commerce

### Card/Product
| State | Difference |
|---|---|
| Default | Image, title, price, ADD + Form/Qty |
| Promo | Adds the Multi-buy badge top-left |
| Out of stock | Actions replaced by the grey OUT OF STOCK block |

Anatomy: 216 wide, `spacing-10` padding and gap, 1px `border-default`, no radius. Image 195 tall. Title Product/Title, uppercase, centred, `text-link`. Price centred. Actions row: Button (Primary) + Form/Qty, 3px gap.

### Card/Store
437 x 417. Store name, address, hours, phone and actions.

### Cart/Table Header and Cart/Line Item
836 wide table. Line item 102 tall: image, name, Price (Cart), Form/Qty, total, trash icon.

### Filter/Accordion Header
Tone = Offers, Category, Recently viewed. State = Collapsed, Expanded (Recently viewed is Static). H6/Filter Header.

### Filter/Option
Level = 1, 2 (level 2 indented `spacing-25`). State = Default, Selected.

### Filter/Sort Bar
944 wide. Result info, sort select and View Toggle.

### Pagination
Label/Pager. Built from nopCommerce pager markup; never seen live.

### Toast/Added to Cart
Full-width 1440 x 75 cyan (`brand-accent`) toast, 20px text.

### Checkout/Step Header
1100 x 32 collapsible step bar for one-page checkout.

---

## Overlays & banners

### Modal/Age Gate
Breakpoint = Desktop (450 wide), Mobile (370 wide). H2/Modal heading, CTA buttons. Shown on every new session.

### Modal/Store Selector
450 wide. Region then Store selects (live). Consider suburb search and geolocation (see research notes).

### Banner/Cashpoints
Type = Hero, Benefit Card, Strip. Strip is a Proposal.

### Banner/Newsletter
1440 x 310 "JOIN NOW" banner linking out. There's no inline email field on the live site.

### Banner/Service Promises
1270 x 144 row of service promises (pickup, delivery, store count).

### Hero/Tile Large, Hero/Tile Small, Hero/Modular Carousel
Sandbox hero components: Tile Large 830 x 600, Tile Small 510 x 290, Modular Carousel with 4 slides (1360 wide).
