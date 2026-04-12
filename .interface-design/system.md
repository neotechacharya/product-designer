# Jigar Acharya — Portfolio Design System

> This file is the single source of truth for all pages in this portfolio.  
> Every new page **must** reference this document before writing any CSS or HTML.

---

## 1. Intent

**Who:** Jigar Acharya — Lead Product Designer. Portfolio viewers are hiring managers, founders, and design leads who evaluate depth of craft and product thinking.

**Feel:** Cinematic dark. Like a premium editorial book or a high-end SaaS product in dark mode. Quiet, confident, unhurried. Nothing decorative — every element earns its place.

**Not:** Generic dark dashboard template. No purple gradients, no neon glow, no rounded-corner UI-kit defaults.

---

## 2. Design Tokens (CSS Custom Properties)

Copy this `:root` block verbatim into every page `<style>` tag.

```css
:root {
  --bg:       hsl(0, 0%, 4%);   /* #0a0a0a — canvas */
  --surface:  hsl(0, 0%, 8%);   /* #141414 — cards, panels */
  --text:     hsl(0, 0%, 96%);  /* #f5f5f5 — primary text */
  --muted:    hsl(0, 0%, 53%);  /* #878787 — secondary text, labels */
  --stroke:   hsl(0, 0%, 12%);  /* #1f1f1f — borders */
  --accent-a: #89AACC;          /* steel blue — gradient start */
  --accent-b: #4E85BF;          /* deeper blue — gradient end */
}
```

### Accent gradient
```css
linear-gradient(90deg, var(--accent-a) 0%, var(--accent-b) 100%)
```

Use for: loading bar, logo ring, focus rings, hover glow outlines, CTA borders.  
Never use as a background fill for large surfaces.

### Semantic note
- `--bg` = page canvas. All sections use this unless elevated.
- `--surface` = one elevation step up. Cards, nav pill, dropdowns.
- Borders use `var(--stroke)` = `rgba(31,31,31)` equivalent. Never use a high-contrast border.
- Dividers between sections: `border-top: 1px solid var(--stroke)`

---

## 3. Typography

### Fonts (CDN — include in every page `<head>`)
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Instrument+Serif:ital@1&display=swap" rel="stylesheet">
```

### Rules
| Role | Font | Style | Weight | Notes |
|------|------|-------|--------|-------|
| Body / UI | Inter | normal | 400–600 | All navigation, labels, descriptions |
| Display / Hero name | Instrument Serif | **italic** | 400 | Large hero names, section `<em>` words |
| Stats / Counter | Instrument Serif | **italic** | 400 | Numbers that need presence |
| Testimonial heading | Instrument Serif | **italic** | 400 | Emotional section headings |
| Marquee | Instrument Serif | **italic** | 400 | Ghost-text marquee in footer |

### Scale
```css
/* Eyebrow labels */
font-size: 0.7rem; letter-spacing: 0.3em; text-transform: uppercase; color: var(--muted);

/* Section heading */
font-size: clamp(1.75rem, 3.5vw, 2.75rem); font-weight: 600; color: var(--text); line-height: 1.2;
/* em inside heading → Instrument Serif italic, font-weight: 400 */

/* Body / description */
font-size: 0.875rem–0.95rem; line-height: 1.65–1.75; color: var(--muted);

/* Hero name */
font-size: clamp(3.5rem, 10vw, 9rem); line-height: 0.9; letter-spacing: -0.02em;

/* Stat number */
font-size: clamp(3rem, 6vw, 5rem); line-height: 1;

/* Nav links */
font-size: 0.78rem;

/* Card label / tag */
font-size: 0.68rem; letter-spacing: 0.22em; text-transform: uppercase;

/* Card title */
font-size: clamp(1.5rem, 2.5vw, 2.1rem); Instrument Serif italic;
```

---

## 4. Depth Strategy: Borders Only

This portfolio uses **borders-only** depth. No dramatic drop shadows anywhere.

```css
/* Standard card border */
border: 1px solid var(--stroke);

