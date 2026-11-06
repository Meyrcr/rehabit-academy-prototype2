# Design tokens for `prototype2`

`ORG_SITE_DESIGN.md` marks its colour, type and spacing tables `[TO EXTRACT]` and says: "Do not invent values." This file records the values I extracted, where each one came from, and the places where I made a documented change instead.

- Source site: https://rehabit.co.za/
- Source stylesheet: https://rehabit.co.za/assets/css/styles.css (35 KB, unminified, no CSS custom properties)
- Extracted: 2026-11-06
- Method (Step 0 of the guide):

```bash
curl -sL https://rehabit.co.za/ -o /tmp/rehabit.html
grep -oE '(href|src)="[^"]+\.(css|woff2?|ttf|svg)[^"]*"' /tmp/rehabit.html
grep -oE 'fonts\.googleapis\.com[^"]+' /tmp/rehabit.html
curl -sL https://rehabit.co.za/assets/css/styles.css -o /tmp/site.css
grep -oE '#[0-9a-fA-F]{3,8}\b' /tmp/site.css | sort | uniq -c | sort -rn | head -30
grep -oE 'font-family:[^;]+' /tmp/site.css | sort | uniq -c | sort -rn
grep -oE 'border-radius:[^;]+' /tmp/site.css | sort | uniq -c | sort -rn
```

The site declares no CSS custom properties, so the token names below are mine. The **values** are theirs.

## 1. Colour

| Token in `style.css` | Value | Where the value comes from | Use in this prototype |
|---|---|---|---|
| `--navy` | `#002b49` | `.blog-sidebar h4` border, `.blog-body h2`, `.pricing-header` neighbour rules, used 30 times | Header bar, headings, dark panels, footer, stat band |
| `--navy-2` | `#02243b` | `.testimonials-logo-container` border | Hero gradient start |
| `--navy-3` | `#0e3c5f` | Derived: lighten of `#002b49` | Hero gradient end. **Derived, not extracted.** |
| `--orange` | `#ff7c44` | Most frequent colour in the sheet (34 uses): `.toggle-on-benefit`, `.pricing-button-secondary`, `.redirect-button`, `.blog-body h3` | Accent, secondary button, focus ring, icon ticks, progress fill |
| `--orange-ink` | `#cc4a1a` | `.blog-final-cta` gradient stop | Orange that carries text or links |
| `--orange-hover` | `#b8420f` | Derived from `--orange-ink` | Secondary button hover. **Derived, not extracted.** |
| `--red` | `#ff1d25` | `.above-the-fold-cta-link`, `.pricing-button` | Large display CTA only |
| `--red-2` | `#e83024` | `.blog-sidebar-cta-btn` | Danger notice border |
| `--cta` | `#c9281d` | `.blog-sidebar-cta-btn:hover` | Primary button fill (see contrast audit) |
| `--cta-hover` | `#a3201a` | Derived from `--cta` | Primary button hover. **Derived, not extracted.** |
| `--ink` | `#1f282f` | `html,body` colour | Body copy |
| `--cream` | `#ece7e1` | `.header-link`, `.toggle-off-disadvantage`, `.above-the-fold-cta h4` | "OFF" column, muted tags, light band, hero sub-headline |
| `--peach` | `#fff5ef` | Section background | Notice background, course tile |
| `--mist` | `#f0f5fa` | Section background | Table header, checked option, tag background |
| `--muted` | `#767676` | Replaced. The site uses `#888`, `#999`, `#aaa`, `#ccc` | Secondary text (see contrast audit) |
| `--border` | `#e1e1e1` | Present in the sheet | Card and input borders |
| `--border-2` | `#eee` | `.pricing-container` border | Hairline dividers |
| `--good` | `#1c7a4d` | **Not a Rehabit colour** | Pass state on the assessment result only |

`[VERIFIED]` from the guide, section 2 note: the comparison section uses an OFF / ON contrast. The extracted pair is `#ece7e1` with black text (OFF, plus `filter:grayscale(100%)`) against `#ff7c44` with navy text (ON). `.compare-col.off` and `.compare-col.on` in `style.css` implement that pair.

## 2. Typography

| Role | Family | Weight | Size / line-height | Source rule |
|---|---|---|---|---|
| Body | Poppins, then Montserrat | 400 | 16px / 1.7 | `html,body{color:#1f282f;font-family:"Poppins","Montserrat",serif}` |
| H1 | Montserrat | 700 | 48px | `h1{text-align:center;font-weight:700;font-size:48px}` |
| H1, hero | Montserrat | 600 | 64px, clamped down to 36px on small screens | `.above-the-fold-cta h1{font-size:64px;font-weight:600}` |
| Sub-headline | Poppins | 400 | 22px | `.above-the-fold-cta h4{color:#ece7e1;font-weight:normal;font-size:22px}` |
| H2, section | Montserrat | 700 | 32px | `.team-introduction h2{font-size:32px}`, `.feature-carousel-grid-item h1{font-size:32px}` |
| H3 | Montserrat | 500 | 22px | `h3{font-size:22px;font-weight:500}` |
| H3, accent | Montserrat | 700 | 18px | `.blog-body h3{font-family:"Montserrat";color:#ff7c44}` |
| Eyebrow / label | Montserrat | 700 | 12px, uppercase, letter-spacing 0.08em | `.blog-sidebar h4{font-size:0.75rem;text-transform:uppercase;letter-spacing:0.08em}` |
| Button | Montserrat | 700 | 16px | `.redirect-button{font-size:20px}` scaled down for app screens |
| Price / stat number | Montserrat | 700 | 40px, 30px in the stat band | `.pricing-value{font-size:36px;font-weight:500}`, `.cta-header{font-size:36px}` |
| Small print | Poppins | 400 | 13px | `.pricing-frequency{font-size:14px}` |

