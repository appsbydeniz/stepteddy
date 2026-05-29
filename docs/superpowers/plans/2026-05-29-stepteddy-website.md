# StepTeddy Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a 3-page static website (landing page, privacy policy, terms) for the StepTeddy iOS app, hosted on GitHub Pages.

**Architecture:** Pure HTML/CSS/JS — no framework, no build step. Three pages share a common nav/footer via copy. One stylesheet with CSS custom properties for the brand color system. Fully responsive.

**Tech Stack:** HTML5, CSS3 (custom properties, flexbox, grid), vanilla JS (scroll nav effect only), GitHub Pages

---

## File Map

```
/Users/deniz.ilkaya/Websites/StepTeddy/
├── .gitignore
├── index.html
├── privacy.html
├── terms.html
└── assets/
    ├── css/
    │   └── styles.css
    ├── js/
    │   └── main.js
    └── images/
        ├── app-icon.png        ← copied from app assets
        ├── hero-iphone.png     ← IMG_3717-portrait.png
        └── streaks-iphone.png  ← IMG_3718-portrait.png
```

**Note:** `hello@stepteddy.app` is a placeholder email in privacy.html and terms.html — replace before launch.

---

### Task 1: Project setup & assets

**Files:**
- Create: `.gitignore`
- Create: `assets/css/`, `assets/js/`, `assets/images/` (directories)
- Copy: app icon + iPhone screenshots into `assets/images/`

- [ ] **Step 1: Create .gitignore**

Create `/Users/deniz.ilkaya/Websites/StepTeddy/.gitignore`:
```
# macOS
.DS_Store
._*
.Spotlight-V100
.Trashes
.AppleDouble
.LSOverride

# Website build artifacts
node_modules/
dist/
.cache/
*.log

# Claude
.claude/
```

- [ ] **Step 2: Create asset directories**

```bash
mkdir -p /Users/deniz.ilkaya/Websites/StepTeddy/assets/css
mkdir -p /Users/deniz.ilkaya/Websites/StepTeddy/assets/js
mkdir -p /Users/deniz.ilkaya/Websites/StepTeddy/assets/images
```

- [ ] **Step 3: Copy app icon**

```bash
cp "/Users/deniz.ilkaya/PersonalProjects/Pawdometer/pawdometer/Pawdometer/Pawdometer/Assets.xcassets/AppIcon.appiconset/Pawdometer_AppIcon.png" \
   /Users/deniz.ilkaya/Websites/StepTeddy/assets/images/app-icon.png
```

- [ ] **Step 4: Copy iPhone screenshots**

```bash
cp /Users/deniz.ilkaya/Websites/StepTeddy/iphone_images/IMG_3717-portrait.png \
   /Users/deniz.ilkaya/Websites/StepTeddy/assets/images/hero-iphone.png

cp /Users/deniz.ilkaya/Websites/StepTeddy/iphone_images/IMG_3718-portrait.png \
   /Users/deniz.ilkaya/Websites/StepTeddy/assets/images/streaks-iphone.png
```

- [ ] **Step 5: Initialize git repo and commit**

```bash
cd /Users/deniz.ilkaya/Websites/StepTeddy
git init
git add .gitignore assets/images/
git commit -m "chore: init repo with gitignore and images"
```

Expected output: `[main (root-commit) xxxxxxx] chore: init repo with gitignore and images`

---

### Task 2: CSS foundation — variables, reset, typography, buttons, layout

**Files:**
- Create: `assets/css/styles.css`

- [ ] **Step 1: Create styles.css with custom properties, reset, and base styles**