/* Hover glow outline (replaces border on hover) */
box-shadow: 0 0 0 1px var(--accent-a), 0 0 0 2.5px var(--accent-b);

/* Card hover lift shadow (subtle, not heavy) */
box-shadow: 0 24px 60px rgba(0,0,0,0.45), 0 4px 16px rgba(0,0,0,0.3);

/* Active testimonial avatar */
outline: 3px solid var(--accent-a); outline-offset: 2px;
box-shadow: 0 0 20px rgba(137,170,204,0.25);
```

Never use: colored glow on large surfaces, multi-layer dramatic shadows, `filter: drop-shadow()` on cards.

---

## 5. Border Radius Scale

| Element | Radius |
|---------|--------|
| Pills (nav, buttons) | `9999px` |
| Cards (cs-card, exp-card) | `1.5rem` |
| Stack items | `1.25rem` |
| Card media image | `1rem` |
| Card media glassmorphism border | `1.1rem` |
| Journal entries | `3rem` (pill) |
| Avatar thumbnails | `1.1rem` |
| Icon containers | `50%` (circle) |
| Stack icons | `0.6rem` |

---

## 6. Spacing Scale

Base unit: `0.25rem` (4px). Build on multiples.

| Use | Value |
|-----|-------|
| Icon internal gap | `0.2rem` |
| Inline button gap | `0.4–0.5rem` |
| Label-to-heading gap | `0.75rem` |
| Card inner padding (desktop) | `3rem` |
| Card inner padding (mobile) | `1.75rem` |
| Card gap in list | `1.5rem` |
| Section vertical padding | `6rem 0 7rem` |
| `sec-wrap` max-width | `1200px` with `padding: 0 1.5rem` |
| Section header bottom gap | `margin-bottom: 2.5rem` |

---

## 7. Shared Section Structure

Every section follows this pattern:

```html
<section id="section-id" aria-label="Section Name">
  <div class="sec-wrap">

    <div class="sec-header-row reveal">
      <div>
        <div class="sec-eyebrow">
          <div class="sec-eyebrow__bar"></div>
          <span class="sec-eyebrow__txt">Eyebrow Text</span>
        </div>
        <h2 class="sec-heading">Heading <em>word</em></h2>
        <p class="sec-sub">Optional subtitle.</p>
      </div>
      <!-- optional: <a href="#" class="view-all-link">View all →</a> -->
    </div>

    <!-- section content -->

  </div>
</section>
```

### Required shared CSS (copy to every page)
```css
.sec-wrap  { max-width: 1200px; margin: 0 auto; padding: 0 1.5rem; }

.sec-eyebrow { display: flex; align-items: center; gap: 0.75rem; margin-bottom: 0.75rem; }
.sec-eyebrow--center { justify-content: center; }
.sec-eyebrow__bar { width: 2rem; height: 1px; background: var(--stroke); flex-shrink: 0; }
.sec-eyebrow__txt { font-size: 0.7rem; color: var(--muted); letter-spacing: 0.3em; text-transform: uppercase; }

.sec-heading { font-size: clamp(1.75rem, 3.5vw, 2.75rem); font-weight: 600; color: var(--text); line-height: 1.2; margin-bottom: 0.6rem; }
.sec-heading em { font-family: 'Instrument Serif', serif; font-style: italic; font-weight: 400; }

.sec-sub { font-size: 0.875rem; color: var(--muted); line-height: 1.65; max-width: 30rem; }

.sec-header-row { display: flex; justify-content: space-between; align-items: flex-end; margin-bottom: 2.5rem; }
```

---

## 8. Components

### 8a. Navbar (Floating Pill)

Fixed, centered, backdrop-blur, same on all pages.

```css
#navbar { position: fixed; top: 0; left: 0; right: 0; z-index: 50; display: flex; justify-content: center; padding: 1rem; pointer-events: none; }

.nav__pill { pointer-events: all; display: inline-flex; align-items: center; border-radius: 9999px; backdrop-filter: blur(16px); -webkit-backdrop-filter: blur(16px); border: 1px solid rgba(255,255,255,0.08); background: rgba(20,20,20,0.9); padding: 0.4rem 0.4rem; transition: box-shadow 0.3s ease; }
.nav__pill.scrolled { box-shadow: 0 4px 30px rgba(0,0,0,0.4); }

