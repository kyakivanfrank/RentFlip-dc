# RentFlip — Design System

> **Source of truth.** This document describes the *current, approved* RentFlip design
> as built in the Claude design prototype. Where it disagrees with the code in this
> repo, **the code should be updated to match this document** — not the other way around.
> §13 lists the exact constants/widgets to change.
>
> App = one product, two roles: **Landlord** (purple) and **Tenant** (amber/coral).
> Layout, type, spacing, radius and shadows are identical across roles — only the
> **accent color, hero-card art, and a couple of labels** change.
>
> Maps onto: `lib/core/constants/app_colors.dart`, `app_dimens.dart`, `rf_icons.dart`,
> `lib/core/theme/app_theme.dart`, and `lib/core/widgets/*`.

---

## 1. Brand

- **Wordmark:** `RentFlip`, Plus Jakarta Sans **ExtraBold (w800)**, letter-spacing `-0.6`.
- **Logo mark:** `assets/images/logo_rentflip.svg` — two interlocking forms (rent
  "flipping" between tenant & landlord) in brand **purple `#814BC4`** + **indigo `#2939A1`**.
  Native ratio **117 × 130** (≈ 0.9 : 1).
- **Rules:** place on white/light surfaces; on a colored surface set the mark inside a
  **white rounded tile** (app-icon style); never recolor, stretch, or rotate the glyph;
  always pair with the Plus Jakarta Sans wordmark in a lockup.

---

## 2. Color  → `AppColors`

sRGB hex, `Color(0xFF…)`. **Field name** = the constant in `app_colors.dart`.
⚠️ flags a value that must change from what's currently in the repo (see §13).

### Brand / Primary (Landlord)
| Token | Hex | AppColors field | Note |
|---|---|---|---|
| Primary | `#814BC4` | `brandPurple` ⚠️ (`#7A3FD4`→`#814BC4`) | Landlord accent, primary buttons, links, seed |
| Primary Deep | `#6E43AC` | `landlordGradientEnd` ⚠️ | Hero gradient end / fallback under card art |
| Primary 400 | `#9E72D8` | `landlordGradientStart` ⚠️ | Hero gradient start |
| Primary 100 | `#E7DEF6` | *(add)* `primary100` | Selected segment fill, soft chips |
| Primary 50 | `#F4EEFB` | `landlordSurface` ⚠️ (`#F7F4FD`→`#F4EEFB`) | Tint surface, OTP/phone field bg |
| Brand Indigo | `#2939A1` | `brandIndigo` ✓ | Logo dark wing, splash wordmark |
| Onboarding Ink | `#2A1B45` | *(add)* `onboardInk` | Onboarding hero panel (deep end) |
| Onboarding Ink 2 | `#3A2A6B` | *(add)* `onboardInk2` | Onboarding hero panel (top end) |

### Role accent (Tenant)
| Token | Hex | AppColors field | Note |
|---|---|---|---|
| Tenant | `#FEB201` | `tenantGradientStart` ⚠️ (`#F15A24`→`#FEB201`) | Tenant accent, "Pay" CTAs, amounts |
| Tenant Coral | `#FF8D5E` | `tenantGradientEnd` ⚠️ (`#EC008C`→`#FF8D5E`) | Tenant hero art fallback |
| Tenant 100 | `#FBF1E0` | `tenantSurface` ⚠️ (`#FFF8F5`→`#FBF1E0`) | Tenant tint surfaces |

> **Direction change:** the tenant identity is now **warm amber→coral**, not the old
> orange→magenta. Drop the magenta `#EC008C` entirely.

### Semantic (constant across roles)
| Token | Hex | AppColors field | Use |
|---|---|---|---|
| Success | `#1E8A4C` | `statusCollected` ⚠️ (`#2E7D32`→`#1E8A4C`) | Collected text, RECEIPT badge text |
| Success BG | `#DFF7E7` | `statusCollectedBg` ⚠️ (`#E8F5E9`→`#DFF7E7`) | RECEIPT badge bg, paid icon chip |
| Outstanding | `#C5602F` | `statusOutstanding` ⚠️ (`#F57F17`→`#C5602F`) | Outstanding/warn text + icon |
| Outstanding BG | `#FFE9DC` | `statusOutstandingBg` ⚠️ (`#FFF8E1`→`#FFE9DC`) | Outstanding chip, PENDING bg |
| Pending text | `#FE8D47` | *(add)* `statusPending` | PENDING badge text |
| Info | `#2B6FB0` | *(add)* `statusInfo` | Info note text, "Collected" icon |
| Info BG | `#E7F2FF` | *(add)* `statusInfoBg` | Info note bg, collected icon chip |

