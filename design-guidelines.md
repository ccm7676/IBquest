# Physics Match — Design Guidelines

Reference document for replicating the Physics Match visual system in future games.

---

## 1. Color System

### CSS Custom Properties

```css
:root {
  --bg:       #111111;   /* Page background */
  --surface:  #1a1a1a;   /* Card/panel backgrounds */
  --border:   #2e2e2e;   /* Primary borders */
  --border2:  #222222;   /* Secondary (darker) borders */
  --text:     #ebebeb;   /* Primary text */
  --text2:    #888888;   /* Secondary text (subtitles, metadata) */
  --text3:    #555555;   /* Tertiary text (labels, hints) */
  --accent:   #B0ADFF;   /* Interactive highlight (soft lavender) */
  --green:    #4caf6e;   /* Correct / success */
  --red:      #e05252;   /* Wrong / error */
  --yellow:   #c9922a;   /* Achievement / streak */
  --orange:   #c97a3a;   /* Fire streak (6+ combo) */
  --purple:   #9b9b9b;   /* Progress bar fill */
}
```

### Semantic Usage

| Color | Where Used |
|-------|-----------|
| `--bg` | Page body, stat card insets, missed-item backgrounds |
| `--surface` | All cards, panels, HUD bar, option buttons |
| `--border` | Default borders on cards, inputs, chips, tags |
| `--border2` | Subtle inner borders (stat cards, option letter boxes) |
| `--text` | Headings, option text, primary content |
| `--text2` | Subtitles, secondary labels, inactive chips |
| `--text3` | Micro-labels (HUD, filters, stat captions), question numbers |
| `--accent` | Selected states, hover highlights, primary buttons, wordmark highlight, score display, high score values |
| `--green` | Correct answer borders/text, positive feedback, timer bar (>50%) |
| `--red` | Wrong answer borders/text, negative feedback, game-over title |
| `--yellow` | Streak badge, level-up text, new record text, timer bar (25-50%) |
| `--orange` | Fire streak badge (6+ streak) |

### Opacity Conventions

- **Selected/active backgrounds**: 12% opacity of accent — `rgba(176,173,255,.12)`
- **Hover backgrounds**: Slightly lighter surface — `#1e1e2e` (accent-tinted) or `#202020` (neutral)
- **Correct answer bg**: `rgba(76,175,110,.1)`
- **Wrong answer bg**: `rgba(224,82,82,.08)`
- **Tag backgrounds**: 6% opacity — `rgba(176,173,255,.06)`
- **Tag borders**: 35% opacity — `rgba(176,173,255,.35)`
- **Background dots**: `rgba(255,255,255,0.05)`
- **Flash overlays**: green `rgba(63,185,80,.08)`, red `rgba(248,81,73,.1)`

### Hardcoded Colors

| Value | Usage |
|-------|-------|
| `#0c0c18` | Dark text on accent-colored buttons |
| `#202020` | Neutral hover background |
| `#1e1e2e` | Accent-tinted hover/selected background |

### Confetti Palette

```js
['#58a6ff', '#bc8cff', '#3fb950', '#d29922', '#f85149']
// blue,     purple,    green,     yellow,    red
```

---

## 2. Typography

### Font Stack

```css
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
```

Base size: `16px` on `<html>`.

### Size Scale

| Size | Usage |
|------|-------|
| `clamp(2.6rem, 8vw, 4rem)` | App wordmark |
| `clamp(3rem, 10vw, 6rem)` | Level-up overlay text |
| `clamp(2rem, 7vw, 3.5rem)` | Combo popup |
| `clamp(1.1rem, 3vw, 1.6rem)` | Equation display |
| `2rem` | Game-over title |
| `1.6rem` | Stat values |
| `1.5rem` | High score card values |
| `1.3rem` | Score pop (floating) |
| `1.2rem` | HUD values, hearts |
| `1.05rem` | Primary button, scenario text |
| `.95rem` | Mode card title |
| `.9rem` | Option buttons, submit button |
| `.88rem` | Feedback message, ghost button, symbol question |
| `.85rem` | Game-over subtitle |
| `.82rem` | Streak badge |
| `.8rem` | Missed-item text, scenario hint |
| `.75rem` | New record banner |
| `.74rem` | Chips |
| `.72rem` | Question prompt, option letter |
| `.68rem` | Filter label, tags, question number, HS mode label, missed label |
| `.65rem` | Stat labels, badges, mi-labels |
| `.6rem` | HUD labels |

