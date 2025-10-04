Here’s a **single “source of truth”** you can drop in your repo as `BRAND_GUIDE.md`. After it, I added quick steps to get the recommended fonts.

---

# Zivvi — Brand System (Source of Truth)

_Last updated: {{today}}_

## 0) Brand Essence

- **Name:** Zivvi (pronounced _ZIH-vee_)
- **Tagline:** _Create. Clip. Catch fire._
- **Vibe:** dark canvas + neon energy, fast, creator-first, playful.
- **Logo motif:** **double-V ▶▶** (forward/play).

---

## 1) Logo & Icon

- **Primary mark:** Double-V chevrons “▶▶” in white on a cyan→magenta gradient tile.
- **Wordmark:** `zivvi` (lowercase) in Plus Jakarta Sans or Inter Bold.
- **Clear space:** ≥ height of one chevron around the mark.
- **Don’ts:** no drop shadows on the chevrons, no skewing, don’t recolor the chevrons.
- **App icon:** rounded square (squircle) with gradient background + white ▶▶ centered.

**SVG base (app/icon & avatar)**

```svg
<svg viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <linearGradient id="g" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0%" stop-color="#00F5FF"/>
      <stop offset="100%" stop-color="#FF005C"/>
    </linearGradient>
  </defs>
  <rect rx="220" ry="220" width="1024" height="1024" fill="url(#g)"/>
  <path d="M310 355 L430 512 L310 669" fill="none" stroke="#FFFFFF" stroke-width="90" stroke-linecap="round" stroke-linejoin="round"/>
  <path d="M514 355 L634 512 L514 669" fill="none" stroke="#FFFFFF" stroke-width="90" stroke-linecap="round" stroke-linejoin="round"/>
</svg>
```

---

## 2) Color System

### Core

- **Ink (bg):** `#0A0A0A`
- **Snow (text):** `#FFFFFF`
- **Slate (secondary text):** `#9CA3AF`

### Accent

- **Aqua:** `#00F5FF`
- **Magenta:** `#FF005C`
- **Signature Gradient:** `linear-gradient(135deg, #00F5FF 0%, #FF005C 100%)`

### Usage

- Backgrounds = Ink
- Text = Snow; secondary = Slate
- CTAs / highlights = Gradient (Aqua→Magenta)
- Success/Warning/Error (later) can be derived from accent hues, but keep MVP minimal.

**Tailwind v4 tokens (globals.css)**

```css
@import "tailwindcss";
@theme {
  --color-ink: #0a0a0a;
  --color-snow: #ffffff;
  --color-slate: #9ca3af;
  --color-aqua: #00f5ff;
  --color-magenta: #ff005c;
  --radius-2xl: 1.25rem;
}
```

---

## 3) Typography

### Families

- **Headings (Display/Brand):** Plus Jakarta Sans (fallback Inter)
- **Body/UI:** Inter

### Weights

- Display / H1: **Black 800**
- H2–H3: **Bold 700**
- Body: **Regular 400** / **Medium 500**
- Meta/Caption: **Regular 400**

### Scale (mobile-first)

- **Display XL:** 48–64
- **H1:** 40
- **H2:** 32
- **H3:** 24
- **Body L:** 18
- **Body M:** 16
- **Caption:** 12–14

### Line-height

- Display/H1: 1.05–1.1
- Body: 1.5

---

## 4) Spacing, Radius, Shadows

- **Spacing (4pt):** 4 / 8 / 12 / 16 / 24 / 32 / 48 / 64
- **Radius:** buttons/tags `12px` (`--radius-2xl`), cards `20px`, icon tile `220px`
- **Glows (use sparingly):**

  - Aqua glow: `0 0 24px rgba(0,245,255,0.25)`
  - Magenta glow: `0 0 24px rgba(255,0,92,0.25)`

---

## 5) Motion

- **Feel:** snappy, playful, never jittery.
- **Primary gestures:** vertical swipe (feed), long-press to mute/unmute.
- **Easing:** `cubic-bezier(0.2, 0.8, 0.2, 1)`
- **Micro-interactions:** like pulse, gradient shimmer on primary buttons (≤150ms).