### Neutrals
| Token | Hex | AppColors field |
|---|---|---|
| Ink | `#16121F` | `textDark` ⚠️ (`#1A1A2E`→`#16121F`) |
| Muted | `#6E6880` | *(add)* `textMuted` |
| Faint | `#9A95A8` | *(add)* `textFaint` (placeholders, dots) |
| Stat label | `#8A8594` | *(add)* `textStatLabel` |
| Border | `#ECEAF1` | *(add)* `border` |
| Field fill | `#F2F3F3` | `inputFill` ✓ (≈`#F2F2F4`) |
| Surface | `#FFFFFF` | `white` ✓ |
| Segment border | `#C9B6E6` | *(add)* `segmentBorder` |

**Gradients** (only where the hero SVG art is not used):
- Landlord fallback: `linear 140°  #9E72D8 → #7C4FB8 (60%) → #6E43AC`
- Tenant fallback: `linear 150°  #FFB199 → #FF9776 (55%) → #FF8D5E`
- Onboarding hero panel: `linear 165°  #3A2A6B → #2A1B45`

> The role **ink** values used as `_build(ink:)` seeds should move toward neutral
> `#16121F` for both roles (the tinted near-blacks `#1A0050`/`#4A1000` read muddy at
> small sizes). Keep `surface` tinted per role.

---

## 3. Typography → `AppTheme._textTheme` (Plus Jakarta Sans)

Family: **Plus Jakarta Sans** via `GoogleFonts.plusJakartaSansTextTheme()`. ✓ already correct.
Hierarchy is carried by **weight + opacity**, not big size jumps — keep that principle.
Map the prototype scale to Material `TextTheme` slots:

| Prototype style | Size | Weight | Tracking | TextTheme slot | Color |
|---|---|---|---|---|---|
| Revenue amount | 42 | 800 | -1.4 | `displayMedium` | white (on hero) |
| Display | 36 | 800 | -1.0 | `displayLarge` | Ink |
| Onboarding title | 29 | 800 | -0.6 | `displaySmall` | Ink |
| Screen title | 26 | 700 | 0 | `headlineSmall` | Ink |
| Section heading | 22 | 800 | 0 | `headlineMedium` | Ink |
| Card title / amount | 20 | 800 | -0.3 | `titleLarge` | Ink |
| Body | 16 | 600 | 0 | `titleMedium` | Ink |
| Body / onboarding | 16 | 500 | 0 | `bodyLarge` | Muted |
| Caption | 14 | 500 | 0 | `bodyMedium` | Muted |
| Stat value | 20 | 800 | -0.3 | `titleLarge` | Ink |
| Stat label | 13 | 600 | 0 | `bodySmall` | Stat label |
| Field label / kicker | 11–12 | 800 | +1.0–2.0 / UPPERCASE | `labelSmall` | Ink / Primary |

> Repo's `muted = ink.withOpacity(0.72)` ≈ `#6E6880` on white — fine. The prototype's
> letter-spacing on display/amount text (`-1.0` to `-1.4`) is tighter than the repo's
> `-0.5`; bump `displayLarge/Medium` tracking to match for the big UGX figures.

---

## 4. Spacing → `AppDimens` (4px base)

Scale `4·8·12·16·20·24·32·40` ✓ already present (`s4`…`s40`).
- Screen gutter: **20** (`pagePadding` ✓). Forms may use 22.
- Screen top padding below status bar: **60**.
- Between stacked cards: **18**. Between stat tiles / side-by-side fields: **14**.
- Card inner padding: **18** content / **18–26** hero.

> Add `s18 = 18` and `s14 = 14`, or use `s16`/`s20` where close. The 18/14 rhythm is what
> gives the new layout its "less compressed" feel — don't collapse it to 16/12.

---

## 5. Radius → `AppDimens`

| Token | px | AppDimens field | Applies to |
|---|---|---|---|
| Input | 16 | `rInput` ✓ | Text fields, OTP boxes |
| Button | 16 | *(add)* `rButton` ⚠️ | **All buttons** (see note) |
| Icon chip | 12 | *(add)* `rChip` | Stat-tile icon chips |
| Tile | 18 | `rTile` ⚠️ (`20`→`18`) | Stat tiles, segmented inner |
| Card | 20 | `rCard` ⚠️ (`28`→`20`) | Content cards, list rows |
| Hero card | 26 | *(add)* `rHero` | Landlord/Tenant revenue cards |
| Pill | 999 | `rPill` ✓ | Badges, role pills, switches |