Create `assets/css/styles.css`:
```css
/* ── Custom properties ─────────────────────────────── */
:root {
  --bg:              #faf5ed;
  --card:            #fff7f0;
  --primary:         #1b7d45;
  --primary-hover:   #34c759;
  --text:            #1c1c1e;
  --text-secondary:  #6c6c70;
  --text-on-btn:     #ffffff;
  --radius:          16px;
  --radius-pill:     100px;
  --shadow-phone:    0 24px 80px rgba(0, 0, 0, 0.15);
  --max-width:       1100px;
  --font:            -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
}

/* ── Reset ─────────────────────────────────────────── */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html { scroll-behavior: smooth; }

body {
  background-color: var(--bg);
  color: var(--text);
  font-family: var(--font);
  font-size: 17px;
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}

img { max-width: 100%; display: block; }
a   { color: inherit; text-decoration: none; }

/* ── Layout ─────────────────────────────────────────── */
.container {
  max-width: var(--max-width);
  margin: 0 auto;
  padding: 0 24px;
}

/* ── Buttons ─────────────────────────────────────────── */
.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 14px 28px;
  border-radius: var(--radius-pill);
  font-family: var(--font);
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  border: none;
  transition: background-color 0.2s ease, transform 0.1s ease;
  text-decoration: none;
}

.btn--primary {
  background-color: var(--primary);
  color: var(--text-on-btn);
}

.btn--primary:hover  { background-color: var(--primary-hover); }
.btn--primary:active { transform: scale(0.98); }

.btn--sm {
  padding: 10px 20px;
  font-size: 15px;
}
```

- [ ] **Step 2: Commit**

```bash
cd /Users/deniz.ilkaya/Websites/StepTeddy
git add assets/css/styles.css
git commit -m "style: CSS foundation — variables, reset, layout, buttons"
```

---

### Task 3: Nav bar

**Files:**
- Create: `index.html`
- Create: `assets/js/main.js`
- Modify: `assets/css/styles.css`

- [ ] **Step 1: Create index.html with nav**

Create `index.html`:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>StepTeddy — Happy Bear, Happy You.</title>
  <meta name="description" content="StepTeddy's little bear cheers you on with every step — hit your daily goal and watch him shine.">
  <link rel="icon" type="image/png" href="assets/images/app-icon.png">
  <link rel="stylesheet" href="assets/css/styles.css">
</head>
<body>

  <nav class="nav" id="nav">
    <div class="container nav__container">
      <a href="index.html" class="nav__brand">
        <img src="assets/images/app-icon.png" alt="StepTeddy" class="nav__icon">
        <span class="nav__name">StepTeddy</span>
      </a>
      <a href="#download" class="btn btn--primary btn--sm">Download</a>
    </div>
  </nav>

  <!-- Sections will be added in subsequent tasks -->

  <script src="assets/js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Add nav CSS to styles.css**

Append to `assets/css/styles.css`:
```css
/* ── Nav ─────────────────────────────────────────────── */
.nav {
  position: sticky;
  top: 0;
  z-index: 100;
  padding: 16px 0;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.nav.scrolled {
  background-color: rgba(250, 245, 237, 0.92);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  box-shadow: 0 1px 0 rgba(0, 0, 0, 0.08);
}

.nav__container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav__brand {
  display: flex;
  align-items: center;
  gap: 10px;
}

.nav__icon {
  width: 36px;
  height: 36px;
  border-radius: 8px;
}

.nav__name {
  font-size: 18px;
  font-weight: 700;
}
```

- [ ] **Step 3: Create main.js for scroll effect**

Create `assets/js/main.js`:
```javascript
const nav = document.getElementById('nav');
window.addEventListener('scroll', () => {
  nav.classList.toggle('scrolled', window.scrollY > 20);
});
```

- [ ] **Step 4: Open index.html in browser and verify**

Open `file:///Users/deniz.ilkaya/Websites/StepTeddy/index.html` in Safari or Chrome.

Expected:
- Cream background (`#faf5ed`)
- Nav: bear icon + "StepTeddy" left, green "Download" pill button right
- Scroll down (add temporary tall content or use dev tools) → nav becomes frosted glass

- [ ] **Step 5: Commit**

```bash
cd /Users/deniz.ilkaya/Websites/StepTeddy
git add index.html assets/js/main.js assets/css/styles.css
git commit -m "feat: add sticky nav with scroll effect"
```

---

### Task 4: Hero section

**Files:**
- Modify: `index.html`
- Modify: `assets/css/styles.css`

- [ ] **Step 1: Add hero HTML inside index.html, between `<nav>` and the script tag**

