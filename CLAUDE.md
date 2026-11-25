# CLAUDE.md

Guidance for Claude (and other AI coding agents) working in this repo. Read this first, then [DESIGN.md](DESIGN.md).

## What this repo is

The design system and front-end work for **Super Liquor NZ**, a New Zealand liquor retailer with 185+ stores. The design source of truth is the Figma file **Design Sandbox - Super Liquor**:
https://www.figma.com/design/qADYjXC1rLk367Etfyql3I/Design-Sandbox---Super-Liquor

## Where things live

| Path | What |
|---|---|
| `DESIGN.md` | Tokens (colour, type, spacing, radius, elevation), layout, accessibility, voice |
| `docs/COMPONENTS.md` | Every component with variants, states and usage rules |
| `docs/RESEARCH-NOTES.md` | Capture notes, assumptions and UX findings from the live site || `README.md` | Project overview |

## Rules for building UI

1. **Use tokens, never raw values.** Colours, spacing, radii, shadows and type come from the `--sl-*` CSS variables in DESIGN.md. No hard-coded hex codes or px values that already have a token.
2. **Use semantic tokens, not primitives.** Write `var(--sl-color-text-price)`, not `#E00041` or `red/600`.
3. **Reuse components before building new ones.** Check `docs/COMPONENTS.md` first. Match Figma names and variant properties (e.g. `Button` with `variant="primary" | "promo" | "cta" | "outline" | "block"`).
4. **Font is Barlow.** Load it from Google Fonts (400, 500, 600, 700, 700 italic, 900). Use the named text styles; don't invent sizes.
5. **Colour roles are strict.** Brand blue for everyday actions and links. Red (`promo`, `action-cta`, `text-price`) only for deals, prices and high-intent CTAs.
6. **Store context matters.** Price and stock UI must assume a selected store and handle the "store not selected" state.
7. **Accessibility is required, not optional.** Visible focus rings (`--sl-color-focus-*`), ARIA on form fields, stock never shown by colour alone, keyboard-operable modals. Target WCAG 2.2 AA.
8. **Mobile first.** Design for 390px, then scale to 1440px (gutters 20px mobile, 85px desktop).
9. **Light mode only.** Don't add dark-mode styles unless asked.

## Working with Figma

- Read designs through the Figma MCP connector (file key `qADYjXC1rLk367Etfyql3I`).
- Component docs in Figma (descriptions on each component) override assumptions. If Figma and DESIGN.md disagree, flag it and ask; don't silently pick one.
- Values marked **Proposal** (hover, pressed, focus, disabled, loading states; H3 and H4) are pending client sign-off. Use them, but mention them in PR descriptions.
- Rasters in Figma (logo, product, store images) are placeholder crops. Never ship them as final assets.

## Adding or changing tokens

1. Change it in Figma first (or get design sign-off).
2. Update DESIGN.md in the same PR as any code that uses it.
3. Name new tokens by role: `color/<group>/<role>`, `spacing/<px>`, `radius/<size>`.

## Writing style

- NZ English ("colour", "favourite"). Prices as `$64.99` (NZD).
- Sentence case for UI copy, except where the live site uses caps (`ADD`, `CHECKOUT`).
- Use "Free pickup" and "Nationwide delivery" consistently.
- Responsible-service content: never encourage excessive drinking; the age gate is required.

## Git

- Branch from `main`; keep PRs small and focused.
- Commit messages in the imperative ("Add Card/Product component").
- Don't commit secrets, `.env` files or large binary exports.
