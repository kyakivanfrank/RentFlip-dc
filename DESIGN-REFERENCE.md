# MAAMA CIELO NURSERY SCHOOL — Design Reference

> **Source**: Exported from Claude Design (desktop + phone mockups)
> **Original files**: [`_raw/desktop.dc.html`](file:///E:/projects/nextjs/MAAMA CIELO NURSERY SCHOOL%20EDUCATION%20SERVICES/MAAMA CIELO NURSERY SCHOOL%20design%20files/_raw/desktop.dc.html), [`_raw/phone.dc.html`](file:///E:/projects/nextjs/MAAMA CIELO NURSERY SCHOOL%20EDUCATION%20SERVICES/MAAMA CIELO NURSERY SCHOOL%20design%20files/_raw/phone.dc.html), [`_raw/support.js`](file:///E:/projects/nextjs/MAAMA CIELO NURSERY SCHOOL%20EDUCATION%20SERVICES/MAAMA CIELO NURSERY SCHOOL%20design%20files/_raw/support.js)
> **Motto**: _Arise and Shine_

---

## 1. Design Tokens

### Colors

| Token | Hex | Usage |
|---|---|---|
| **Primary Green (dark)** | `#0B4625` | Hero bg, dark sections, accents on dark ground |
| **Primary Green** | `#116A3A` | Body text, nav bg, borders, header, footer bg |
| **Primary Green (light)** | `#01914C` | Hover states, secondary accents |
| **Yellow accent** | `#F3EC29` | CTA buttons, yellow highlight, section labels, selection bg |
| **Yellow accent (hover)** | `#D4CD1B` | CTA hover state |
| **Page background** | `#F8FAF5` | Main body background (soft green-white) |
| **Light green panel** | `#E8F0E4` | Intro section, Why MAAMA CIELO NURSERY SCHOOL section bg |
| **Pale green panel** | `#D1E0CA` | Nav panel bg, Transport section bg, placeholder image bg |
| **White** | `#FFFFFF` | Card bg, logo bg, input bg |
| **Selection bg** | `#F3EC29` with text `#0B4625` | Text selection |

### Typography

| Role | Font | Weights | Usage |
|---|---|---|---|
| **Headings** | `Young Serif`, Georgia, serif | 400 | All section headings, nav links, stat numbers, card titles |
| **Body** | `Outfit`, system-ui, sans-serif | 300, 400, 500, 600, 700 | Body text, labels, buttons, meta text |
| **Monospace** | `ui-monospace, Menlo, monospace` | — | Image path annotations, figcaptions (dev reference only) |

**Google Fonts import**: `Outfit:wght@300;400;500;600;700` + `Young+Serif`

### Text Sizing (Desktop)

| Element | Size | Line Height | Extra |
|---|---|---|---|
| Hero h1 | `clamp(2.4rem, 6.8vw, 5.8rem)` | 1.02 | uppercase, letter-spacing -0.02em |
| Section h2 | `clamp(1.9rem, 3.6vw, 3rem)` | 1.1 | — |
| Large section h2 | `clamp(2.2rem, 5.2vw, 4.6rem)` | 1.04 | uppercase |
| Card h3 | `1.75rem` | 1.08 | — |
| Body text | `1.125rem` | 1.65 | — |
| Small body | `1.0625rem` | 1.65 | — |
| Section label | `11px` | — | weight 700, letter-spacing 0.22em, uppercase |
| Button text | `12–13px` | — | weight 700, letter-spacing 0.16em, uppercase |
| Tag/meta | `10–11px` | — | weight 700, letter-spacing 0.14em, uppercase |

### Animations (Keyframes)

| Name | Description |
|---|---|
| `gd-kb` | Ken Burns zoom (hero background): scale 1.05 → 1.16 with translate, 28s infinite alternate |
| `gd-fade` | Simple opacity 0 → 1 |
| `gd-rise` | Entry: opacity 0 + translateY(26px) → visible, 0.9s cubic-bezier |
| `gd-blink` | Pulse opacity 1 → 0.3 → 1, 3s infinite (scroll indicator) |
| `gd-march` | Marquee: translateX(0) → translateX(-50%), linear infinite |
| `gd-up` | Mobile entry: opacity 0 + translateY(20px) → visible |
| `gd-drawer` | Mobile nav slide: opacity 0 + translateY(-14px) → visible |

### Interaction Patterns

- **Scroll reveal**: `[data-reveal]` elements start at `opacity: 0; translateY(26px)` and animate in via IntersectionObserver (rootMargin `-8%`, threshold 0.05). `data-delay` attribute adds staggered delay in ms.
- **Parallax**: Hero media moves at 0.22× scroll speed (`translate3d`)
- **Progress bar**: Fixed top bar (`#F3EC29`, 3px high) tracks scroll percentage
- **Hover transitions**: Buttons use `transition: background .25s ease, gap .25s ease`; images use `transition: transform .9s cubic-bezier(.2,.7,.2,1)` for subtle zoom on hover
- **Splash screen**: Desktop has a 2-second splash with logo + pencil bg pattern, click to dismiss

---

## 2. Page Sections (12 total, in order)

### Section 01 — Header + Navigation

**Desktop**: Fixed header with logo (top-left) + "Apply" CTA button (yellow) + hamburger menu (green circle, 56px). Full-screen split nav overlay — left panel (55%, pale green `#D1E0CA`) shows nav links in `Young Serif` uppercase, right panel (45%, light green `#E8F0E4`) shows an admissions card image with "Begin your journey" caption.

**Mobile**: Sticky header bar (green `#116A3A`). Logo in white box + school name. Hamburger toggles a drawer nav below header with nav links, "Call office" / "Apply" buttons, and social links (TikTok, WhatsApp).

**Nav items**: Home, About us, Academics, Admissions, Gallery, News, Contact

---

### Section 02 — Splash Screen (desktop only)

Full-screen fixed overlay. Background `#116A3A` with repeating `pencilbg.svg` pattern at 12% opacity. Centered logo, auto-dismisses after 2s or on click.

---

### Section 03 — Hero

**Background**: Video with Ken Burns zoom animation (poster fallback from Unsplash). Dark gradient overlay: `linear-gradient(to top, rgba(11,70,37,.94) 0%, rgba(17,106,58,.42) 50%, rgba(17,106,58,.36) 100%)`. Parallax scroll at 0.22×.

**Content** (bottom-aligned):
- Yellow label: "— Arise and Shine" (with 34px yellow line before text)
- H1: "MAAMA CIELO NURSERY SCHOOL" (uppercase, Young Serif, white, text-shadow)
- Subtitle: "A nursery and primary school on Kimera Road, Kasubi — quality holistic education..."
- Two CTAs: "Apply for 2027" (yellow solid) + "Watch the school film" (white outline, play icon)
- Scroll indicator: blinking "Scroll to explore" with down-arrow icon

**Desktop**: Full viewport height (100vh, min 620px). Max-width 1180px content.
**Mobile**: 76vh height (min 520px). Stacked CTAs. "Swipe up" instead of "Scroll to explore".

---

### Section 04 — Intro ("Who We Are")

**Label**: `01 — Who we are`
**Background**: `#E8F0E4` with decorative block `#D1E0CA` (64% width, 56% height, top-left, desktop only)

**Content**:
- H2: "Nurturing Tomorrow's Leaders Today" (Young Serif, uppercase)
- Body text: "For over 7 years MAAMA CIELO NURSERY SCHOOL has grown from a humble nursery..."
- Image: `opportunities-bg.jpeg` (mix-blend-mode: multiply, opacity 0.92)

**Stats row** (4 items, 2px green top border each):

| Stat | Label |
|---|---|
| 7 yrs | Nurturing learners |
| Baby – P6 | One continuous ladder |
| 1 : 20 | Teacher to class |
| Kasubi | Rubaga Division |

**Desktop**: 2-column grid (text left, image right) + 4-column stats below.
**Mobile**: Single column, 2×2 stats grid.

---

### Section 05 — Marquee Ticker

Green bar (`#116A3A`) with yellow text scrolling infinitely: "Arise and Shine · Baby Class to Primary 6 · Kimera Road, Kasubi · Arise and Shine · Small classes, known by name ·" (duplicated for seamless loop). Young Serif, uppercase. 2px dark green borders top/bottom.

Desktop: 26s animation, ~1.75rem font. Mobile: 20s, 1rem font.

---

### Section 06 — Our Story

**Label**: `02 — Our story`
**Background**: `#F8FAF5`

**Content**:
- Founder photo (placeholder from Unsplash, grayscale filter → color on hover, 2px green border + 8px white padding)
- H2: "Started by educators who wanted a school they would send their own children to."
- Body: "What began in 2019 as a single nursery class..."
- "Read the full story" button (green solid) → opens modal

**Desktop**: 2-column grid (image left, text right). Photo aspect-ratio 4/5.
**Mobile**: Single column (image first, then text). Photo aspect-ratio 4/3.

---

### Section 07 — Vision & Mission

**Label**: `03 — Vision & mission`
**Background**: `#116A3A` (dark green), white text

**Desktop**: 2-column grid with 2px yellow top border per column
- **Vision**: "To be the centre of excellence for quality holistic education..." (Young Serif, ~1.9rem)
- **Mission**: Two paragraphs about holistic child development and inclusive learning

**Mobile**: Accordion — tap to expand/collapse each (+ / – toggle). Yellow top borders.

---

### Section 08 — Programs

**Label**: `04 — Programs`
**Background**: `#0B4625` (darkest green), white text, 2px yellow top border

H2: "Explore our programs"

**Three program cards**:

| Card | Kicker | Title | Grades |
|---|---|---|---|
| 1 | Early childhood education | Nursery Section | Baby Class to Top Class |
| 2 | Foundational learning | Lower Primary | Primary 1 to Primary 3 |
| 3 | Preparing for the future | Upper Primary | Primary 4 to Primary 6 |

Each card: green bg (`#116A3A`), 2px white/25% border, image (placeholder), kicker in yellow, title in Young Serif, "Explore program" link with arrow icon. Hover: bg → `#01914C`, border → yellow.

**Desktop**: 3-column grid, images from picsum.photos.
**Mobile**: Horizontal swipeable rail (78% width cards, scroll-snap).

---

### Section 09 — Life at MAAMA CIELO NURSERY SCHOOL (Gallery)

**Label**: `05 — Life at MAAMA CIELO NURSERY SCHOOL`
**Background**: `#F8FAF5`

- H2: "Classrooms, sport and school life"
- "See full gallery" link with arrow
- Filter buttons: All, Classrooms, Co-curricular, Campus, Sports, Transport (active = green fill)
- 4-column photo grid (aspect 4/5, 2px green borders, hover zoom). Each has caption + image path.
- Below: 2-column row for wider landscape images (aspect 16/10)

**Desktop**: Grid layout with placeholder images from picsum.
**Mobile**: 2-column grid with "Photo needed" placeholders + full-width landscape below.

---

### Section 10 — Why MAAMA CIELO NURSERY SCHOOL

**Label**: `06 — Why MAAMA CIELO NURSERY SCHOOL`
**Background**: `#E8F0E4`, 2px green top border

H2: "Four reasons parents choose us"

**Four items** (each with 2px green top border, numbered):

| # | Title | Body |
|---|---|---|
| 01 | Small classes | Class sizes are capped so every child is known by name and progress is tracked individually. |
| 02 | Qualified staff | Teachers are trained and certified in early childhood or primary education, with continuous in-service training. |
| 03 | Safe, supervised campus | Gated entry, a sign-in and sign-out log, and staff supervision at every break. |
| 04 | Moral values | A God-fearing environment where integrity, responsibility and respect are taught alongside academics. |

**Safety panel** (dark green box below):
Label: "Safety at a glance" (yellow)

| Title | Body |
|---|---|
| Gated, supervised entry | One controlled gate staffed through the school day; visitors sign in at the office. |
| Camera coverage | Cameras cover the entrance and shared outdoor areas. |
| Named pickup only | Children are released only to the named guardian, or an alternate confirmed by phone. |

---

### Section 11 — Meet the Staff

**Label**: `07 — Meet the staff`
**Background**: `#F8FAF5`

H2: "The people in the classrooms"

**Staff cards** (clickable, open bio modal):

| Role | Department | Image path |
|---|---|---|
| Head Teacher | School administration | `staff/head-teacher.jpg` |
| Deputy Head Teacher | Academics | `staff/deputy.jpg` |
| Nursery Coordinator | Early childhood | `staff/nursery-coordinator.jpg` |
| Admissions Desk | Enrolment support | `staff/admissions.jpg` (desktop only) |

Photo style: 2px green border, 8px white padding, grayscale → color on hover, aspect 4/5.

**Desktop**: 4-column grid.
**Mobile**: Horizontal swipeable rail (62% width cards).

---

### Section 12 — Transport

**Label**: `08 — Transport`
**Background**: `#D1E0CA`, 2px green top border

H2: "Door to gate, every morning"

**3-slide carousel** with prev/next buttons:

| Slide | Kicker | Title | Body |
|---|---|---|---|
| 1 | Routes | Kasubi, Bwaise, Kawaala and Makerere | Vans run three morning and three evening routes... |
| 2 | On board | A matron on every trip | Each van carries a trained matron alongside the driver... |
| 3 | Safety | Serviced monthly, speed-limited | Vehicles are serviced monthly, fitted with working seat belts... |

**Desktop**: 2-column (image left, text right) inside a white-bg bordered card. Prev/next buttons in header.
**Mobile**: Single card with image above text, counter + prev/next at bottom.

---

### Section 13 — Testimonials

**Label**: `09 — Parents`
**Background**: `#0B4625` (darkest green), white text

H2: "What families say"

**Three testimonial cards** (clickable):

| Quote | Name | Meta |
|---|---|---|
| "My daughter went from shy to reading aloud in front of her class in two terms." | Zubeda N. | Parent · Top Class |
| "The teachers call me before I have to call them. That is rare." | Parent testimonial | Parent · P2 · consent pending |
| "Small classes were the reason we moved. We have not looked back." | Parent testimonial | Parent · P5 · consent pending |

Card: green bg (`#116A3A`), 2px white/25% border, min-height 280px. Hover: bg → `#01914C`, border → yellow.

**Desktop**: 3-column grid.
**Mobile**: Horizontal swipeable rail (82% width cards).

---

### Section 14 — News & Events

**Label**: `10 — News & events`
**Background**: `#F8FAF5`

H2: "Latest from MAAMA CIELO NURSERY SCHOOL" + "All news" link

**Three news items** (each with 1px green/25% top border):

| Date | Title | Blurb |
|---|---|---|
| 24 July 2026 | Term III opens on 8 September | Reporting day, requirements and the fees deadline. |
| 10 July 2026 | Sports day: house results | Tug of war, athletics and the swimming gala. |
| 28 June 2026 | P6 end-of-term assessment results | Class averages, most-improved learners and remedial arrangements. |

**Desktop**: 3-column grid. **Mobile**: Stacked list.

---

### Section 15 — CTA (Call to Action)

**Background**: `#F3EC29` (yellow), text `#0B4625`

H2: "Ready to join MAAMA CIELO NURSERY SCHOOL?" (Young Serif, uppercase, large)
Body: "Applications for Term I are open..."

**Two CTAs**:
- "Start an application" (green solid button)
- "Quick inquiry" (dark green outline button) → opens inquiry modal with form

---

### Section 16 — Footer

**Background**: `#116A3A`, white text

**Content**:
- Logo in white box
- Tagline: "Nurturing tomorrow's leaders today."
- "Contact us" (white outline) + "Apply now" (yellow) buttons

**Four footer columns** (separated by 1px white/25% border):
1. **Our campus**: Address (P.O. Box 35627, Kampala / Kasubi–Rubaga Division / Along Kimera Road / Near Makerere University) + phone
2. **Programs**: Nursery Section, Lower Primary, Upper Primary, Co-curricular activities
3. **Admissions**: How to apply, Fees structure, Schedule a visit, FAQs
4. **Explore**: About us, Gallery, News & events, School calendar

**Bottom bar**: "© 2026 MAAMA CIELO NURSERY SCHOOL. All rights reserved." + "Arise and Shine"

**Mobile**: 2-column footer links. Floating social FAB (TikTok, WhatsApp, Apply) bottom-right.

---

## 3. Components

### Buttons

| Variant | Style |
|---|---|
| **Primary CTA** | bg `#F3EC29`, text `#0B4625`, uppercase, weight 700, letter-spacing 0.16em, padding 18px 24px. Hover: bg `#D4CD1B` |
| **Green solid** | bg `#116A3A`, text white. Hover: bg `#01914C` |
| **White outline** | bg transparent, border 2px white/70%, text white. Hover: border yellow, bg yellow, text dark green |
| **Dark outline** | bg transparent, border 2px `#0B4625`, text `#0B4625`. Hover: bg `#0B4625`, text yellow |
| **Hamburger** | bg `#01914C`, white, 56px circle, box-shadow. Hover: bg `#116A3A`, rotate 90° |

All buttons: `font-family: inherit; cursor: pointer; transition: 0.25s ease`

### Modal / Lightbox

Full-screen overlay (bg `rgba(11,70,37,.88)`). White content box (`#F8FAF5`, 2px green border, max-width 840px). Sticky header with kicker + title + close button. Body with optional frame (for images/video), text, and optional inquiry form.

**Desktop**: Centered, max-height 86vh, fade + rise animation.
**Mobile**: Bottom sheet style (aligned to bottom), max-height 92vh, yellow top border, slide-up animation.

### Inquiry Form

Fields: Parent/guardian name (text), Phone/WhatsApp (tel, placeholder "+256"), Class of interest (select: Baby Class, Middle/Top Class, Primary 1–3, Primary 4–6), Preferred term (select: Term I, II, III — desktop only).

Input style: 2px green border, white bg, 14px padding, inherit font, green text, 1rem size.

### Image Treatment

- **Bordered frame**: 2px green border, 8px white padding inside
- **Grayscale portraits**: `filter: grayscale(100%)`, hover → `filter: grayscale(0)` + subtle scale(1.04)
- **Gallery images**: 2px green border, hover scale(1.06), 0.9s cubic-bezier transition
- **Blend mode images**: `mix-blend-mode: multiply; opacity: 0.92` (used for illustrations)

---

## 4. Asset Map

### Existing Assets ✅

| Path | Type | Used in |
|---|---|---|
| `assets/images/logo/logo.svg` | SVG | Header, splash, footer (both views) |
| `assets/images/logo/pencilbg.svg` | SVG | Splash screen background pattern (desktop) |
| `assets/images/menu/admissions-card.jpg` | JPG | Nav overlay right panel (desktop) |
| `assets/images/opportunities-bg.jpeg` | JPEG | Intro section illustration (both views) |

### Needed Assets (placeholders in design) ⚠️

| Path | Type | Section |
|---|---|---|
| `assets/images/about/founder.jpg` | JPG | Our Story — founder portrait |
| `assets/images/about/founders-early-years.jpg` | JPG | Our Story modal frame |
| `assets/images/programs/nursery.jpg` | JPG | Program card — Nursery |
| `assets/images/programs/lower-primary.jpg` | JPG | Program card — Lower Primary |
| `assets/images/programs/upper-primary.jpg` | JPG | Program card — Upper Primary |
| `assets/images/gallery/classrooms/01.jpg` | JPG | Gallery — Top Class literacy |
| `assets/images/gallery/classrooms/02.jpg` | JPG | Gallery — P3 mathematics |
| `assets/images/gallery/cca/swimming.jpg` | JPG | Gallery — Swimming CCA |
| `assets/images/gallery/cca/tug-of-war.jpg` | JPG | Gallery — Tug of war |
| `assets/images/gallery/cca/mdd.jpg` | JPG | Gallery — Music, dance and drama |
| `assets/images/gallery/campus/compound.jpg` | JPG | Gallery — The compound at break |
| `assets/images/staff/head-teacher.jpg` | JPG | Staff card |
| `assets/images/staff/deputy.jpg` | JPG | Staff card |
| `assets/images/staff/nursery-coordinator.jpg` | JPG | Staff card |
| `assets/images/staff/admissions.jpg` | JPG | Staff card (desktop only) |
| `assets/images/transport/van-exterior.jpg` | JPG | Transport carousel slide 1 |
| `assets/images/transport/van-interior.jpg` | JPG | Transport carousel slide 2 |
| `assets/images/transport/safety.jpg` | JPG | Transport carousel slide 3 |
| `assets/videos/hero-background.mp4` | MP4 | Hero section (desktop) |
| `assets/videos/hero-background-portrait.mp4` | MP4 | Hero section (mobile) |
| `assets/videos/testimonials/zubeda.mp4` | MP4 | Zubeda N. video testimonial |

---

## 5. Contact Information

| | |
|---|---|
| **School name** | MAAMA CIELO NURSERY SCHOOL |
| **Address** | P.O. Box 35627, Kampala |
| **Location** | Kasubi–Rubaga Division, Along Kimera Road, Near Makerere University |
| **Phone** | +256 772 330488 |
| **WhatsApp** | wa.me/256772330488 |
| **TikTok** | @MAAMA CIELO NURSERY SCHOOL |

---

## 6. Mobile vs Desktop — Key Differences

| Feature | Desktop | Mobile |
|---|---|---|
| **Header** | Fixed, transparent over hero | Sticky green bar |
| **Navigation** | Full-screen split overlay | Dropdown drawer below header |
| **Splash** | Yes (2s auto-dismiss) | No |
| **Hero height** | 100vh (min 620px) | 76vh (min 520px) |
| **CTAs layout** | Inline row | Stacked column |
| **Vision/Mission** | Side-by-side columns | Accordion (tap to expand) |
| **Program cards** | 3-column grid | Swipeable horizontal rail |
| **Gallery** | 4-column + 2-column grid | 2-column grid |
| **Staff cards** | 4-column grid | Swipeable horizontal rail |
| **Testimonials** | 3-column grid | Swipeable horizontal rail |
| **Transport** | 2-column card (image + text) | Stacked card |
| **Modal** | Centered, max-width 840px | Bottom sheet |
| **Social links** | In nav overlay | Floating FAB (bottom-right) |
| **Footer** | 4-column grid | 2-column grid |