/* Logo ring — accent gradient */
.nav__logo-ring { background: linear-gradient(135deg, var(--accent-a), var(--accent-b)); border-radius: 50%; }
.nav__logo-inner { font-family: 'Instrument Serif', serif; font-style: italic; font-size: 0.72rem; background: var(--bg); }

/* Links */
.nav__link { font-size: 0.78rem; border-radius: 9999px; padding: 0.35rem 0.8rem; color: var(--muted); }
.nav__link:hover, .nav__link.active { color: var(--text); background: rgba(31,31,31,0.6); }

/* CTA "Say hi" — gradient border on hover via ::before */
.nav__cta::before { content: ''; position: absolute; inset: -2px; border-radius: 9999px; background: linear-gradient(90deg, var(--accent-a), var(--accent-b)); opacity: 0; transition: opacity 0.3s; }
.nav__cta:hover::before { opacity: 1; }
.nav__cta-inner { position: relative; z-index: 1; background: rgba(20,20,20,0.9); border-radius: 9999px; padding: 0.35rem 0.8rem; font-size: 0.78rem; color: var(--text); }
```

Nav links: Home → `#hero`, Work → `#works`, Resume → external Google Doc. CTA mailto.  
JS: scroll position adds `.scrolled` to `#nav-pill`. Active link tracked by section IntersectionObserver.

---

### 8b. Buttons

Two variants. Always full-pill radius.

```css
/* Primary — solid white, inverts on hover with accent ring */
.btn-solid { border-radius: 9999px; padding: 0.8rem 1.75rem; font-size: 0.875rem; font-weight: 500; background: var(--text); color: var(--bg); transition: transform 0.2s, background 0.25s, color 0.25s, box-shadow 0.25s; }
.btn-solid:hover { background: var(--bg); color: var(--text); transform: scale(1.04); box-shadow: 0 0 0 1.5px var(--accent-a), 0 0 0 3px var(--accent-b); }

/* Ghost — dark bg, stroke border, accent ring on hover */
.btn-ghost { border-radius: 9999px; padding: 0.8rem 1.75rem; font-size: 0.875rem; font-weight: 500; background: var(--bg); color: var(--text); border: 2px solid var(--stroke); transition: transform 0.2s, border-color 0.25s, box-shadow 0.25s; }
.btn-ghost:hover { border-color: transparent; transform: scale(1.04); box-shadow: 0 0 0 1.5px var(--accent-a), 0 0 0 3px var(--accent-b); }
```

---

### 8c. Case Study Card (`.cs-card`)

Horizontal layout: media left (52%), content right (44%). Stacks vertically on mobile.

Key patterns:
- **Glassmorphism image border**: `::before` pseudo-element with `inset: -1px`, accent gradient, `opacity: 0.7` at rest → `opacity: 1` on hover
- **3D tilt on hover**: `perspective(1200px) rotateX(0.8deg) rotateY(-0.8deg) translateY(-4px)`
- **Accent glow outline on button hover**: same `box-shadow` double-ring pattern

