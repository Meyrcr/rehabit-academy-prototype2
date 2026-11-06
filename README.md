# Prototype 2 — Rehabit Academy, Rehabit-branded

Same eleven pages, same content, same browser interactions as `prototype/`. The visual layer is rebuilt to follow `ORG_SITE_DESIGN.md`, the design guide for rehabit.co.za.

Run from this folder: `python3 -m http.server 8081`; visit `http://localhost:8081`. Any page also opens from disk: double-click `index.html`. No build step and no network request is needed.

## What changed against `prototype/`

| Area | `prototype/` | `prototype2/` |
|---|---|---|
| Colour | Invented green and mint palette | Extracted Rehabit palette: navy `#002b49`, orange `#ff7c44`, CTA red, cream `#ece7e1` |
| Type | System font stack | Montserrat headings, Poppins body, self-hosted |
| Header | White bar, no account links | Navy bar, cream links, orange underline on the active page, `login` icon link, one account call to action |
| Buttons | One green fill, one mint fill | Red primary, orange secondary with navy text, ghost tertiary. Full-width on phones |
| Cards | 19px radius, heavy soft shadow | 10px radius, extracted shadow, `.featured` state for the recommended plan |
| Icons | Emoji only | Material Symbols Outlined subset, 25 names, plus the emoji course tiles |
| Hero | Two columns, green gradient, `✳` glyph | Centred headline, 22px sub-headline, call-to-action row, overlapping product-screenshot placeholder. Guide section 5.2 |
| Forms | Plain inputs | Inputs with icon slots, brand focus ring, card container |
| Footer | Light grey strip | Navy band, orange links |
| Accessibility | Not audited | Contrast audit and four forced changes, keyboard nav, reduced-motion, print sheet. `DESIGN_TOKENS.md` section 5 |

## Read these first

- `DESIGN_TOKENS.md` — every colour, size and radius, the source rule it came from, and the four values I changed for contrast.
- `../ORG_SITE_DESIGN.md` — the guide. Sections marked `[TO EXTRACT]` are resolved in `DESIGN_TOKENS.md`.

## Deviations from the guide, on purpose

1. The header is the product navigation, not a marketing anchor menu. Features, Pricing, Blog and Login become Dashboard, My CPD, Pricing and Login.
2. The nav call to action reads "Create account". Guide section 1 lists "Try Rehabit for FREE" as the conversion label. The Academy price is not approved, so this prototype makes no free claim.
3. The logo is typographic. `logo.svg` on rehabit.co.za is a trademark. Do not copy it here.
4. Screenshots and photos are CSS placeholders. Do not hot-link Rehabit assets, client logos or testimonials.
5. Zoom stays enabled. The source page sets `maximum-scale=1`, which guide section 8 already warns against.
6. Component rules for the stat band, the OFF / ON comparison and the alternating feature rows are in the stylesheet. No page uses them yet, because the prototype has no copy for them.

## NOT A PRODUCTION APP

No real auth, password storage, payments, assessment security, CEU award, PDF certificate, CPD submission or content accreditation. The quiz uses browser-only grading to demonstrate UX. Production grading must be server-side and transactional. Do not relabel these demo pages as fully implemented tickets.

The visual layer is now traceable to the live Rehabit site, but it is still a prototype. Confirm the colours, the logo and the components against the licensed brand assets and the production UI kit before you ship anything.