Fonts are self-hosted in `assets/fonts/`. Families, weights and the two Google Fonts requests come from the source page markup. Files are the latin subset of Montserrat 500/600/700 and Poppins 400/500/600 (SIL Open Font License 1.1), so the prototype renders identically offline and needs no third-party request.

## 3. Shape, elevation, measure

| Token | Value | Source |
|---|---|---|
| `--r-card` | 10px | `border-radius:10px` — the dominant value, 16 uses |
| `--r-btn` | 6px | `.above-the-fold-cta-link{border-radius:6px}`, `.cta-button{border-radius:4px}` |
| `--r-chip` | 50px | `.toggle-slider{border-radius:60px}`, `.blog-mobile-toc-btn{border-radius:50px}` |
| `--r-input` | 8px | `.blog-sidebar-cta{border-radius:8px}` |
| `--sh-card` | `0 2px 12px rgba(0,0,0,.12)` | Present in the sheet |
| `--sh-float` | `0 4px 8px rgba(0,0,0,.3)` | `.redirect-button`, `.toggle-on-benefit` |
| `--sh-pop` | `0 8px 24px rgba(0,0,0,.15)` | `.blog-mobile-toc-header` |
| `--container` | 1200px | `.container,.container-1200{max-width:1200px}` |
| `--container-wide` | 1500px | `.container-1500{max-width:1500px}` |
| Section padding | 48px vertical, 24px inline | Inferred from `.testimonials-header-grid{padding:48px}` and `.testimonials-frame{padding-bottom:48px}`. **Inferred, not extracted.** |
| Button padding | 16px 24px | `.cta-button`, `.above-the-fold-cta-link` |
| Breakpoints | 1000px, 850px, 580px | The sheet tests 958px and 960px. **Adjusted, not extracted.** |

## 4. Iconography

Guide section 4 asks for Material Symbols. `assets/fonts/MaterialSymbolsOutlined.woff2` is a 4.2 KB subset that holds only the 25 ligature names this prototype uses: `login`, `menu`, `close`, `search`, `arrow_circle_left`, `arrow_circle_right`, `check_circle`, `cancel`, `lock`, `mail`, `person`, `school`, `description`, `verified`, `credit_card`, `dashboard`, `play_circle`, `download`, `chevron_right`, `insights`, `badge`, `health_and_safety`, `timer`, `checklist`, `visibility`.

`login` in the header matches the source site. Use `<span class="material-symbols-outlined">name</span>` and keep `aria-hidden="true"`.

Icons are ligature text. If the font file is missing, the browser shows the ligature name in place of the glyph. The pages stay readable. That is the intended fallback, and it is also how to spot a broken icon name.

## 5. Contrast audit and the four changes it forced

Guide section 9.5 requires 4.5:1 for text. WCAG 2.1 relative-luminance ratios against the extracted palette:

| Pairing | Ratio | Verdict |
|---|---|---|
| `#ff7c44` on `#fff` | 2.56:1 | Fails, even for large text |
| `#fff` on `#ff1d25` | 3.85:1 | Passes large text only |
| `#fff` on `#e83024` | 4.30:1 | Passes large text only |
| `#fff` on `#c9281d` | 5.52:1 | Passes |
| `#002b49` on `#ff7c44` | 5.70:1 | Passes |
| `#cc4a1a` on `#fff` | 4.60:1 | Passes |
| `#002b49` on `#fff` | 14.57:1 | Passes |
| `#888` on `#fff` | 3.54:1 | Fails for body text |
| `#767676` on `#fff` | 4.54:1 | Passes |

Changes made, in each case to hold 4.5:1 while staying inside the extracted palette:

1. Primary buttons use `#c9281d`, the site's own CTA hover colour, not `#ff1d25`.
2. Orange never carries text on white. Text and links that need orange use `#cc4a1a`. Orange on navy is legal and is used for eyebrows and hover.
3. Secondary buttons pair `#ff7c44` with navy text instead of white text.
4. `--muted` is `#767676`. The source sheet uses `#888` and `#999`, which fail on white.

Other accessibility rules from guide section 9: the viewport keeps zoom enabled, so `maximum-scale=1` is **not** copied. Focus uses a 3px orange ring with offset. `prefers-reduced-motion` disables transitions and smooth scroll. The header nav is keyboard operable and the mobile toggle sets `aria-expanded`.

## 6. Patterns that exist in CSS but not in the pages

`style.css` also carries `.statband`, `.stat`, `.compare`, `.compare-col` and `.feature-row` rules, which the guide lists in sections 5 and 6. The prototype pages hold no copy for them, so no page uses them. Do not treat them as approved design. They are ready when the client supplies real content, logos or testimonials.

## 7. What is still unverified

- Logo and wordmark. `brand-mark` is a typographic placeholder in brand orange. The site's `logo.svg` is a trademark. Do not copy it into this prototype or hand it to a third party without written permission.
- Photography and product screenshots. `.shot` draws a labelled placeholder in CSS. Guide section 7 lists real asset paths. Do not hot-link them, and do not redistribute Rehabit client logos or testimonials in another product.
- Hero background artwork. The site uses PNG backgrounds (`cta_background.png`, `footer_blobs.png`). I used a navy gradient instead.
- Section vertical rhythm, grid gutters and container padding are inferred, not measured.
- Approved prices, accreditation status and CEU rules are unchanged in meaning: every number on these pages stays illustrative.