### Weight Scale

| Weight | Usage |
|--------|-------|
| `400` | Body text, default |
| `600` | Section labels, mode titles, feedback messages, missed-item names |
| `700` | Buttons, HUD values, streak badge, HS values |
| `800` | Wordmark, game-over title, stat values, combo text |
| `900` | Level-up text, combo popup |

### Letter Spacing

| Value | Usage |
|-------|-------|
| `-1px` | Wordmark (tight) |
| `.03em` | Feedback messages |
| `.06em` | Tags, submit/ghost buttons |
| `.08em` | Badges, mi-labels |
| `.1em` | Filter labels, HUD labels, stat labels, HS mode labels, missed labels, new record |
| `.12em` | Primary button |

### Text Transform

`text-transform: uppercase` is applied to: buttons, filter labels, HUD labels, stat labels, badges, chips (implicitly via label styling), tags, new-record banner, mi-labels.

---

## 3. Spacing & Layout

### Common Padding Values

| Padding | Components |
|---------|-----------|
| `36px 32px` | Game-over card |
| `22px 22px 18px` | Question card |
| `16px 18px` | Mode card |
| `16px 0` | Primary button (full-width, centered text) |
| `14px 18px` | Filter box |
| `14px 16px` | Option buttons |
| `11px 36px` | Submit button |
| `11px 28px` | Ghost button |
| `10px 18px` | High score card |
| `10px 14px` | Missed items |
| `9px 22px` | Feedback popup |
| `5px 12px` | Chips |
| `3px 12px` | Streak badge |
| `3px 10px` | Tags |
| `2px 9px` | Badge |
| `2px 6px` | Mi-label |
| `20px` | Screen padding (all sides) |

### Gap Values

| Gap | Components |
|-----|-----------|
| `20px` | Start screen vertical flow |
| `14px` | Game body column, game HUD |
| `12px` | HS row, mode grid, chips row (between groups) |
| `10px` | Stats grid, options grid, button row, option inner (letter + body) |
| `8px` | Q-meta tags, missed-row, options grid (mobile) |
| `6px` | Chips, game-top |
| `5px` | Lives hearts |

### Max-Width Constraints

| Width | Component |
|-------|-----------|
| `820px` | Mode grid |
| `800px` | Game body |
| `700px` | Filter box |
| `560px` | Game-over card |
| `340px` | Primary button (`min(340px, 100%)`) |
| `220px` | Mode card (max) |
| `150px` | Mode card (min) |
| `130px` | HS card (min) |

### Layout Systems

**Flexbox** (most layouts):
- Screens: `flex-direction: column; align-items: center; justify-content: center`
- HUD: `flex-wrap: wrap; align-items: center`
- Chip/tag rows: `flex-wrap: wrap`
- Options: `align-items: flex-start` (letter + body)

**CSS Grid** (structured grids):
- Options: `grid-template-columns: 1fr 1fr` (collapses to `1fr` at 520px)
- Stats: `grid-template-columns: 1fr 1fr`

### Z-Index Layers

| Z-Index | Element |
|---------|---------|
| `0` | Background canvas (`#bg`) |
| `10` | Screens |
| `20` | Game HUD (sticky top) |
| `100` | Flash overlay |
| `140` | Confetti canvas |
| `150` | Level-up overlay |
| `200` | Combo popup |
| `250` | Feedback messages |
| `300` | Score pop |

---

## 4. Borders & Radius

### Border Weights

| Weight | Usage |
|--------|-------|
| `1px solid` | Default for cards, options, chips, tags, badges, filter box, HS cards |
| `2px solid` | Mode cards, symbol highlight underline |
| `none` | Primary button, submit button |

### Border Radius