```html
  <section class="hero">
    <div class="container hero__container">
      <div class="hero__content">
        <h1 class="hero__headline">Happy Bear,<br>Happy You.</h1>
        <p class="hero__subline">StepTeddy's little bear cheers you on with every step — hit your daily goal and watch him shine.</p>
        <a href="#download" class="btn btn--primary hero__cta">⬇ Download on the App Store</a>
      </div>
      <div class="hero__visual">
        <img
          src="assets/images/hero-iphone.png"
          alt="StepTeddy app — daily step tracking screen"
          class="hero__iphone"
        >
      </div>
    </div>
  </section>
```

- [ ] **Step 2: Add hero CSS to styles.css**

Append to `assets/css/styles.css`:
```css
/* ── Hero ────────────────────────────────────────────── */
.hero {
  padding: 80px 0 60px;
}

.hero__container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  gap: 60px;
}

.hero__headline {
  font-size: clamp(40px, 6vw, 64px);
  font-weight: 800;
  line-height: 1.1;
  letter-spacing: -1.5px;
  margin-bottom: 20px;
}

.hero__subline {
  font-size: 19px;
  color: var(--text-secondary);
  max-width: 440px;
  margin-bottom: 32px;
}

.hero__cta {
  font-size: 17px;
  padding: 16px 32px;
}

.hero__visual {
  display: flex;
  justify-content: center;
}

.hero__iphone {
  width: 280px;
  border-radius: 40px;
  box-shadow: var(--shadow-phone);
}
```

- [ ] **Step 3: Open in browser and verify**

Expected: Two-column layout — left: large bold "Happy Bear, Happy You." headline, gray subline, green download button; right: iPhone screenshot with soft shadow. Both columns vertically centered.

- [ ] **Step 4: Commit**

```bash
cd /Users/deniz.ilkaya/Websites/StepTeddy
git add index.html assets/css/styles.css
git commit -m "feat: add hero section"
```

---

### Task 5: Features section

**Files:**
- Modify: `index.html`
- Modify: `assets/css/styles.css`

- [ ] **Step 1: Add features HTML inside index.html, after the hero section**

```html
  <section class="features">
    <div class="container">

      <div class="feature">
        <div class="feature__content">
          <span class="feature__icon">👟</span>
          <h2 class="feature__title">Hit your daily goal. Watch Teddy dance.</h2>
          <p class="feature__desc">Track your steps in real time and watch Teddy's mood change as you get closer to your goal. The closer you get, the happier he gets.</p>
        </div>
        <div class="feature__visual">
          <img src="assets/images/hero-iphone.png" alt="Step tracking screen" class="feature__iphone">
        </div>
      </div>

      <div class="feature feature--reverse">
        <div class="feature__content">
          <span class="feature__icon">🔥</span>
          <h2 class="feature__title">Build your streak. Don't break the chain.</h2>
          <p class="feature__desc">Hit your step goal every day and build a streak. Teddy's got your back — and a freeze for those off days.</p>
        </div>
        <div class="feature__visual">
          <img src="assets/images/streaks-iphone.png" alt="Streak calendar screen" class="feature__iphone">
        </div>
      </div>

      <div class="feature">
        <div class="feature__content">
          <span class="feature__icon">🏅</span>
          <h2 class="feature__title">Earn badges for every milestone.</h2>
          <p class="feature__desc">From your first 1K steps to 30-day streaks — StepTeddy rewards every achievement with a badge worth showing off.</p>
        </div>
        <div class="feature__visual">
          <img src="assets/images/hero-iphone.png" alt="Badges on the main screen" class="feature__iphone">
        </div>
      </div>

    </div>
  </section>
```

- [ ] **Step 2: Add features CSS to styles.css**

Append to `assets/css/styles.css`:
```css
/* ── Features ────────────────────────────────────────── */
.features {
  padding: 40px 0 80px;
}

.feature {
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  gap: 80px;
  padding: 72px 0;
}

.feature + .feature {
  border-top: 1px solid rgba(0, 0, 0, 0.06);
}

.feature--reverse .feature__content { order: 2; }
.feature--reverse .feature__visual  { order: 1; }

.feature__icon {
  font-size: 40px;
  display: block;
  margin-bottom: 16px;
}

.feature__title {
  font-size: clamp(24px, 3.5vw, 36px);
  font-weight: 700;
  line-height: 1.2;
  letter-spacing: -0.5px;
  margin-bottom: 16px;
}

.feature__desc {
  font-size: 17px;
  color: var(--text-secondary);
  max-width: 420px;
}

.feature__visual {
  display: flex;
  justify-content: center;
}

.feature__iphone {
  width: 240px;
  border-radius: 40px;
  box-shadow: var(--shadow-phone);
}
```

