# 36Studio

A scroll-driven, animation-heavy landing page for a digital production studio, built with React, GSAP and Locomotive Scroll.

**Live demo:** https://36studio.kashyap-education2234.workers.dev/

## About

36Studio is a single-page front-end project that recreates the look and feel of an immersive agency website. It combines smooth inertial scrolling, canvas-based frame animations, a custom cursor and a light/dark theme switch to show how far a pure front-end stack can go without a backend.

The page is split into three full-height sections:

1. **Hero** – A bold studio intro with an oversized wordmark. Clicking the intro text toggles the site between light and dark themes, and clicking the wordmark reveals floating animated image sequences.
2. **What we do / Our service** – A short mission statement with a hover-reveal video, followed by a services paragraph with inline rounded images.
3. **Values** – Three expandable cards (Agile, Innovative, Cultured) that fill with colour on hover or touch, plus a closing note on social sustainability.

## Features

- **Smooth scrolling** with Locomotive Scroll, synced to GSAP ScrollTrigger through a scroller proxy.
- **Canvas frame animation:** a sequence of 1,000+ preloaded PNG frames is drawn to `<canvas>` elements and looped with a GSAP tween. Each canvas starts at a different frame offset, so the floating objects animate out of sync.
- **Parallax:** every canvas layer gets a random `data-scroll-speed`, giving depth while scrolling.
- **Theme toggle:** GSAP animates the background and text colour between white and black, along with the accent line elements.
- **Custom cursor:** a mix-blend-difference circle follows the mouse with easing and scales up over interactive text (desktop only).
- **Hover video reveal:** the video grows and fades in when the paragraph beside it is hovered.
- **Interactive cards:** a colour fill and blend-mode change on hover, with touch support for mobile.
- **Responsive layout:** Tailwind CSS utilities with separate mobile and desktop treatments for text, video and canvas sizing.

## Tech Stack

| Area | Tools |
| --- | --- |
| UI | React 19 |
| Build tool | Vite 7 |
| Styling | Tailwind CSS 4 (`@tailwindcss/vite`) |
| Animation | GSAP, `@gsap/react`, ScrollTrigger |
| Scrolling | Locomotive Scroll 4 |
| Linting | ESLint 9 with React Hooks and React Refresh plugins |
| Font | Satoshi (local `.otf`) |

## Project Structure

```
36Studio/
├── index.html
├── vite.config.js
├── eslint.config.js
├── package.json
└── src/
    ├── main.jsx               # App entry point
    ├── App.jsx                # Scroll setup, theme toggle, cursor, section layout
    ├── index.css              # Tailwind import, font-face, global styles
    ├── Fonts/                 # Satoshi font
    ├── video/                 # Section 2 motion video (mp4 and webm)
    └── components/
        ├── Canvas.jsx         # Frame-by-frame canvas animation component
        ├── canvasimages.js    # List of animation frame URLs
        ├── imageData.js       # Size, position and start frame for each canvas
        ├── Page1.jsx          # Hero section
        ├── Page2.jsx          # What we do / services section
        └── Page3.jsx          # Values cards and closing note
```

## Getting Started

### Prerequisites

- Node.js 18 or newer
- npm

### Installation

```bash
git clone https://github.com/KashyapDas/36Studio.git
cd 36Studio
npm install
```

### Run locally

```bash
npm run dev
```

Vite starts with `--host`, so the site is also reachable from other devices on your network (handy for testing on a phone).

### Other scripts

```bash
npm run build     # Production build into dist/
npm run preview   # Preview the production build locally
npm run lint      # Run ESLint
```

## How It Works

- `App.jsx` creates the Locomotive Scroll instance and registers it as a ScrollTrigger scroller proxy, so GSAP and the smooth scroller share one scroll position.
- `imageData.js` describes each animated canvas (start frame, size, position). `App.jsx` maps over it to render one `Canvas` per entry inside each section.
- `Canvas.jsx` preloads all frames once into a shared cache. A GSAP tween drives a frame counter, and `drawFrame` paints the matching image only when the frame changes.
- The theme and the canvas visibility are controlled from `App.jsx` through state and GSAP timelines.

## Notes

- The animation frames in `canvasimages.js` are loaded from remote URLs, so an internet connection is required for the canvas animation to work.
- This project is a learning and portfolio piece focused on front-end animation techniques. Branding, copy and imagery belong to their respective owners.

## Possible Improvements

- Host the animation frames locally or as a sprite sheet to remove the external dependency.
- Replace the hard-coded page index checks in `App.jsx` with a section config.
- Update the page title and favicon in `index.html` (still the Vite defaults).
- Add accessibility improvements such as alt text, keyboard-friendly theme toggle and `prefers-reduced-motion` support.

## Author

Built by [Kashyap Das](https://github.com/KashyapDas).