| Radius | Usage |
|--------|-------|
| `4px` | Cards (question, mode, HS, filter box, game-over), option buttons, missed items |
| `3px` | Buttons, chips, tags, badges, streak badge, stat cards, time track, feedback |
| `2px` | Mi-labels, time-fill inner, xp-track |
| `1px` | XP track |

**Rule of thumb**: Outer containers get `4px`, inner elements and small pills get `3px`.

---

## 5. Components

### Wordmark

```css
.wordmark {
  font-size: clamp(2.6rem, 8vw, 4rem);
  font-weight: 800;
  letter-spacing: -1px;
  color: var(--text);
}
.wordmark span { color: var(--accent); }
```

The second word is wrapped in `<span>` and rendered in accent color.

### Mode Card

- Surface background, `2px` border, `4px` radius
- `flex: 1` in a row, constrained `150–220px`
- Selected: accent border + `#1e1e2e` background
- Hover: `--text3` border + `#202020` background
- Contains only `.mode-title` (no icons, no descriptions)

### Chip (Toggle Filter)

- Transparent background by default, `1px` border
- Active (`.on`): accent text/border + 12% accent background
- Hover: text and border lighten to `--text2` / `--text`
- Preset chips ("All Topics", "SL Only") and individual topic chips

### Primary Button

- Full accent background, dark text (`#0c0c18`)
- `width: min(340px, 100%)`, tall padding (`16px 0`)
- Hover: slight opacity decrease (`.92`) + accent glow shadow (`0 0 20px`)
- Active: `scale(.97)`

### Ghost Button

- Transparent background, `1px` border
- Hover: border/text lighten
- Used for secondary actions (e.g., "Home" on game-over)

### Option Button

- Surface background, `1px` border, `4px` radius
- Flexbox: letter badge (22px square, `--border2` bg) + body content
- Hover: accent border, `#1e1e2e` bg, lift `-1px`
- Correct: green border/text, green-tinted bg
- Wrong: red border/text, red-tinted bg
- Picked (scenario multi-select): accent border, accent-tinted bg
- 2-column grid, collapses to 1 column at 520px

### High Score Card

- Surface bg, `1px` border, `4px` radius
- Mode name: `.68rem`, `--text3`, uppercase
- Score value: `1.5rem`, `700` weight, accent color
- `min-width: 130px`, flex row with wrapping

### Tag

- Small pill: `3px` radius, `.68rem` text
- Mode tag: accent color with semi-transparent accent border/bg
- Topic tag: `--text2` with `--border`

### Streak Badge

- `3px` radius, `--yellow` text/border
- Fire state (streak >= 6): `--orange` with pulsing glow animation
- Shows multiplier text: "x2", "x5", "x10"

### Progress Bars

- **Timer bar**: `4px` height, green > yellow > red based on time remaining
- **XP bar**: `2px` height, `--purple` fill, below timer bar

### Feedback Message

- Fixed position, `top: 70px`, centered horizontally
- Slides in from `-10px` offset
- Good: green border/text, green-tinted bg
- Bad: red border/text, red-tinted bg
- Auto-dismisses after ~1.2s

### Score Pop

- Floating number at screen center
- Animates up 70px while scaling to 1.2x and fading out
- Duration: 1s

### Game-Over Card

- `560px` max-width, centered
- Title: red default, yellow for high accuracy (80%+)
- 2x2 stats grid with dark inset backgrounds
- Missed questions section with "You chose" vs "Correct" rows
- New record banner: yellow, blinking animation

---

## 6. Interactive States

### Hover

| Component | Border | Background | Other |
|-----------|--------|------------|-------|
| Primary button | — | `opacity: .92` | `box-shadow: 0 0 20px rgba(176,173,255,.3)` |
| Ghost button | `--text2` | — | — |
| Option | `--accent` | `#1e1e2e` | `translateY(-1px)` |
| Mode card | `--text3` | `#202020` | — |
| Chip | `--text2` border | — | text → `--text` |
| Submit button | — | `opacity: .85` | — |

### Active

| Component | Effect |
|-----------|--------|
| Primary button | `scale(.97)` |
| Option | `transform: none` (cancels hover lift) |

### Selected