---

## 6) Components (UI Rules)

### Buttons

- **Primary:** gradient fill, white text, radius `12px`, subtle glow on hover.
- **Secondary:** transparent bg, `1px` white/20% border, brighten on hover.

### Inputs

- BG: white/5%, Border: white/10%, Focus: aqua border (no shadow rings).

### Action rail (video card)

- Vertical stack on right: Like / Comment / Share / Sound.
- Counters right-aligned, small (12–14), Slate.

### Cards & Surfaces

- Surfaces = slightly lighter than Ink if needed (avoid heavy gray panels).
- Maintain strong contrast with text/controls.

---

## 7) Layout (Web Landing)

1. **Hero:** Logo, headline with gradient word, two CTAs.
2. **Preview:** phone mockup or placeholder (9:16) with dark frame.
3. **Three features:** Create / Share / Catch fire (icon + one-liner).
4. **CTA band:** gradient stripe w/ “Get the app”.
5. **Footer:** links + © Zivvi.

---

## 8) Accessibility

- Aim contrast ratios ≥ 4.5:1 for text; avoid small Slate on Ink for critical copy.
- Focus styles visible (border aqua).
- Tap targets ≥ 44px.

---

## 9) Content & Tone

- Short, energetic verbs (“Create”, “Drop”, “Remix”, “Catch fire”).
- Avoid jargon. One-liners over paragraphs.

---

## 10) Do / Don’t

**Do**

- Use gradient only for focus elements (logos, CTAs, highlights).
- Keep backgrounds dark to let content pop.
- Keep iconography simple, line-based.

**Don’t**

- Overuse multiple gradients at once.
- Add heavy drop shadows to the ▶▶ mark.
- Stuff long text blocks into the hero.

---

## 11) Developer Cheatsheet

**Gradient text**

```html
<span
  class="bg-gradient-to-br from-aqua to-magenta bg-clip-text text-transparent"
  >Catch fire</span
>
```

**Primary button**

```html
<a
  class="px-5 py-3 rounded-2xl bg-gradient-to-br from-aqua to-magenta font-semibold"
  >Get the App</a
>
```

**Dark section**

```html
<section class="bg-ink text-snow"></section>
```

---

# Font Setup (Next.js & general)

## Recommended Fonts

- **Plus Jakarta Sans** (brand headings)
- **Inter** (UI/body)
  _Both are variable Google Fonts; modern, crisp, global-friendly._

## Next.js (App Router) — install via `next/font`

`apps/web/app/layout.tsx`

```tsx
import "./globals.css";
import { Inter, Plus_Jakarta_Sans } from "next/font/google";

const inter = Inter({
  subsets: ["latin"],
  variable: "--font-inter",
  display: "swap",
});
const pjs = Plus_Jakarta_Sans({
  subsets: ["latin"],
  variable: "--font-pjs",
  display: "swap",
});

export const metadata = { title: "Zivvi — Create. Clip. Catch fire." };

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en" className={`${inter.variable} ${pjs.variable}`}>
      <body className="bg-ink text-snow antialiased">{children}</body>
    </html>
  );
}
```

`apps/web/app/globals.css`

```css
:root {
  --font-inter: "Inter", ui-sans-serif, system-ui, sans-serif;
  --font-pjs: "Plus Jakarta Sans", ui-sans-serif, system-ui, sans-serif;
}

/* Use PJS for headings, Inter for body */
h1,
h2,
h3,
h4,
h5,
h6 {
  font-family: var(--font-pjs);
}
body {
  font-family: var(--font-inter);
}
```

## Outside Next.js

- Download from Google Fonts and include as variable fonts (WOFF2).
- React Native: use Expo Google Fonts packages or local font files (later).

---

If you want, I’ll also generate a **Figma Tokens** JSON or a **Tailwind v4 plugin-less snippet** for your designers so everything stays in sync.