```css
.cs-card { background: var(--surface); border: 1px solid var(--stroke); border-radius: 1.5rem; overflow: hidden; }
.cs-card:hover { transform: perspective(1200px) rotateX(0.8deg) rotateY(-0.8deg) translateY(-4px); box-shadow: 0 24px 60px rgba(0,0,0,0.45), 0 4px 16px rgba(0,0,0,0.3); border-color: rgba(255,255,255,0.1); }

/* Glassmorphism border */
.cs-card__media { position: relative; }
.cs-card__media::before { content: ''; position: absolute; inset: -1px; border-radius: 1.1rem; background: linear-gradient(135deg, rgba(137,170,204,0.55) 0%, rgba(78,133,191,0.35) 50%, rgba(137,170,204,0.15) 100%); z-index: 0; opacity: 0.7; transition: opacity 0.4s ease; }
.cs-card:hover .cs-card__media::before { opacity: 1; background: linear-gradient(135deg, rgba(137,170,204,0.8) 0%, rgba(78,133,191,0.55) 50%, rgba(137,170,204,0.3) 100%); }
.cs-card__media img { position: relative; z-index: 1; border-radius: 1rem; border: 1px solid rgba(255,255,255,0.06); }

/* Card inner */
.cs-card__inner { display: flex; align-items: center; gap: 3.5rem; padding: 3rem; }
.cs-card__media { flex: 1 1 52%; }
.cs-card__content { flex: 1 1 44%; }

/* Card typography */
.cs-card__label { font-size: 0.68rem; font-weight: 500; letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); margin-bottom: 0.9rem; }
.cs-card__title { font-family: 'Instrument Serif', serif; font-style: italic; font-size: clamp(1.5rem, 2.5vw, 2.1rem); line-height: 1.2; color: var(--text); margin-bottom: 1.1rem; }
.cs-card__desc { font-size: 0.9rem; line-height: 1.75; color: var(--muted); margin-bottom: 1.75rem; }
```

---

### 8d. Expertise Card (`.exp-card`)

Grid: 3 columns on ≥640px. Same surface/border treatment as cs-card.

```css
.exp-card { background: var(--surface); border: 1px solid var(--stroke); border-radius: 1.5rem; padding: 2rem 2rem 2.25rem; }
.exp-card:hover { border-color: rgba(137,170,204,0.2); box-shadow: 0 0 0 1px rgba(137,170,204,0.08), 0 8px 32px rgba(0,0,0,0.3); }

/* Icon circle */
.exp-card__icon { width: 2.75rem; height: 2.75rem; border-radius: 50%; border: 1px solid var(--stroke); display: flex; align-items: center; justify-content: center; margin-bottom: 2rem; color: var(--muted); }
.exp-card:hover .exp-card__icon { border-color: rgba(137,170,204,0.35); color: var(--accent-a); }

.exp-card__title { font-size: 1rem; font-weight: 600; color: var(--text); margin-bottom: 0.6rem; }
.exp-card__desc { font-size: 0.875rem; color: var(--muted); line-height: 1.7; }
```

---

### 8e. Stack Item (`.stack-item`)

Grid: 4 columns on desktop, 2 columns on ≤480px. Lift on hover.

```css
.stack-item { background: var(--surface); border: 1px solid var(--stroke); border-radius: 1.25rem; padding: 1.5rem 1rem 1.25rem; display: flex; flex-direction: column; align-items: center; gap: 1rem; }
.stack-item:hover { border-color: rgba(137,170,204,0.2); box-shadow: 0 0 0 1px rgba(137,170,204,0.08), 0 8px 28px rgba(0,0,0,0.35); transform: translateY(-3px); }
.stack-item__icon { width: 3rem; height: 3rem; object-fit: contain; border-radius: 0.6rem; }
.stack-item__name { font-size: 0.78rem; font-weight: 500; color: var(--muted); }
.stack-item:hover .stack-item__name { color: var(--text); }
```

Icon sources: local `img/tech/` for Photoshop, Figma, Illustrator, Sketch, HTML5, CSS3, Notion.  
JavaScript icon: `https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/javascript/javascript-original.svg` (yellow, readable on dark).

---

### 8f. Journal Entry (`.journal-entry`)

Full-pill row list. Thumbnail + title + meta + arrow.

```css
.journal-entry { display: flex; align-items: center; gap: 1.25rem; padding: 0.9rem 1.1rem; background: rgba(20,20,20,0.3); border: 1px solid var(--stroke); border-radius: 3rem; }
.journal-entry:hover { background: var(--surface); border-color: rgba(255,255,255,0.07); }
.journal-entry__thumb { width: 3.25rem; height: 3.25rem; border-radius: 0.9rem; object-fit: cover; }
.journal-entry__title { font-size: 0.875rem; font-weight: 500; color: var(--text); }
.journal-entry__meta { font-size: 0.72rem; color: var(--muted); }
.journal-entry__arr { color: var(--muted); transition: transform 0.2s, color 0.2s; }
.journal-entry:hover .journal-entry__arr { transform: translate(2px, -2px); color: var(--text); }
```

