# Super Liquor NZ Design System

The single source of truth for how Super Liquor NZ looks and behaves. Every value in this file comes from the Figma file **Design Sandbox - Super Liquor**, whose foundations were pulled from computed CSS on superliquor.co.nz on 20 Oct 2026.

- Figma: https://www.figma.com/design/qADYjXC1rLk367Etfyql3I/Design-Sandbox---Super-Liquor
- Pages: `03 Foundations` (tokens), `02 Components` (library), `00 Notes` (capture notes), `Designs` (sandbox screens)
- Mode: light only (the live site has no dark mode)

> **Status legend**
> - **Live**: captured from the live site's computed CSS.
> - **Proposal**: a Journey proposal, pending client sign-off. Use it, but flag it in reviews.

---

## 1. Principles

1. **Store first.** Prices, stock and pickup depend on the selected store. Always show which store the shopper is in, and make changing it one tap away.
2. **Category intent over SKU search.** Most liquor searches are categories ("gin", "rosé"). Route them straight to a filtered listing.
3. **Price is the hero.** Prices are always red (`--sl-color-text-price`), large and scannable.
4. **Blue means act, red means deal.** Brand blue drives everyday actions. Red is reserved for promo, price and high-intent CTAs. Don't mix them up.
5. **Tokens, never raw values.** If a value isn't a token, it isn't part of the system. Propose a new token instead.

---

## 2. Colour

Two layers: **Primitives** (raw palette) and **Semantic** tokens (what to use in code). Semantic tokens alias primitives. Always use semantic tokens in components.

### 2.1 Semantic tokens

| Token | CSS variable | Value | Primitive | Use |
|---|---|---|---|---|
| color/brand/primary | `--sl-color-brand-primary` | `#205AA7` | blue/700 | Primary buttons, brand surfaces |
| color/brand/secondary | `--sl-color-brand-secondary` | `#0069B9` | blue/600 | Secondary brand accents |
| color/brand/accent | `--sl-color-brand-accent` | `#25C8E0` | cyan/400 | Highlights, add-to-cart toast |
| color/promo | `--sl-color-promo` | `#E00041` | red/600 | Promo buttons, deal surfaces |
| color/action/cta | `--sl-color-action-cta` | `#DC2332` | red/500 | High-intent CTAs (age gate Yes, Shop Now) |
| color/action/cta-edge | `--sl-color-action-cta-edge` | `#88141E` | red/900 | 4px bottom edge on CTA buttons |
| color/text/primary | `--sl-color-text-primary` | `#212529` | grey/900 | Body text |
| color/text/secondary | `--sl-color-text-secondary` | `#333333` | grey/800 | Supporting text |
| color/text/strong | `--sl-color-text-strong` | `#212121` | grey/850 | Emphasised text |
| color/text/input | `--sl-color-text-input` | `#495057` | grey/700 | Input values |
| color/text/placeholder | `--sl-color-text-placeholder` | `#6C757D` | | Input placeholders |
| color/text/helper | `--sl-color-text-helper` | `#6C757D` | | Form helper text |
| color/text/inverse | `--sl-color-text-inverse` | `#FFFFFF` | white | Text on dark/brand fills |
| color/text/link | `--sl-color-text-link` | `#205AA7` | blue/700 | Links, product titles |
| color/text/price | `--sl-color-text-price` | `#E00041` | red/600 | All prices |
| color/text/heading-promo | `--sl-color-text-heading-promo` | `#E00041` | red/600 | Promo headings |
| color/text/error | `--sl-color-text-error` | `#E00041` | red/600 | Error messages |
| color/text/disabled | `--sl-color-text-disabled` | `#999999` | grey/500 | Disabled text (Proposal) |
| color/bg/page | `--sl-color-bg-page` | `#FFFFFF` | white | Page background |
| color/bg/utility | `--sl-color-bg-utility` | `#F8F9FA` | grey/50 | Utility bar |
| color/bg/footer | `--sl-color-bg-footer` | `#F5F5F5` | grey/75 | Footer |
| color/bg/panel | `--sl-color-bg-panel` | `#F3F3F3` | grey/100 | Panels, filters |
| color/bg/promo-soft | `--sl-color-bg-promo-soft` | `#EEE9D6` | cream/100 | Soft promo surfaces |
| color/bg/out-of-stock | `--sl-color-bg-out-of-stock` | `#AEB2B6` | grey/450 | OUT OF STOCK block |
| color/bg/toggle | `--sl-color-bg-toggle` | `#999999` | grey/500 | Inactive view toggle |
| color/bg/drawer | `--sl-color-bg-drawer` | `#333333` | | Mobile nav drawer |
| color/border/default | `--sl-color-border-default` | `#E2E2E2` | grey/150 | Cards, dividers |
| color/border/input | `--sl-color-border-input` | `#CED4DA` | grey/250 | Text inputs |
| color/border/select | `--sl-color-border-select` | `#DDDDDD` | grey/200 | Selects |
| color/border/strong | `--sl-color-border-strong` | `#B7B7B7` | grey/400 | Qty box, strong dividers |
| color/border/card-home | `--sl-color-border-card-home` | `#CBCBCB` | grey/300 | Home page cards |
| color/border/brand | `--sl-color-border-brand` | `#205AA7` | blue/700 | Brand-outlined elements |
| color/border/error | `--sl-color-border-error` | `#E00041` | red/600 | Inputs in error |
| color/border/drawer | `--sl-color-border-drawer` | `#222222` | | Drawer dividers |

