# StepTeddy Website — Landing Page Design

**Date:** 2026-05-29  
**Status:** Approved

---

## Overview

A static 3-page website for the iOS app **StepTeddy** — a step-tracking app with a cute teddy bear mascot. Hosted on **GitHub Pages**, built with pure HTML/CSS/JS (no framework, no build step).

---

## Pages

| File | Purpose |
|---|---|
| `index.html` | Landing page / Startseite |
| `privacy.html` | Privacy Policy (placeholder text) |
| `terms.html` | Terms & Conditions (placeholder text) |

Supporting assets live in `assets/css/`, `assets/images/`.

---

## index.html Layout (top to bottom)

### 1. Nav
- Left: App icon + "StepTeddy" wordmark
- Right: "Download" CTA button (placeholder App Store link)
- Sticky, transparent background that fills on scroll

### 2. Hero
- **Headline:** "Happy Bear, Happy You."
- **Subline:** "StepTeddy's little bear cheers you on with every step — hit your daily goal and watch him shine."
- **CTA Button:** "Download on the App Store" (placeholder link)
- **Visual:** iPhone screenshot IMG_3717-portrait.png (right side on desktop, below text on mobile)
- Two-column layout on desktop, single column stacked on mobile

### 3. Features (3 blocks, alternating image left/right)
1. **Step Tracking** — IMG_3717-portrait.png — "Hit your daily goal. Watch Teddy dance."
2. **Streaks** — IMG_3718-portrait.png — "Build your streak. Don't break the chain."
3. **Badges** — IMG_3717-portrait.png — "Earn badges for every milestone."

Each block: screenshot on one side, icon + feature title + short description on the other. Alternating layout (text-left/text-right) on desktop, always stacked on mobile.

### 4. CTA Banner
- Short motivational line + repeated Download button
- Slightly darker background to visually separate from features

### 5. Footer
- Links: Privacy Policy | Terms & Conditions
- Copyright: © 2026 StepTeddy

---

## Visual Design

| Token | Value | Usage |
|---|---|---|
| Background | `#faf5ed` | Page background |
| Card/Section alt | `#fff7f0` | Alternating section backgrounds |
| Primary / Buttons | `#1b7d45` | CTAs, accent elements |
| Button hover | `#34c759` | Hover state |
| Text primary | `#1c1c1e` | Headlines, body |
| Text secondary | `#6c6c70` | Sublines, captions |
| Text on button | `#ffffff` | Button labels |

**Typography:** `-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif` — matches iOS feel of the app.

**UI style:** Rounded corners throughout, soft drop shadows on iPhone screenshots, no hard borders. Warm and friendly to match the bear mascot.

---

## Responsive Behavior
- Desktop (≥768px): two-column layouts (hero + feature blocks)
- Mobile (<768px): single column, images above text in features

---

## privacy.html & terms.html

Both pages share the same header/footer as index.html. Content is placeholder text (user will fill in later). Layout: centered single-column, max-width 720px, comfortable reading line-length.

---

## .gitignore

Covers:
- macOS system files (`.DS_Store`, `._*`, `.Spotlight-V100`, `.Trashes`)
- Website build artifacts (`node_modules/`, `dist/`, `.cache/`)
- Claude artifacts (`.claude/`)

---

## Out of Scope
- Blog or additional content pages
- Contact form or backend
- Analytics integration
- Dark mode
