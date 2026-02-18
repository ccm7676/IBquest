# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Physics Match** is a single-file, browser-based educational game for IB Physics students. It helps students master physics formulas through interactive equation matching.

- **No build process** — open `index.html` directly in any modern browser
- **No package manager, no npm, no bundler**
- All external dependencies (KaTeX for LaTeX rendering) are loaded via CDN

## Architecture

The entire application lives in `index.html` — embedded CSS, JavaScript, and HTML in one file.

**Key JavaScript globals:**
- `GS` — central Game State object (score, lives, level, streak, mode, timer, question pool, missed questions)
- `EQ` — array of 63 physics equations, each with: LaTeX string, symbol definitions, scenario examples, IB topic tag, and SL/HL flag

**Three game modes:**
1. **Symbol Match** — identify what a symbol represents
2. **Equation Match** — match descriptions to equations
3. **Scenario Match** — multi-select which equations apply to a scenario

**Screen system:** Full-screen overlay divs toggled via CSS classes — start screen, game screen, game-over screen.

**Progression:** 10 correct answers → level up. Streak multiplier: 1× base, 2× at 3 streak, 5× at 6 streak, 10× at 10 streak. Time-based scoring (points decrease as timer depletes). 3 lives.

**Storage:** `localStorage` for high scores per mode.

**Audio:** Web Audio API with synthesized sound effects — no external audio files.

**Canvas:** Two canvas elements — dot-grid background texture and confetti particle system.

## Design System

`design-guidelines.md` is the authoritative design reference. Consult it before making visual changes. It covers:
- CSS custom properties (color variables, spacing, typography)
- Z-index layers (0–400)
- Component specs (cards, buttons, badges)
- Animation timings and easing
- Canvas particle/confetti specs
- Responsive breakpoints: 520px, 600px

## Content Structure

Each entry in the `EQ` array has:
```js
{
  latex: "...",          // KaTeX-renderable string
  symbols: {...},        // symbol → description map
  scenarios: [...],      // real-world example strings
  topic: "A.1",          // IB topic identifier
  hl: false              // true if Higher Level only
}
```

Topics span IB curriculum sections A.1 through E.3, covering mechanics, thermal physics, waves, fields, quantum, and nuclear physics.