---

### 8g. Testimonials (`.testi__*`)

3-avatar "fan" layout. Click to switch. Active avatar gets accent outline ring.

**Avatar sizes (nth-child):**
- 1st, 3rd: `width: 108px; height: 82px; margin-bottom: 28px;` (flanking, raised)
- 2nd (center): `width: 136px; height: 104px;` (dominant)

```css
.testi__avatar { border-radius: 1.1rem; opacity: 0.45; transition: transform 0.3s, opacity 0.3s; }
.testi__avatar.active { opacity: 1; }
.testi__avatar.active .testi__avatar-inner { outline: 3px solid var(--accent-a); outline-offset: 2px; box-shadow: 0 0 20px rgba(137,170,204,0.25); }
.testi__avatar img { width: 100%; height: 100%; object-fit: cover; object-position: top center; }

/* Quote */
.testi__item { display: none; font-size: clamp(0.95rem, 1.8vw, 1.125rem); color: var(--muted); line-height: 1.8; text-align: center; }
.testi__item.active { display: block; }
.testi__name { display: block; font-size: 0.9rem; font-weight: 600; color: var(--text); margin-top: 1.75rem; }
.testi__role { display: block; font-size: 0.78rem; color: var(--muted); }

/* Heading uses Instrument Serif italic */
.testi__heading { font-family: 'Instrument Serif', serif; font-style: italic; font-weight: 400; text-align: center; }
```

**JS switcher (vanilla):**
```js
const avatars = document.querySelectorAll('.testi__avatar');
const items   = document.querySelectorAll('.testi__item');
avatars.forEach(av => {
  av.addEventListener('click', () => {
    const idx = av.dataset.idx;
    avatars.forEach(a => a.classList.remove('active'));
    items.forEach(i => i.classList.remove('active'));
    av.classList.add('active');
    document.querySelector(`.testi__item[data-idx="${idx}"]`).classList.add('active');
  });
});
```

---

### 8h. Stats Bar (`#stats`)

3-column grid. Dividers via `border-top` + `border-bottom` on the section.

```css
#stats { background: var(--bg); padding: 5rem 0; border-top: 1px solid var(--stroke); border-bottom: 1px solid var(--stroke); }
.stat__num { font-family: 'Instrument Serif', serif; font-style: italic; font-size: clamp(3rem, 6vw, 5rem); color: var(--text); line-height: 1; margin-bottom: 0.5rem; }
.stat__lbl { font-size: 0.7rem; color: var(--muted); letter-spacing: 0.22em; text-transform: uppercase; }
```

---

### 8i. Footer / Contact

Video background (Mux HLS, flipped vertically with `scaleY(-1)`). Marquee ghost text. CTA email button with gradient border on hover.

```css
.email-btn { position: relative; display: inline-flex; border-radius: 9999px; }
.email-btn::before { content: ''; position: absolute; inset: -1px; border-radius: 9999px; background: linear-gradient(90deg, var(--accent-a), var(--accent-b)); opacity: 0; transition: opacity 0.3s; }
.email-btn:hover::before { opacity: 1; }
.email-btn__inner { position: relative; z-index: 1; background: var(--bg); border-radius: 9999px; border: 1px solid var(--stroke); padding: 0.875rem 2rem; font-size: 0.875rem; color: var(--text); }

/* Marquee ghost text */
.marquee-item { font-family: 'Instrument Serif', serif; font-style: italic; font-size: clamp(3rem, 7vw, 6rem); color: rgba(245,245,245,0.055); }
```

Footer bar: flex row on ≥640px. Contains availability dot (green, pulsing), socials, copyright.

```css
.avail-dot { width: 0.45rem; height: 0.45rem; border-radius: 50%; background: #22c55e; animation: pulse-dot 2s ease-in-out infinite; }
```

---

## 9. Scroll Reveal

All visible section content gets `.reveal`. Stagger children with modifier classes.

