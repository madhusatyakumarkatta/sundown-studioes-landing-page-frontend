# ☀️ Sundown Studio — Landing Page Replica

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://html.spec.whatwg.org/)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://www.w3.org/Style/CSS/)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![GSAP](https://img.shields.io/badge/GSAP-88CE02?style=for-the-badge&logo=greensock&logoColor=white)](https://gsap.com/)
[![Lenis](https://img.shields.io/badge/Lenis-Smooth_Scroll-black?style=for-the-badge)](https://lenis.darkroom.engineering/)
[![Swiper](https://img.shields.io/badge/Swiper-6332F6?style=for-the-badge&logo=swiper&logoColor=white)](https://swiperjs.com/)

A pixel-perfect, highly interactive frontend replica of the award-winning **[Sundown Studio](https://www.sundown-studio.com/)** website. Built entirely with vanilla HTML, CSS, and JavaScript — no frameworks, no build tools — showcasing advanced animation techniques, custom typography, and premium UI interactions.

---

## 🎬 Preview

| Desktop | Mobile |
|---------|--------|
| Hero section with autoplay video, animated gooey blobs, and smooth-scroll navigation | Responsive layout with slide-down full-screen menu overlay and touch-enabled carousels |

---

## ✨ Features

### 🎞️ Preloader Animation
A cinematic intro sequence cycles through three brand concepts — **ENVIRONMENTS → EXPERIENCES → CONTENT** — using staggered CSS keyframe animations with gradient text clipping. The loader slides away after 4 seconds to reveal the main page.

### 🫧 Organic Gooey Blobs
Fluid, morphing background shapes powered by CSS `filter: blur()` and multi-layered `@keyframes` animations. Three independently animating circles overlap to create a realistic lava-lamp / liquid glow effect behind the hero video and inside the footer.

### 🖱️ Cursor-Tracking Project Preview
Hovering over the Featured Projects list triggers a floating image card that tracks the user's cursor using **GSAP's** `gsap.to()` with `power3.out` easing — producing a smooth, lagging trail effect. Each project row dynamically swaps the preview image via `data-image` attributes.

### 🔄 Infinite Scrolling Marquee
A pure CSS infinite horizontal text banner built from three duplicated text strips. Uses `translateX(-100%)` keyframes at constant speed for a seamless, gap-free loop across all screen widths.

### 📜 Smooth Inertial Scrolling
Integrated with **[Lenis](https://lenis.darkroom.engineering/)** for buttery-smooth, physics-based scroll behavior. Custom easing curve (`1.001 - 2^(-10t)`) provides natural deceleration, with separate tuning for mouse and touch input.

### 🎡 Touch-Enabled Client Carousel
A drag-and-swipe brand slider built with **[Swiper.js](https://swiperjs.com/)** in free-mode — no snap points, natural momentum scrolling. Showcases client partnerships with Nike, Converse, Arc'teryx, Hunter, MediaLink, and Afterpay.

### 🧭 Interactive Service Tabs
A dark rounded panel with clickable Design / Project / Execution tabs, paired with a large project image. Tabs use `data-img` attributes for dynamic image swapping.

### 🦶 Scroll-Reveal Footer
The footer is `position: fixed` at the bottom of the viewport. The main content sits above it at a higher `z-index`, creating a cinematic "lift the curtain" reveal effect as the user scrolls to the end. Animated orange blobs with `skew`, `rotate`, and `scale` transforms add visual depth.

### 📱 Fully Responsive
Optimized for mobile (≤ 600px) with:
- Slide-down menu overlay with animated gooey blob background
- Column-reversed hero layout (headline first, tagline below)
- Touch-optimized Swiper carousel (2 slides visible)
- Adjusted blob sizes, font scales, and spacing

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **HTML5** | Semantic structure with descriptive `data-*` attributes |
| **CSS3** | Custom `@font-face`, keyframe animations, flexbox/grid layouts, `filter: blur()` gooey effects, gradient text clipping, responsive media queries |
| **JavaScript (ES6+)** | Vanilla DOM manipulation, event-driven interactions, `requestAnimationFrame` loop |
| **GSAP 3.13** | High-performance cursor-following animation with eased interpolation |
| **GSAP ScrollTrigger** | Imported for scroll-based animations (available for future use) |
| **Lenis** | Smooth-scroll library with custom easing and touch/mouse multipliers |
| **Swiper 11** | Free-mode drag carousel for the client logo section |

---

## 📁 Project Structure

```
sundown-studioes-landing-page-frontend/
├── index.html                              # Main page — 5 sections + fixed footer
├── README.md
├── .gitattributes
│
└── assets/
    ├── css/
    │   └── style.css                       # All styles (1292 lines) — desktop + mobile
    │
    ├── js/
    │   └── studio.js                       # Lenis, GSAP, Swiper, menu toggle, loader
    │
    ├── fonts/
    │   ├── NHaasGroteskTXPro-55Rg.ttf      # Neue Haas Grotesk — Regular
    │   ├── NHaasGroteskTXPro-65Md.ttf      # Neue Haas Grotesk — Medium
    │   └── NHaasGroteskTXPro-75Bd.ttf      # Neue Haas Grotesk — Bold
    │
    ├── images/
    │   ├── icon.png                        # Favicon
    │   ├── image.webp                      # Team photo (About section)
    │   ├── page4-img.webp                  # Services section hero image
    │   ├── page4-1.webp, page4-2.webp,     # Tab-switchable service images
    │   │   page4-3.webp
    │   └── swipper*.svg                    # Client logos (Nike, Converse, Arc'teryx, etc.)
    │
    └── videos/
        └── video.mp4                       # Hero background video (~16 MB)
```

---

## 🏗️ Architecture

The page is structured as a **single-page layout** with five stacked sections wrapped in a `#main` container, plus a fixed footer revealed on scroll:

```
┌──────────────────────────────────────┐
│  #loader (fixed, z:999)              │  ← Intro animation, removed after 4s
├──────────────────────────────────────┤
│  #full-scr (fixed, z:99)            │  ← Menu overlay, toggled by JS
├──────────────────────────────────────┤
│  #main (relative, z:10)             │
│  ┌────────────────────────────────┐  │
│  │ #page1 — Hero + Nav + Video   │  │
│  │ #page2 — Marquee + About      │  │
│  │ #page3 — Featured Projects    │  │
│  │ #page4 — Services + Clients   │  │
│  │ #page5 — Scroll spacer        │  │
│  └────────────────────────────────┘  │
├──────────────────────────────────────┤
│  #footer (fixed, z:9, bottom:0)     │  ← Revealed as #main scrolls away
└──────────────────────────────────────┘
```

---

## 🚀 Getting Started

This is a zero-dependency vanilla project — no `npm install`, no build step.

### 1. Clone the repository

```bash
git clone https://github.com/madhusatyakumarkatta/sundown-studioes-landing-page-frontend.git
cd sundown-studioes-landing-page-frontend
```

### 2. Run locally

**Option A — VS Code Live Server (Recommended):**
Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension, right-click `index.html`, and select *Open with Live Server*.

**Option B — Python HTTP server:**
```bash
python -m http.server 8000
```
Then visit [`http://localhost:8000`](http://localhost:8000).

**Option C — Direct file open:**
Double-click `index.html` — works for basic browsing, but local fonts and videos may not load due to CORS restrictions.

> **Note:** A local server is recommended so that custom fonts (`NHaasGroteskTXPro`) and the hero video load correctly.

---

## 🎨 Animation Breakdown

| Animation | Technique | Location |
|---|---|---|
| Loader word cycle | `@keyframes load` with staggered `animation-delay` | `style.css:1279` |
| Hero gooey blobs | `@keyframes anime1/anime2` on blurred circles | `style.css:271–280` |
| Infinite marquee | `@keyframes move` with `translateX(-100%)` | `style.css:337–340` |
| About section glow | `@keyframes big-gola` on blurred gradient circle | `style.css:399–402` |
| Project row hover | CSS `#overlay` slides from `top:-100%` to `0%` | `style.css:451–463` |
| Cursor-following image | `gsap.to()` with `power3.out` easing | `studio.js:73–81` |
| Footer blob morphing | `@keyframes shapeAnime/shapeAnime2` with skew + rotate | `style.css:767–776` |
| Mobile menu gooey | `@keyframes gooey` with blur + skew pulsing | `style.css:923–932` |

---

## ⚠️ Known Issues

- **`responsiveMenu()` selector bug:** `document.querySelector("navimg")` (line 166 in `studio.js`) should be `"nav img"`. Currently fails silently — the logo opacity toggle doesn't work when opening/closing the mobile menu.
- **`backBtn` selector bug:** `document.querySelector("#fill-div1 ...")` (line 206) should be `"#full-div1 ..."`. Throws a console error on page load.
- **Duplicate `id` attributes:** Multiple elements share the same `id` (e.g., `#gola`, `#overlay`, `#proj`, `#gol`). While browsers tolerate this, it's invalid HTML and may cause unexpected behavior with `querySelector`.

---

## 🖌️ Credits

All design assets, typography, and branding concepts are replicated from the original **[Sundown Studio](https://www.sundown-studio.com/)** website. This project is created strictly for **educational and frontend practice purposes**.

**Typography:** [Neue Haas Grotesk Text Pro](https://www.linotype.com/1246918/neue-haas-grotesk-text-pro-family.html) by Max Miedinger / Linotype.

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