| Component | Border | Background | Text |
|-----------|--------|------------|------|
| Mode card | `--accent` | `#1e1e2e` | — |
| Chip (`.on`) | `--accent` | `rgba(176,173,255,.12)` | `--accent` |
| Option (`.picked`) | `--accent` | `rgba(176,173,255,.1)` | — |

### Answer Feedback

| State | Border | Background | Text |
|-------|--------|------------|------|
| Correct | `--green !important` | `rgba(76,175,110,.1) !important` | `--green` |
| Wrong | `--red !important` | `rgba(224,82,82,.08) !important` | `--red` |

### Disabled

Options after answer: `cursor: default`, no hover effects.

---

## 7. Animation & Motion

### Transition Defaults

| Duration | Easing | Properties |
|----------|--------|-----------|
| `.1s` | default | `transform` (button active, option lift) |
| `.12s` | default | `border-color`, `background` (options) |
| `.15s` | default | `border-color`, `background`, `opacity`, `color` (cards, chips, buttons) |
| `.25s` | default | `all` (feedback), `opacity` (screens, flash) |
| `.3s` | default | `opacity` (hearts, level-up overlay) |
| `.4s` | default | `background` (timer bar color), `width` (XP bar) |

### Keyframe Animations

**Fire Pulse** (streak badge glow):
```css
@keyframes fpulse {
  from { box-shadow: 0 0 4px rgba(219,109,40,.3); }
  to   { box-shadow: 0 0 14px rgba(219,109,40,.7); }
}
/* .6s ease-in-out infinite alternate */
```

**Score Float** (score pop):
```css
@keyframes sfloat {
  0%   { opacity: 1; transform: translateY(0) scale(1); }
  100% { opacity: 0; transform: translateY(-70px) scale(1.2); }
}
/* 1s ease-out forwards */
```

**Level-Up Spin**:
```css
@keyframes lvlspin {
  0%   { transform: scale(0) rotate(-8deg); }
  60%  { transform: scale(1.1); }
  100% { transform: scale(1); }
}
/* .5s ease-out */
```

**Screen Shake** (wrong answer):
```css
@keyframes shake {
  0%,100% { transform: translateX(0); }
  15%     { transform: translateX(-9px) rotate(-.4deg); }
  35%     { transform: translateX(9px) rotate(.4deg); }
  55%     { transform: translateX(-6px); }
  75%     { transform: translateX(6px); }
  90%     { transform: translateX(-3px); }
}
/* .45s ease */
```

**Blink** (new record):
```css
@keyframes blink {
  0%,100% { opacity: 1 }
  50%     { opacity: .4 }
}
/* 1s infinite */
```

### Easing Reference

| Easing | Usage |
|--------|-------|
| `linear` | Timer bar width countdown |
| `ease` | Shake animation |
| `ease-out` | Score float, level-up spin |
| `ease-in-out` | Fire pulse |
| `cubic-bezier(.34, 1.56, .64, 1)` | Combo popup (bouncy overshoot) |

### Motion Principles

- Transitions are fast (`.1s–.25s`) — snappy, not sluggish
- Feedback animations are slightly longer (`.45s–1s`) for visibility
- Celebratory effects (confetti, level-up) use overshoot/bounce easing
- Error feedback uses shake with dampening amplitude
- All overlays use `pointer-events: none` so they don't block interaction

---

## 8. Canvas Effects

### Background Dot Grid

```
Canvas: #bg, z-index: 0, pointer-events: none, fixed position
Grid spacing: 40px
Dot radius: 1px
Dot color: rgba(255,255,255,0.05)
Offset: starts at spacing/2 from edges
Redraws on window resize
```

### Confetti Particle System

```
Canvas: #confetti, z-index: 140, pointer-events: none, fixed position
Runs continuously via requestAnimationFrame

Particle properties:
  - Shape: filled rectangle (4-9px wide, 2-5px tall)
  - Colors: ['#58a6ff', '#bc8cff', '#3fb950', '#d29922', '#f85149']
  - Speed: 3-10 px/frame, random angle
  - Upward bias: -3 added to vy
  - Gravity: +0.25 per frame
  - Rotation: random start, ±0.075 rad/frame
  - Decay: 0.018-0.036 per frame (life: 1 → 0)
  - Alpha: tied to life value

Burst triggers:
  - Combo achievement (x2, x5, x10): 28 particles at screen center
  - Level-up: 55 particles at (center, 1/3 height)
  - New high score: 70 particles at (center, 1/4 height)
```

