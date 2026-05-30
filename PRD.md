# Product Requirement Document (PRD)

## Project: Sundown Studio — Landing Page Replica
**Status:** In Development (Refactoring Phase)  
**Author:** AI Pair Programmer / Antigravity  
**Date:** May 29, 2026  
**Version:** 1.0.0  

---

## 1. Executive Summary
The **Sundown Studio Landing Page Replica** is a high-fidelity, frontend-only recreation of the award-winning [Sundown Studio website](https://www.sundown-studio.com/). The primary purpose of this project is to showcase advanced UI/UX interactions, complex CSS animations, high-performance scroll physics, and smooth canvas/vector-like layouts using only standard web technologies (HTML5, CSS3, Vanilla ES6+ JavaScript, and GSAP).

This project serves as a showcase of premium web engineering techniques, emphasizing micro-interactions, responsive styling, and modern organic aesthetics (e.g., gooey lava-lamp effects, cursor-tracking previews).

---

## 2. Product Vision & Core Objectives
- **1:1 Visual Fidelity:** Replicate the brand identity, typography, layouts, colors, and asset placements of the original Sundown Studio landing page.
- **Buttery-Smooth Performance:** Maintain 60fps scrolling and animation cycles across modern desktop and mobile browsers.
- **Zero-Build Architecture:** Rely entirely on vanilla files (HTML, CSS, JS) without a build step (no Webpack, Vite, or npm compilation required for execution), maximizing direct browser accessibility.
- **Educational Showcase:** Document advanced animations (gooey morphs, smooth scroll, marquee loops, custom cursor trails) for portfolio review and development study.

---

## 3. User Experience & Design System

### 3.1 Typography
- **Primary Typeface:** *Neue Haas Grotesk Text Pro* (Regular, Medium, Bold) served locally via custom `@font-face` rules.
- **Backup Stack:** `sans-serif`, Arial.
- **Hierarchy:**
  - Loader Concept Words: `10vw`, Text-Transform: Uppercase.
  - Page 1 Hero Headline: `10vw` / `12vw` (highly responsive).
  - Section Titles: `1rem` + small orange circular bullet indicator.
  - Body Text: `1rem` to `1.2rem` with loose line-height (`1.3`–`1.5`) for premium editorial aesthetic.

### 3.2 Color Palette
- **Backgrounds:** 
  - Primary light background: White/Off-white `#EFEAE3`.
  - Secondary dark background: Deep Grey/Black `#0F0D0D`.
- **Primary Brand Color:** Bright Neon Orange (`#FE320A` / `#FE3F0A` for glowing elements).
- **Secondary Accents:** Soft Orange (`#FFE0D3`), Dark Grey (`#504A45` for inactive text).
- **Text:** Dark Charcoal (`#1C1B19`) on light backgrounds, Off-white (`#EFEAE3`) on dark backgrounds.

### 3.3 Visual Style Elements
- **Gooey Morphs (Lava-Lamp):** Organic shapes utilizing heavy CSS filters (`blur(25px)` / `blur(30px)`) combined with a high-contrast container or layered transparency to create fluid merge-and-split visual effects.
- **Smooth Deceleration Curves:** Avoid default step-based browser scroll physics; integrate custom physics-based scroll decay.

---

## 4. Functional Requirements & Feature Specifications

### F01: Preloader Screen (Intro Animation)
- **Description:** A cinematic intro overlay that loops through three core brand concepts before presenting the site.
- **Technical Specs:**
  - Fixed full-screen overlay with `#loader` (`z-index: 999`, `#000000` background).
  - Staggered animation cycle cycling through three headers: `ENVIRONMENTS` → `EXPERIENCES` → `CONTENT`.
  - Staggering achieved via CSS keyframe animations and `animation-delay` offsets (1s, 2s, 3s).
  - After 4 seconds, JavaScript changes the loader style (`top: -100%`) utilizing CSS transitions to slide the loader out of view.

### F02: Navigation & Full-Screen Mobile Menu
- **Description:** Clean desktop header navigation that collapses into a custom full-screen slide-down menu overlay on tablet/mobile screens.
- **Technical Specs:**
  - Nav logo fetches the Sundown Studio vector logo dynamically.
  - Desktop: Displays links for `Work`, `Studio`, and `Contact` with smooth hover states.
  - Mobile (<= 600px): Desktop links hide; a `#menu` button displays.
  - Clicking `#menu` toggles `#full-scr` (`top: 0` when open, `top: -100%` when closed) using smooth slide-down transitions.
  - The mobile menu overlay contains custom links and a pulsing background gooey blob.

### F03: Hero Section & Autoplay Video
- **Description:** High-impact hero screen containing tagline, main bold headline, background gooey visual effects, and a background loop video.
- **Technical Specs:**
  - Columns auto-wrap on mobile (headline moves to top, tagline to bottom).
  - HTML5 video tag configured with `autoplay`, `loop`, `muted`, and `playsinline` (crucial for iOS/Safari autoplay compliance).
  - Background gooey blob `#hero-shape` with three child divs morphing via CSS keyframe loops and high blur parameters, sitting behind the video layer (`z-index` stack).

### F04: Infinite Scrolling Marquee
- **Description:** Continuous, seamless, gap-free horizontal text loop displaying core offerings.
- **Technical Specs:**
  - Container `#move-text` set to `white-space: nowrap` and `overflow-x: hidden`.
  - Three duplicated `.con` text blocks loop horizontally.
  - Smooth looping uses CSS keyframes:
    ```css
    @keyframes move {
        from { transform: translateX(0); }
        to { transform: translateX(-100%); }
    }
    ```
  - Inter-word separator: `#gola` (a small orange circle bullet).

### F05: Project List with Cursor-Tracking Preview
- **Description:** A list of recent studio work. Hovering over a project name slides up a hover overlay and reveals a floating image card that tracks the mouse cursor dynamically.
- **Technical Specs:**
  - Row hover event triggers `#overlay` CSS transition to slide orange block from `top: -100%` to `0%`.
  - Mouse movement over the container `#elem-container` tracks coords `dets.x` and `dets.y`.
  - GSAP `gsap.to()` smoothly moves the absolute-positioned `#fixed-image` div to match the cursor coords with a `0.4s` lag duration and `power3.out` easing curve.
  - Entering each project row `.elem` extracts its custom `data-image` URL attribute and swaps the `#fixed-image` background image dynamically.

### F06: Interactive Services Tabs (Black Box Section)
- **Description:** A dark-themed container showcasing design services. Clicking tabs dynamically updates descriptive content and swaps the hero image.
- **Technical Specs:**
  - Tabs container (`#tabs`) contains clickable headers: `Design`, `Project`, and `Execution`.
  - Click event handlers swap active text styling (color, border-left accent).
  - The right-side image (`#page4-img`) is updated dynamically by reading the tab's `data-img` attribute.

### F07: Brand Partnerships Swiper Carousel
- **Description:** A smooth, touch-draggable carousel displaying logos of partner brands with short contextual paragraphs.
- **Technical Specs:**
  - Swiper.js integration.
  - Configuration: `slidesPerView: "auto"`, `spaceBetween: 50`, `freeMode: true` (no rigid snapping, smooth slide deceleration), and `grabCursor: true`.
  - Displays partner SVG logos: Nike, Converse, Arc'teryx, Hunter, MediaLink, and Afterpay.

### F08: Curtain-Reveal Footer
- **Description:** A cinematic footer that is slowly uncovered as the user scrolls to the bottom of the page.
- **Technical Specs:**
  - `#footer` is set to `position: fixed; bottom: 0; z-index: 9;`.
  - The main page wrapper `#main` has a relative position, background color, and `z-index: 10`.
  - An empty spacer section `#page5` is placed at the end of `#main`.
  - As `#main` scrolls up, the footer is revealed from underneath.
  - Background morphs in the footer use keyframed CSS blob shapes (`#shape1`, `#shape2`).

---

## 5. Technology Stack & Integration Details

| Layer | Technology | Details / Configuration |
|---|---|---|
| **Structure** | HTML5 | Semantic layout with `#main` section blocks, custom `data-*` attributes for dynamic content swapping. |
| **Styling** | CSS3 | Custom `@font-face` loaders, CSS custom properties (variables), transitions, keyframe animations, `@media` queries for responsive layout adjustments. |
| **Logic** | ES6+ JavaScript | Vanilla DOM manipulation, event listener attachments, dynamic attribute handling. |
| **Scroll Animation** | Lenis.js | Physics-based inertial scroll setup. Configured with: `duration: 1.3`, `easing: 1.001 - 2^(-10t)`, `smoothTouch: false` (to preserve native mobile scroll feel). |
| **Cursor Animation** | GSAP 3.13 | High-performance tweening library handles the trailing cursor effect for the hover image preview. |
| **Slider Engine** | Swiper 11 | Powering the horizontal drag-to-scroll clients section. |

---

## 6. Non-Functional & Performance Requirements

### 6.1 Performance & Rendering
- **Animation Smoothness:** Scroll interactions and gooey calculations must target `60fps` with no frame drops. Limit heavy filters on high-paint-area components where possible.
- **Asset Loading:** The hero video asset (~16MB) should load asynchronously and play in compliance with mobile hardware configurations. In future releases, video and WebP compression must be prioritized to keep page-load times under **2.5 seconds** on a 3G network connection.

### 6.2 Responsiveness & Adaptability
- **Breakpoints:**
  - Mobile: `<= 600px` (Adjusts grid column layout, triggers sticky slide overlay menu, scales down text headers).
  - Tablet: `601px - 1023px`.
  - Desktop / Ultrawide: `>= 1024px`.
- Touch-handling overrides: Lenis scroll easing disabled on touch interfaces to allow native OS-level scrolling.

### 6.3 Browser Compatibility
- Must function identically across all modern rendering engines: Chromium (Chrome, Edge, Opera), WebKit (Safari), and Gecko (Firefox).

---

## 7. Known Issues & Remediation Plan

The following issues were identified in the v1.0 code and are scheduled for correction in the next maintenance release:

1. **Responsive Menu Selector Bug:** 
   - *Current Code:* `document.querySelector("navimg")` in `studio.js` (line 166).
   - *Behavior:* Fails silently as there is no `<navimg>` element in the HTML document.
   - *Remediation:* Update selector to `document.querySelector("nav img")`.
2. **Back Button Selector Bug:**
   - *Current Code:* `document.querySelector("#fill-div1 button:last-child")` in `studio.js` (line 206).
   - *Behavior:* Throws a console error because the element in HTML is `#full-div1`, not `#fill-div1`.
   - *Remediation:* Update selector to `document.querySelector("#full-div1 button:last-child")` or correct target element IDs.
3. **Duplicate ID Violations:**
   - *Current Code:* Multiple elements in `index.html` share duplicate IDs (e.g., `#gola` in the marquee, `#overlay` and `#proj` in the project cards, `#gol` in section headers).
   - *Behavior:* Invalidates HTML5 markup compliance; can cause undefined behavior in browser query engines when querying by ID.
   - *Remediation:* Refactor duplicate IDs to reusable CSS class descriptors (e.g., `.gola`, `.proj-overlay`, `.proj-info`, `.bullet-point`).

---

## 8. Future Roadmap & Enhancement Backlog
- [ ] **Accessibility (a11y) Audit:** Add `aria-*` tags, keyboard navigation capabilities to service tabs and client sliders, and proper alt text on all icons.
- [ ] **Asset Optimization:** Compress hero video format (use WebM with MP4 fallback) and scale responsive WebP images via `srcset` tags.
- [ ] **State-Driven Tabs:** Refactor service tabs to load descriptions and metadata from a clean JSON config file rather than hardcoding long text directly into the DOM/JS functions.
- [ ] **Clean Code Refactoring:** Transition style definitions out of inline selectors and consolidate CSS files; clean up unused desktop/mobile duplicate elements (such as duplicate `#full-scr` structures).