- [ ] **Step 3: Open in browser and verify**

Expected: 3 feature blocks separated by hairline dividers. Block 1: text left, phone right. Block 2: phone left, text right. Block 3: text left, phone right. Each block has an emoji icon, bold title, gray description.

- [ ] **Step 4: Commit**

```bash
cd /Users/deniz.ilkaya/Websites/StepTeddy
git add index.html assets/css/styles.css
git commit -m "feat: add features section with alternating layout"
```

---

### Task 6: CTA banner + Footer

**Files:**
- Modify: `index.html`
- Modify: `assets/css/styles.css`

- [ ] **Step 1: Add CTA + footer HTML inside index.html, after the features section and before the script tag**

```html
  <section class="cta" id="download">
    <div class="container cta__container">
      <h2 class="cta__headline">Start walking. Make Teddy happy.</h2>
      <a href="https://apps.apple.com/app/PLACEHOLDER" class="btn btn--primary cta__btn">
        ⬇ Download on the App Store
      </a>
    </div>
  </section>

  <footer class="footer">
    <div class="container footer__container">
      <p class="footer__copy">© 2026 StepTeddy</p>
      <nav class="footer__links">
        <a href="privacy.html">Privacy Policy</a>
        <a href="terms.html">Terms &amp; Conditions</a>
      </nav>
    </div>
  </footer>
```

- [ ] **Step 2: Add CTA + footer CSS to styles.css**

Append to `assets/css/styles.css`:
```css
/* ── CTA Banner ──────────────────────────────────────── */
.cta {
  background-color: var(--card);
  padding: 100px 0;
  text-align: center;
}

.cta__headline {
  font-size: clamp(28px, 4vw, 44px);
  font-weight: 800;
  letter-spacing: -1px;
  margin-bottom: 32px;
}

.cta__btn {
  font-size: 17px;
  padding: 16px 36px;
}

/* ── Footer ──────────────────────────────────────────── */
.footer {
  padding: 32px 0;
  border-top: 1px solid rgba(0, 0, 0, 0.08);
}

.footer__container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.footer__copy {
  color: var(--text-secondary);
  font-size: 14px;
}

.footer__links {
  display: flex;
  gap: 24px;
}

.footer__links a {
  color: var(--text-secondary);
  font-size: 14px;
  transition: color 0.2s;
}

.footer__links a:hover { color: var(--primary); }
```

- [ ] **Step 3: Open in browser and verify**

Expected: CTA section with `#fff7f0` background (slightly warmer than page), large bold headline centered, green download button. Footer: copyright left, two text links right.

- [ ] **Step 4: Commit**

```bash
cd /Users/deniz.ilkaya/Websites/StepTeddy
git add index.html assets/css/styles.css
git commit -m "feat: add CTA banner and footer"
```

---

### Task 7: Responsive styles (mobile)

**Files:**
- Modify: `assets/css/styles.css`

- [ ] **Step 1: Add mobile breakpoint to styles.css**

Append to `assets/css/styles.css`:
```css
/* ── Responsive — mobile (<768px) ───────────────────── */
@media (max-width: 767px) {
  /* Hero: stack vertically, center */
  .hero__container {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 40px;
  }

  .hero__subline {
    max-width: 100%;
    margin-left: auto;
    margin-right: auto;
  }

  .hero__visual { order: -1; }

  .hero__iphone { width: 220px; }

  /* Features: stack vertically, remove alternating */
  .feature {
    grid-template-columns: 1fr;
    gap: 32px;
    padding: 48px 0;
    text-align: center;
  }

  .feature--reverse .feature__content { order: 0; }
  .feature--reverse .feature__visual  { order: 0; }

  .feature__visual { justify-content: center; }

  .feature__iphone { width: 200px; }

  .feature__desc { max-width: 100%; }

  /* Footer: stack vertically */
  .footer__container {
    flex-direction: column;
    gap: 16px;
    text-align: center;
  }
}
```