---

## 9. Audio Design

All sounds use the Web Audio API with no external files. AudioContext is created lazily on first use.

### Sound Specs

| Sound | Trigger | Waveform | Frequency | Duration | Max Gain |
|-------|---------|----------|-----------|----------|----------|
| `ok` | Correct answer | sine | 440 → 880 Hz | 300ms | 0.25 |
| `no` | Wrong / timeout | sawtooth | 280 → 140 Hz | 280ms | 0.18 |
| `lvl` | Level up | 4x sine chord | 523, 659, 784, 1047 Hz | 300ms each, staggered 100ms | 0.2 each |
| `str` | Streak milestone | triangle | 600 → 900 Hz | 200ms | 0.2 |
| `tick` | Timer ≤ 3s | sine | 700 Hz (fixed) | 50ms | 0.04 |

### Design Principles

- **Correct**: ascending pitch (rewarding)
- **Wrong**: descending pitch, harsher waveform (sawtooth)
- **Level-up**: major chord arpeggio (C5-E5-G5-C6)
- **Streak**: quick ascending chirp (triangle for softer tone)
- **Tick**: very quiet, minimal — background tension only
- All sounds use `linearRampToValueAtTime` for smooth gain fadeout
- Wrapped in `try-catch` for silent failure in unsupported browsers

---

## 10. Responsive Design

### Breakpoints

**520px** — Options grid collapses from 2 columns to 1:
```css
@media (max-width: 520px) {
  .options-grid { grid-template-columns: 1fr; }
}
```

**600px** — General mobile adaptations:
```css
@media (max-width: 600px) {
  .game-hud { gap: 10px; }
  .game-body { padding: 12px 14px 16px; gap: 10px; }
  .question-card { padding: 16px; }
  .options-grid { gap: 8px; }
  .opt { padding: 11px 12px; }
  .go-card { padding: 24px 18px; }
  .mode-grid { flex-direction: column; align-items: center; }
  .mode-card { max-width: 100%; }
}
```

### Responsive Patterns

- Font sizes use `clamp()` for fluid scaling (wordmark, equations, combo text, level-up)
- Primary button uses `width: min(340px, 100%)` for natural fit
- Mode grid switches from horizontal row to vertical stack at 600px
- All containers use `max-width` with `width: 100%` for natural responsiveness
- `flex-wrap: wrap` on HUD, chips, buttons, tags prevents overflow
- `overflow-x: auto` on equation displays allows horizontal scroll for long formulas

### Global Resets

```css
* { margin: 0; padding: 0; box-sizing: border-box; }
html, body { width: 100%; height: 100%; overflow: hidden; }
body { user-select: none; -webkit-user-select: none; }
```

---

## 11. General Principles

1. **Dark-first**: All backgrounds are near-black. Color comes only from accent and semantic states.
2. **Flat, not glossy**: No gradients, no blur, no glassmorphism. Surfaces are solid colors separated by subtle borders.
3. **Accent is selective**: `--accent` only appears on interactive/selected elements — never as large background fills (except buttons).
4. **Semantic color only**: Green = correct, red = wrong, yellow = achievement. Never decorative.
5. **Square-ish corners**: `3–4px` radius only. No pills, no circles (except heart emoji and canvas dots).
6. **Uppercase labels**: All micro-copy (HUD labels, stat captions, filter labels, tags) is uppercase with wide letter-spacing.
7. **Minimal decoration**: No icons, no emojis in UI (except hearts for lives). Content speaks for itself.
8. **Fast feedback**: Transitions under 250ms for interactions. Longer animations (500ms–1s) only for celebration/feedback overlays.
9. **Single-file architecture**: Everything in one HTML file — CSS in `<style>`, JS in `<script>`, no external assets except KaTeX CDN.
10. **Canvas for atmosphere**: Dot grid adds texture without CSS complexity. Confetti is celebratory, not constant.