> **Two important corrections:**
> 1. **Buttons are NOT fully-pill.** The approved design uses **subtly rounded 16px**
>    buttons (length-to-height proportioned, gentle radius). Change `PillButton` from
>    `StadiumBorder()` to `RoundedRectangleBorder(borderRadius: 16)`. (Keep `rPill`/
>    `StadiumBorder` for *badges* and *role pills* only.)
> 2. **Drop the `× 1.6` squircle multiplier** in `AppDimens.smoothShape`. With the new
>    smaller radii the continuous border should read close to its nominal value — either
>    remove the multiplier or lower it to ~`1.1`. Cards should be **subtly** round, not
>    super-elliptical. Validate visually against the prototype hero card (26px).

---

## 6. Elevation → `AppDimens.softShadow`

Tight, low-alpha, slightly downward. The current `softShadow` (alpha .06, blur 24,
offset 0,8) is a good base — add tier-specific variants:

| Tier | Spec | Note |
|---|---|---|
| Card | `0 10 26  rgba(40,25,70,.05)` | content cards / list container |
| Stat tile | `0 14 26  rgba(40,25,70,.06)` | white tiles on hero card |
| Hero card | `0 24 46  tint @ .14` | tint = role color (purple / coral) |
| Button | `0 14 26  fill @ .30` | tint = button color |
| Floating image | `drop-shadow(0 22 32  rgba(0,0,0,.30))` | image only |

> Flutter `BoxShadow` has no CSS-style negative spread; approximate the soft falloff
> with low alpha + larger blur rather than spread. Keep it subtle — no hard drops.

---

## 7. Iconography → `RfIcons` (Phosphor)

- Family: **Phosphor**, vendored TTF, referenced via `RfIcons` (`PhosphorRegular` /
  `PhosphorFill`). ✓ already in place — keep this; do **not** switch families.
- **Regular** outline is the default; **Fill** only for avatars / success states.
- Single visual weight, ~`22–24px`, tint per context (Primary default; semantic on tiles).
- In active use: `house, buildings, storefront, armchair, key, user, userPlus, users,
  currencyDollar, money, wallet, creditCard, receipt, bell, note, notePencil, chartBar,
  copy, gear, signOut, question, star, mapPin, magnifyingGlass, list, plus, x, caretRight,
  caretDown, warningCircle`; fills: `userFill, checkCircleFill, cameraFill`.

---

## 8. Components → `lib/core/widgets/*`

### `PillButton`  ⚠️ rename intent: "PrimaryButton"
- Height **54–56** (padding ~`vertical:16`), **radius 16** (not stadium — see §5).
- `primary`: bg = role color, white text, **w700**, button shadow tinted to fill.
- `ghost`: white bg, `1.5px` border `#C9B6E6`, role-color text, w700, radius 18.
- Tenant primary CTA: bg `#FEB201`, **text Ink `#16121F`** (amber needs dark text), w800.
- Text 15–16, tracking 0.5–1. Circular icon/next button: `Ø48–62`, role bg, white icon.

### `AppTextField`
- Height ~**52** (`contentPadding` h20/v18 ✓), **radius 16** ✓, fill `inputFill` ✓, no border;
  focus border `1.5px` role color ✓.
- Field label above in `labelSmall` (11/800/UPPERCASE/Ink), 8px gap. Placeholder = Faint.
- OTP: four **62×62** boxes, radius 16, fill `#F4EEFB`, digit 26/800.
- Phone field: `+256` prefix chip on `#F4EEFB` (see `CountryCodePicker`), number field same fill.

### Segmented control (role / filter)
- Outer: white, `1.5px` border `#C9B6E6`, radius 16, padding 5.
- Items equal-flex, h42–50, radius 12–14. Selected = `#E7DEF6` fill, Primary w700;
  unselected = transparent, Primary text.