- [ ] **Step 2: Open in browser, resize window to 375px, and verify**

Expected:
- Hero: iPhone screenshot on top (centered), then headline, subline, button below — all centered
- Feature 1: content above, phone below
- Feature 2: content above, phone below (no longer reversed)
- Feature 3: content above, phone below
- Footer: copyright above, links below — both centered

- [ ] **Step 3: Commit**

```bash
cd /Users/deniz.ilkaya/Websites/StepTeddy
git add assets/css/styles.css
git commit -m "style: responsive breakpoints for mobile"
```

---

### Task 8: privacy.html

**Files:**
- Create: `privacy.html`
- Modify: `assets/css/styles.css`

- [ ] **Step 1: Create privacy.html**

Create `privacy.html`:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Privacy Policy — StepTeddy</title>
  <link rel="icon" type="image/png" href="assets/images/app-icon.png">
  <link rel="stylesheet" href="assets/css/styles.css">
</head>
<body>

  <nav class="nav" id="nav">
    <div class="container nav__container">
      <a href="index.html" class="nav__brand">
        <img src="assets/images/app-icon.png" alt="StepTeddy" class="nav__icon">
        <span class="nav__name">StepTeddy</span>
      </a>
      <a href="index.html#download" class="btn btn--primary btn--sm">Download</a>
    </div>
  </nav>

  <main class="legal">
    <div class="container legal__container">
      <h1>Privacy Policy</h1>
      <p class="legal__date">Last updated: June 2026</p>

      <p>This Privacy Policy describes how StepTeddy collects, uses, and shares information about you when you use our app.</p>

      <h2>Information We Collect</h2>
      <p>StepTeddy collects step count and activity data from your device's motion sensors and Apple Health (with your permission). This data is stored locally on your device and is not transmitted to our servers.</p>

      <h2>How We Use Your Information</h2>
      <p>We use your step data solely to provide the core functionality of the app: tracking your daily steps, building streaks, and awarding badges.</p>

      <h2>Data Sharing</h2>
      <p>We do not sell, trade, or share your personal data with third parties.</p>

      <h2>Data Retention</h2>
      <p>All data is stored locally on your device. Uninstalling the app removes all associated data.</p>

      <h2>Contact</h2>
      <p>If you have questions about this Privacy Policy, please contact us at: <a href="mailto:hello@stepteddy.app">hello@stepteddy.app</a></p>
    </div>
  </main>

  <footer class="footer">
    <div class="container footer__container">
      <p class="footer__copy">© 2026 StepTeddy</p>
      <nav class="footer__links">
        <a href="privacy.html">Privacy Policy</a>
        <a href="terms.html">Terms &amp; Conditions</a>
      </nav>
    </div>
  </footer>

  <script src="assets/js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Add legal page CSS to styles.css**

Append to `assets/css/styles.css`:
```css
/* ── Legal pages (privacy, terms) ───────────────────── */
.legal {
  padding: 60px 0 100px;
}

.legal__container {
  max-width: 720px;
}

.legal h1 {
  font-size: 40px;
  font-weight: 800;
  letter-spacing: -1px;
  margin-bottom: 8px;
}

.legal__date {
  color: var(--text-secondary);
  font-size: 15px;
  margin-bottom: 40px;
}

.legal h2 {
  font-size: 22px;
  font-weight: 700;
  margin-top: 40px;
  margin-bottom: 12px;
}

.legal p {
  color: var(--text-secondary);
  margin-bottom: 16px;
}

.legal a {
  color: var(--primary);
  text-decoration: underline;
}
```

- [ ] **Step 3: Open privacy.html in browser and verify**

Expected: Same nav and footer as index.html. Centered single-column text, max 720px wide. "Privacy Policy" heading, light-gray date, sections with h2 and paragraph text.

- [ ] **Step 4: Commit**

```bash
cd /Users/deniz.ilkaya/Websites/StepTeddy
git add privacy.html assets/css/styles.css
git commit -m "feat: add privacy policy page"
```

---

### Task 9: terms.html

**Files:**
- Create: `terms.html`

- [ ] **Step 1: Create terms.html**