### 2.2 Interaction state tokens (Proposal)

| Token | CSS variable | Value |
|---|---|---|
| color/action/primary-hover | `--sl-color-action-primary-hover` | `#1B4D8F` |
| color/action/primary-pressed | `--sl-color-action-primary-pressed` | `#163F75` |
| color/action/promo-hover | `--sl-color-action-promo-hover` | `#C00038` |
| color/action/promo-pressed | `--sl-color-action-promo-pressed` | `#A0002F` |
| color/action/cta-hover | `--sl-color-action-cta-hover` | `#C11E2C` |
| color/action/cta-pressed | `--sl-color-action-cta-pressed` | `#A81A26` |
| color/action/outline-hover | `--sl-color-action-outline-hover` | `#E9EFF8` |
| color/action/outline-pressed | `--sl-color-action-outline-pressed` | `#D2DEF0` |
| color/action/disabled-bg | `--sl-color-action-disabled-bg` | `#E2E2E2` |
| color/action/disabled-border | `--sl-color-action-disabled-border` | `#CBCBCB` |
| color/focus/ring | `--sl-color-focus-ring` | `#205AA7` |
| color/focus/gap | `--sl-color-focus-gap` | `#FFFFFF` |

### 2.3 Primitives

| Primitive | Value | Primitive | Value |
|---|---|---|---|
| blue/700 | `#205AA7` | grey/450 | `#AEB2B6` |
| blue/600 | `#0069B9` | grey/400 | `#B7B7B7` |
| cyan/400 | `#25C8E0` | grey/300 | `#CBCBCB` |
| red/600 | `#E00041` | grey/250 | `#CED4DA` |
| red/500 | `#DC2332` | grey/200 | `#DDDDDD` |
| red/900 | `#88141E` | grey/150 | `#E2E2E2` |
| grey/900 | `#212529` | grey/100 | `#F3F3F3` |
| grey/850 | `#212121` | grey/75 | `#F5F5F5` |
| grey/800 | `#333333` | grey/50 | `#F8F9FA` |
| grey/700 | `#495057` | white | `#FFFFFF` |
| grey/500 | `#999999` | cream/100 | `#EEE9D6` |

> The Cashpoints promo microsite uses a purple/yellow sub-brand palette. It is **not** tokenised and must not be used on the core site.

---

## 3. Typography

- **Family:** Barlow (Google Fonts). Weights used: 400, 500, 600, 700, 900, plus 700 italic.
- **No uppercase text styles.** Uppercase (product titles, eyebrow labels) is applied per component, not baked into a style.
- **Tracking:** -1px from 22px up; H1 and H2/Modal use -2px.
- Sizes are in px; line height shown as size/line-height.