```css
.reveal { opacity: 0; transform: translateY(28px); transition: opacity 0.75s cubic-bezier(0.25,0.1,0.25,1), transform 0.75s cubic-bezier(0.25,0.1,0.25,1); }
.reveal.vis { opacity: 1; transform: translateY(0); }
.reveal-delay-1 { transition-delay: 0.1s; }
.reveal-delay-2 { transition-delay: 0.2s; }
.reveal-delay-3 { transition-delay: 0.3s; }
```

```js
const ro = new IntersectionObserver((entries) => {
  entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('vis'); ro.unobserve(e.target); } });
}, { threshold: 0.12 });
document.querySelectorAll('.reveal').forEach(el => ro.observe(el));
```

---

## 10. Animation Keyframes

Include all four in every page (they're cheap and used across components):

```css
@keyframes scroll-down   { 0% { transform: translateY(-100%); } 100% { transform: translateY(200%); } }
@keyframes role-fade-in  { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }
@keyframes gradient-shift { 0% { background-position: 0% 50%; } 50% { background-position: 100% 50%; } 100% { background-position: 0% 50%; } }
@keyframes pulse-dot     { 0%, 100% { opacity: 1; transform: scale(1); } 50% { opacity: 0.4; transform: scale(0.75); } }
```

---

## 11. External Dependencies (CDN)

Include in this exact order before `</head>`:

```html
<!-- Fonts (above) -->

<!-- GSAP + ScrollTrigger -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>

<!-- hls.js (only on pages with video backgrounds) -->
<script src="https://cdn.jsdelivr.net/npm/hls.js@1.5.7/dist/hls.min.js"></script>
```

GSAP is used for hero entrance animations (`.gsap-name`, `.gsap-blur` classes).  
ScrollTrigger is used for scroll-linked marquee animation in footer.  
hls.js is only needed on pages with Mux HLS video backgrounds.

---

## 12. Page Layout for New Pages (Case Study Template)

New pages (e.g., `dashboard-redesign.html`) should:

1. Include the same `<head>` CDN stack (fonts, GSAP, hls.js only if video)
2. Copy the full `:root` token block
3. Copy reset + base, utilities, keyframes, scroll reveal CSS
4. Include the navbar HTML + its CSS exactly as-is
5. Add a hero section — typically a full-width image or video with `.hero__fade-btm`
6. Structure content sections using `.sec-wrap` + `.sec-eyebrow` + `.sec-heading` pattern
7. End with the contact footer or a simplified footer bar

**What NOT to do on sub-pages:**
- Do not add a loading screen (that's only on `index.html`)
- Do not use the GSAP `.gsap-name` / `.gsap-blur` hero animation unless there's a large hero name
- Do not introduce new surface colors or fonts — extend only within the token system

---

## 13. Writing New CSS (Checklist)

Before adding any rule, verify:

- [ ] Color is a `var(--token)` or `rgba()` derived from an existing token — no raw hex except for the two accent values
- [ ] Border uses `var(--stroke)` as base, `rgba(137,170,204,…)` only for accent hover states
- [ ] Font family is Inter or Instrument Serif — no other typefaces
- [ ] Border radius comes from the scale in §5 — no arbitrary values
- [ ] Spacing is a multiple of `0.25rem`
- [ ] No inline `style=""` attributes — all styling in `<style>` block via class names
- [ ] Interactive elements have `:hover` and focus/active states
- [ ] No shadows heavier than `0 24px 60px rgba(0,0,0,0.45)`

---

## 14. Image Assets

| Path | Contents |
|------|----------|
| `img/banner/` | Case study hero images |
| `img/tech/` | Tool icons (Photoshop, Figma, Illustrator, Sketch, HTML5, CSS3, Notion, Blender) |
| `img/avatars/` | Testimonial avatar photos (LinkedIn-style headshots) |
| `img/works/` | Journal article thumbnails |
| `img/favicon/` | `favicon.ico`, `apple-touch-icon.png` |
| `img/og-image.jpg` | Open Graph share image |

JS icon exception: use Devicons CDN (`https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/javascript/javascript-original.svg`) — local icon is black and invisible on dark backgrounds.