Create `terms.html`:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Terms &amp; Conditions — StepTeddy</title>
  <link rel="icon" type="image/png" href="assets/images/app-icon.png">
  <link rel="stylesheet" href="assets/css/styles.css">
</head>
<body>

  <nav class="nav" id="nav">
    <div class="container nav__container">
      <a href="index.html" class="nav__brand">
        <img src="assets/images/app-icon.png" alt="StepTeddy" class="nav__icon">
        <span class="nav__name">StepTeddy</span>
      </a>
      <a href="index.html#download" class="btn btn--primary btn--sm">Download</a>
    </div>
  </nav>

  <main class="legal">
    <div class="container legal__container">
      <h1>Terms &amp; Conditions</h1>
      <p class="legal__date">Last updated: June 2026</p>

      <p>By downloading and using StepTeddy, you agree to these Terms &amp; Conditions. Please read them carefully.</p>

      <h2>Use of the App</h2>
      <p>StepTeddy is provided for personal, non-commercial use. You agree not to misuse the app or attempt to access it in unauthorized ways.</p>

      <h2>Health Disclaimer</h2>
      <p>StepTeddy is not a medical device. Step data is provided for informational and motivational purposes only and should not be used as a substitute for professional medical advice.</p>

      <h2>Intellectual Property</h2>
      <p>All content, graphics, and software within StepTeddy are the property of StepTeddy and protected by applicable copyright and trademark laws.</p>

      <h2>Limitation of Liability</h2>
      <p>StepTeddy is provided "as is" without warranties of any kind. We are not liable for any damages arising from your use of the app.</p>

      <h2>Changes to Terms</h2>
      <p>We reserve the right to update these terms at any time. Continued use of the app after changes constitutes acceptance of the new terms.</p>

      <h2>Contact</h2>
      <p>For questions about these terms, contact us at: <a href="mailto:hello@stepteddy.app">hello@stepteddy.app</a></p>
    </div>
  </main>

  <footer class="footer">
    <div class="container footer__container">
      <p class="footer__copy">© 2026 StepTeddy</p>
      <nav class="footer__links">
        <a href="privacy.html">Privacy Policy</a>
        <a href="terms.html">Terms &amp; Conditions</a>
      </nav>
    </div>
  </footer>

  <script src="assets/js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Open terms.html in browser and verify**

Expected: Identical layout to privacy.html with "Terms & Conditions" as the heading and the terms content.

- [ ] **Step 3: Verify all internal links**

Check in the browser:
- `index.html` footer → "Privacy Policy" → opens `privacy.html` ✓
- `index.html` footer → "Terms & Conditions" → opens `terms.html` ✓
- `privacy.html` nav logo → returns to `index.html` ✓
- `terms.html` nav "Download" → goes to `index.html#download` ✓
- `index.html` nav "Download" → scrolls to CTA section ✓

- [ ] **Step 4: Commit**

```bash
cd /Users/deniz.ilkaya/Websites/StepTeddy
git add terms.html
git commit -m "feat: add terms and conditions page"
```

---

### Task 10: GitHub Pages setup

**Files:** None — GitHub Pages serves from repo root by default.

- [ ] **Step 1: Create a GitHub repo**

On github.com, create a new public repository. Suggested name: `stepteddy-website`. Leave it empty (no README).

- [ ] **Step 2: Add remote and push**

```bash
cd /Users/deniz.ilkaya/Websites/StepTeddy
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/stepteddy-website.git
git branch -M main
git push -u origin main
```

Replace `YOUR_GITHUB_USERNAME` with your actual GitHub username.

- [ ] **Step 3: Enable GitHub Pages**

In the GitHub repo: Settings → Pages → Source: `Deploy from a branch` → Branch: `main` → Folder: `/ (root)` → Save.

- [ ] **Step 4: Verify deployment**

Wait ~2 minutes, then visit:
`https://YOUR_GITHUB_USERNAME.github.io/stepteddy-website/`

Expected: Full landing page loads with all images, styles, and navigation working.

**Note:** Replace the `PLACEHOLDER` in the App Store link in `index.html` and `terms.html` once the app is live.
Also replace `hello@stepteddy.app` in `privacy.html` and `terms.html` with your actual contact email.