| Style | Weight | Size / LH | Tracking | Use | Status |
|---|---|---|---|---|---|
| H1/Hero | Bold 700 | 51 / 50 | -2px | Hero headlines | Live |
| H2/Section | Medium 500 | 40 / 40 | -1px | Section headings (live site was 40/60) | Live |
| H2/Modal | Bold Italic 700 | 40 / 48 | -2px | Modal headings (age gate) | Live |
| H3/Feature | SemiBold 600 | 32 / 38 | -1px | Feature headings | Proposal |
| H4/Card Title | SemiBold 600 | 28 / 34 | -1px | Large card titles | Proposal |
| H5/Page Title | SemiBold 600 | 22 / 26.4 | -1px | Page titles, card headings | Live |
| H5/Footer | Regular 400 | 22 / 33 | -1px | Footer headings | Live |
| H5/Promo Strip | Bold 700 | 22 / 33 | -1px | Promo strips | Live |
| H5/Promo Strip Sentence | Bold 700 | 22 / 33 | -1px | Merge candidate with Promo Strip | Live |
| H6/Filter Header | Medium 500 | 18 / 27 | 0 | Filter accordion headers | Live |
| Price/Large | SemiBold 600 | 24 / 36 | -1px | Card and PDP price | Live |
| Body/Large | Regular 400 | 17 / 25.5 | 0 | Intro copy | Live |
| Body/Default | Regular 400 | 16 / 24 | 0 | Default body | Live |
| Body/Strong | Bold 700 | 16 / 24 | 0 | Emphasis | Live |
| Body/Small | Regular 400 | 15 / 22.5 | 0 | Secondary copy | Live |
| Product/Title | Bold 700 | 16 / 19.2 | 0 | Product card titles (uppercase, link blue) | Live |
| Button/Large | Bold 700 | 20 / 30 | 0 | CTA buttons | Live |
| Button/Default | Bold 700 | 18 / 27 | 0 | Standard buttons | Live |
| Label/Nav | SemiBold 600 | 14 / 21 | 0 | Nav items, utility bar | Live |
| Label/Header Icon | SemiBold 600 | 14 / 14 | 0 | Labels under header icons | Live |
| Label/Drawer | Bold 700 | 14 / 21 | 0 | Mobile drawer items | Live |
| Label/Status | Black 900 | 16 / 24 | 0 | OUT OF STOCK and status blocks | Live |
| Label/Pager | Black 900 | 18 / 27 | 0 | Pagination | Live |
| Caption/Default | SemiBold 600 | 12 / 18 | 0 | Captions, eyebrows ("YOUR STORE") | Live |

---

## 4. Spacing

The scale reflects real values on the site (10px and 15px dominate). It is **not** a strict 4/8 grid; use the nearest token.

| Token | CSS variable | Value |
|---|---|---|
| spacing/2 | `--sl-spacing-2` | 2px |
| spacing/3 | `--sl-spacing-3` | 3px |
| spacing/4 | `--sl-spacing-4` | 4px |
| spacing/5 | `--sl-spacing-5` | 5px |
| spacing/6 | `--sl-spacing-6` | 6px (input padding) |
| spacing/8 | `--sl-spacing-8` | 8px |
| spacing/10 | `--sl-spacing-10` | 10px |
| spacing/12 | `--sl-spacing-12` | 12px |
| spacing/15 | `--sl-spacing-15` | 15px |
| spacing/16 | `--sl-spacing-16` | 16px |
| spacing/20 | `--sl-spacing-20` | 20px |
| spacing/25 | `--sl-spacing-25` | 25px |
| spacing/35 | `--sl-spacing-35` | 35px |
| spacing/48 | `--sl-spacing-48` | 48px |

---

## 5. Radius

| Token | CSS variable | Value | Use |
|---|---|---|---|
| radius/none | `--sl-radius-none` | 0 | Cards, panels |
| radius/sm | `--sl-radius-sm` | 3px | Buttons |
| radius/md | `--sl-radius-md` | 4px | Inputs, search bar |
| radius/lg | `--sl-radius-lg` | 5px | Larger surfaces |
| radius/full | `--sl-radius-full` | 999px | Chips, pills, badges |

---

## 6. Elevation