### `StatusPillBadge`  ⚠️ colors + radius
- Padding `7×16`, **pill** radius (currently 20 → use `rPill`), 12/**w800**, +0.5 tracking.
- collected → bg `#DFF7E7` / text `#1E8A4C`; outstanding → bg `#FFE9DC` / text `#C5602F`.
- Add `pending` (bg `#FFE9DC`/text `#FE8D47`) and `receipt` (= collected) variants.

### `RoundedCard`
- Default radius → **20** (`rCard` after change), 18px padding, `softShadow`, white. ✓ structure fine.
- Drop squircle multiplier (§5) so corners are subtly — not heavily — rounded.

### Note strips *(add a `NoteStrip` widget)*
- Padding `11×14`, radius 14, centered, 13/600. Info `#E7F2FF`/`#2B6FB0` · Warn `#FFE9DC`/`#C5602F`
  · Success `#DFF7E7`/`#1E8A4C`.

### List row *(inside `RoundedCard`)*
- `14–16` padding, `40×40` icon tile (radius **11**, white, hairline + soft shadow),
  label 16–17/600 Ink, trailing `caretRight` `#7D7F88`. Rows split by `1px #F0EEF3`.

### Stat tile
- White, radius **18**, padding **18**. `40×40` icon chip (radius 12) tinted by meaning →
  label (13/600 stat-label) → value (20/800, -0.3, Ink). Two-up, 14px gap.

### `SvgSummaryCard` (hero revenue card)  ⚠️ shape
- **Aspect ratio 1 : 1.2** (w : h) — deliberately *not* square. Wrap in
  `AspectRatio(aspectRatio: 1/1.2)`; radius **26** (`rHero`); `SvgPicture.asset(..., BoxFit.cover)`
  with role fallback color underneath.
- Content column **top-aligned, tiles pinned to bottom** (`Spacer()` before the tiles):
  1. Role pill (white@60% outline, pill, 12/700, +1.5)
  2. Month + `caretDown`, centered, 16/600 white@90%
  3. Amount `UGX 2.5M` — 42/800, -1.4, white
  4. Caption (`Revenue` / `Transactions`) 14/600 white@85%
  5. `Spacer`
  6. Two **white** stat tiles (radius 18, tinted icon chips) — generous, not compressed.
- Landlord art `assets/images/card_landlord.svg` · Tenant `assets/images/card_tenant.svg`.

### `CurvedGradientHeader` & `AuthIllustrationHeader`
- Onboarding hero now uses a **concave white scoop** at the panel's bottom edge over a
  deep-purple gradient panel (`#3A2A6B→#2A1B45`); the `_BottomCurveClipper` already
  produces the right concave shape — feed it the onboarding gradient and ~370 height.
- `AuthIllustrationHeader`: swap assets to the new lavender wave + phone-and-lock (see §11),
  height ~350, with 2–3 small **white hovering clouds** drifting (add `AnimatedBuilder`
  float, or pre-baked into the bg). Keep `cloudTint` modulate only if using the old png.

### `FabActionSheet`
- FAB `Ø62`, role bg, white `plus`, elevation soft. Sheet rows reuse list-row pattern.

---

## 9. Screen patterns

- **Splash** (`splash_screen.dart`): centered logo mark (108×120) gentle float; wordmark
  32/800 indigo `#2939A1`; tagline 16/600 Primary.
- **Onboarding intro** (`intro_slides_screen.dart`): top **hero gradient panel** (~370,
  `#3A2A6B→#2A1B45`, soft purple radial glow) with a **concave white scoop** at its bottom
  and the 3D illustration floating; below, centered white content — Kicker (12/800/UPPERCASE
  Primary) → Title (29/800) → Body (16/500 Muted); footer row **Skip** (Muted) · 3 dots
  (active = Primary 22px pill, inactive `#E0DAEC`) · **Next/Get Started** (Primary 800).
  Image map: *Get paid, instantly* = `onb_receive.png`; *Pay with confidence* =
  `onb_secure.png`; *Automate everything* = `onb_reminders.png`.
- **Phone entry / OTP** (`phone_entry_screen.dart`, `otp_screen.dart`): `AuthIllustrationHeader`
  (~350) with lavender wave + floating phone-and-lock + drifting clouds; title 26/700;
  helper 15/600 Primary; fields on `#F4EEFB`; primary CTA.
- **Profile setup** (`profile_setup_screen.dart`): personal-info form + LANDLORD/TENANT
  segmented control.
- **Landlord dashboard / Tenant ledger**: header (`list` + `magnifyingGlass`) → greeting
  (Primary for landlord, amber for tenant) → `SvgSummaryCard` hero → section heading →
  list of property/rental `RoundedCard`s → FAB (landlord).
- **Profile** (`profile_screen.dart`): list rows in a grouped `RoundedCard`.

---

## 10. Motion

- Float loop `translateY 0→-10→0`, 3.2–6s ease-in-out (logo, illustrations, clouds — stagger).
- Screen-in fade `.3–.4s`; sheets rise `translateY 10→0`. Pop `scale .96→1` on success/hero.
- Subtle only — no hard bounce.

---

## 11. Assets

Place under `assets/images/` and declare in `pubspec.yaml`.

| File | Purpose | Status |
|---|---|---|
| `logo_rentflip.svg` | Brand mark (purple + indigo) | **replace** old logo |
| `card_landlord.svg` | Landlord hero bg (purple origami) | **new** |
| `card_tenant.svg` | Tenant hero bg (pink→amber origami) | **new** |
| `onb_receive.png` | Onboarding 1 — cash + receipt | **new** |
| `onb_secure.png` | Onboarding 2 — phone + cash | **new** |
| `onb_reminders.png` | Onboarding 3 — checklist + bell | **new** |
| `phone_and_lock.png` | Phone-with-lock login illustration | **replace** with new art |
| `cloud_background.png` | Lavender wave behind login phone | **replace** with new art |

> SVGs render with `flutter_svg` (`SvgPicture.asset`, `BoxFit.cover`) inside a `ClipRRect`
> at the `1/1.2 AspectRatio`. If you prefer raster, export at ≥3× device width.
> The exact source files are in the Claude project's `assets/` folder (logo-rentflip-mark.svg,
> card-landlord.svg, card-tenant.svg, onb-*.png, auth-phone-new.png, auth-bg-new.png).

---

## 12. Role theming (one switch) → `theme_cubit.dart` / `AppTheme`

| Aspect | Landlord | Tenant |
|---|---|---|
| Accent / seed | `#814BC4` | `#FEB201` |
| Hero card art | `card_landlord.svg` | `card_tenant.svg` |
| Hero caption | "Revenue" | "Transactions" |
| Greeting color | Primary | Tenant amber |
| Primary CTA | purple, white text | amber, **Ink text** |
| Surface tint | `#F4EEFB` | `#FBF1E0` |

Everything else (layout, type, spacing, radius, shadows) is identical across roles.

---

## 13. Code-change checklist (apply to bring the repo to this spec)

**`app_colors.dart`**
- [ ] `brandPurple` `#7A3FD4` → `#814BC4`
- [ ] `landlordGradientStart` → `#9E72D8`, `landlordGradientEnd` → `#6E43AC`
- [ ] `landlordSurface` `#F7F4FD` → `#F4EEFB`
- [ ] `tenantGradientStart` `#F15A24` → `#FEB201`, `tenantGradientEnd` `#EC008C` → `#FF8D5E`
- [ ] `tenantSurface` `#FFF8F5` → `#FBF1E0`
- [ ] `statusCollected/Bg` → `#1E8A4C` / `#DFF7E7`; `statusOutstanding/Bg` → `#C5602F` / `#FFE9DC`
- [ ] `textDark` → `#16121F`
- [ ] add `textMuted #6E6880`, `textFaint #9A95A8`, `textStatLabel #8A8594`, `border #ECEAF1`,
      `segmentBorder #C9B6E6`, `primary100 #E7DEF6`, `statusPending #FE8D47`,
      `statusInfo #2B6FB0`, `statusInfoBg #E7F2FF`, `onboardInk #2A1B45`, `onboardInk2 #3A2A6B`

**`app_dimens.dart`**
- [ ] `rCard` `28` → `20`; `rTile` `20` → `18`; add `rButton 16`, `rHero 26`, `rChip 12`
- [ ] reduce/remove the `× 1.6` multiplier in `smoothShape` (target subtle corners)
- [ ] add `s14`, `s18`

**`app_theme.dart`**
- [ ] both roles: `ink` seed → `#16121F`
- [ ] tighten `displayLarge/Medium` letter-spacing toward `-1.0…-1.4` for big figures

**`pill_button.dart`**
- [ ] primary/ghost shape `StadiumBorder()` → `RoundedRectangleBorder(radius 16)`
- [ ] primary weight w600 → w700; tenant primary uses **Ink** foreground, not white

**`status_pill_badge.dart`**
- [ ] radius 20 → `rPill`; weight w600 → w800; new colors; add `pending`/`receipt` variants

**`svg_summary_card.dart`**
- [ ] wrap in `AspectRatio(1/1.2)`, radius `rHero` (26); bottom-pin stat tiles via `Spacer`

**Widgets to add:** `NoteStrip`; stat-tile + segmented-control helpers if not already factored.

**Assets:** add the 3 onboarding pngs, 2 hero SVGs, new logo, new login art (see §11) and
register them in `pubspec.yaml`.