| Style | Value (CSS `box-shadow`) | Use |
|---|---|---|
| Elevation/Header | `0 0 8px 0 rgba(0,0,0,0.15)` | Sticky header |
| Elevation/Card | `0 1px 2px 0 rgba(0,0,0,0.24), 0 1px 3px 0 rgba(0,0,0,0.12)` | Raised cards |
| Elevation/Subtle | `0 2px 2px 0 #F3F2F8` | Light separation |
| Elevation/Popover | `0 8px 24px 0 rgba(0,0,0,0.16), 0 1px 3px 0 rgba(0,0,0,0.08)` | Search panel, dropdowns |

---

## 7. Layout

| Breakpoint | Frame width | Side gutter | Notes |
|---|---|---|---|
| Desktop | 1440px | 85px (content 1270px) | Header 173px: utility 40 + main 92 + nav 41 |
| Mobile | 390px | 20px (content 350px) | Header 93px; product cards scroll horizontally |

- Product cards are a fixed **216px** wide, in rows with even gaps.
- Section vertical padding is typically 48px on desktop and 25px on mobile.

---

## 8. Iconography

- 24 x 24 SVG icons, redrawn from the live site's Font Awesome glyphs. Default colour: `--sl-color-brand-primary`.
- Set: search, pin, cart, user, mailer, truck, store, phone, chevron-down, chevron-up, chevron-right, caret, menu, close, basket, trash, grid, list, bell, facebook, instagram, dollar, bag, alert.
- Use the Figma names (`Icon/<name>`) as component names in code.

---

## 9. Components

The full catalogue (variants, states, anatomy and usage) is in [docs/COMPONENTS.md](docs/COMPONENTS.md). Summary:

| Group | Components |
|---|---|
| Brand | Brand/Logo, Icons (24) |
| Actions & status | Button, Button/View Toggle, Badge, Price, Stock Indicator |
| Forms & search | Form/Input, Form/Qty, Form/Field, Search Bar, Search, Search/Chip, Search/Suggestion, Search/Product, Search/Panel |
| Header & navigation | Header/Desktop, Header/Mobile, Header/Link, Nav/Item, Nav/Mega-menu, Nav/Mobile Drawer, Page Title, Breadcrumbs, Footer |
| Commerce | Card/Product, Card/Store, Cart/Table Header, Cart/Line Item, Filter/Accordion Header, Filter/Option, Filter/Sort Bar, Pagination, Toast/Added to Cart, Checkout/Step Header |
| Overlays & banners | Modal/Age Gate, Modal/Store Selector, Banner/Cashpoints, Banner/Newsletter, Banner/Service Promises, Hero/Tile Large, Hero/Tile Small, Hero/Modular Carousel |

---

## 10. Accessibility

- **Contrast:** body text `#212529` on white passes WCAG AA. White text on `#205AA7`, `#E00041` and `#DC2332` passes AA for the bold 18px+ button text. Don't put white text on `--sl-color-brand-accent` (cyan) at body size.
- **Focus:** every interactive element shows a visible focus ring: a 2px `--sl-color-focus-gap` (white) gap, then a 2px `--sl-color-focus-ring` outline. Never remove focus outlines.
- **Forms:** use `aria-required`, `aria-invalid` and `aria-describedby` (pointing at the message) on Form/Field. Required fields show a red `*` on the label.
- **Stock:** never signal stock with colour alone. OUT OF STOCK is always written text.
- **Age gate:** must be keyboard-operable, trap focus while open, and return focus when closed.
- **Motion:** state transitions use 150ms ease-out. Respect `prefers-reduced-motion`.

---

## 11. Voice & content

- Short, plain and NZ English ("colour", "favourite"). Prices in NZD with `$` and two decimals (`$64.99`).
- Button labels are verbs in caps where the live site uses caps (`ADD`, `CHECKOUT`). Elsewhere, sentence case.
- Be consistent on fulfilment: use **"Free pickup"** and **"Nationwide delivery"**. Avoid the live site's mixed "Pick up & Delivery" / "Order & Pick Up".
- Responsible service: the age gate is required on entry; copy must not encourage excessive drinking.
