# Day 20 — AI Face Puzzle Game 🧩

## Project Overview

Built a fully interactive face puzzle game as a **single self-contained HTML file** using vanilla JavaScript and the browser's native WebRTC camera API. No frameworks, no external dependencies beyond Google Fonts.

---

## What I Built

**FacePuzzle — "Shatter Yourself"**

A browser-based puzzle game where you:
1. Capture your face via webcam
2. Choose a difficulty (3×3, 4×4, or 5×5 grid)
3. Drag and drop scrambled pieces back into the correct order
4. Race against a live timer with move tracking

---

## Features Implemented

| Feature | Details |
|---|---|
| 📷 Camera Access | `getUserMedia()` with front-facing camera preference, graceful denial fallback |
| 🧩 Puzzle Generation | Image sliced into N×N equal tiles, Fisher-Yates shuffle for guaranteed solvability |
| 🖱️ Drag & Drop | Mouse + touch support, ghost image follows cursor, swap-on-drop mechanic |
| ✅ Correct Piece Highlight | Green border on correctly placed pieces in real time |
| ⏱️ Timer | `requestAnimationFrame`-based live timer in `mm:ss.d` format |
| 🔢 Move Counter | Increments on every valid piece swap |
| 📊 Progress Bar | Fills as pieces are placed correctly |
| 🏆 Win Detection | Auto-detects when all pieces match, stops timer immediately |
| 💾 Leaderboard | Top 20 scores persisted to `localStorage`, top 5 shown in UI |
| 👁️ Peek Button | Flashes piece hints with a 5-second time penalty |
| 🎉 Confetti | Canvas-based particle burst on puzzle completion |
| 📱 Responsive | Works on desktop and mobile, board scales to viewport width |

---

## Difficulties Chosen

- **3×3** — Easy, 9 pieces, great for a first run
- **4×4** — Medium, 16 pieces, good challenge
- **5×5** — Hard, 25 pieces, serious scramble

---

## Tech Stack

- **HTML5** — Single file, no build step
- **CSS3** — CSS custom properties, CSS Grid, `backdrop-filter`, gradient text
- **Vanilla JavaScript** — No libraries
- **Web APIs used:**
  - `navigator.mediaDevices.getUserMedia` — camera stream
  - `HTMLCanvasElement` — image capture and piece slicing
  - `requestAnimationFrame` — smooth timer loop
  - `localStorage` — leaderboard persistence
  - `document.elementFromPoint` — drop target detection for touch

---

## Key Bugs Fixed & Lessons Learned

### Bug 1 — Blank puzzle pieces
`cloneNode(true)` on a `<canvas>` element copies the DOM node but **not** the pixel data. All pieces rendered as blank grey squares.

**Fix:** Convert each piece canvas to a PNG data URL via `toDataURL()` and render with an `<img>` tag instead. Images carry their pixel data correctly.

```js
// Wrong
cell.appendChild(pieceCanvas.cloneNode(true)); // blank!

// Right
const img = document.createElement('img');
img.src = pieceCanvas.toDataURL();
cell.appendChild(img);
```

### Bug 2 — Stale drag closures
Drag event handlers were closing over old `piece` objects captured at render time. After a swap and re-render, the handlers still referenced the original piece positions.

**Fix:** Store all state in a global `G.order[]` array (cell index → piece ID). Every drag event reads from `G.order` at call time, never from a closure.

### Bug 3 — Touch drop detection failing
`e.target` during `touchend` always returns the element where the touch *started*, not where it ended — unlike mouse events.

**Fix:** Use `document.elementFromPoint(e.changedTouches[0].clientX, e.changedTouches[0].clientY)` to find the element under the finger on release.

### Bug 4 — Timer drift with setInterval
`setInterval` accumulates drift over time, making the displayed time inaccurate.

**Fix:** Switched to `requestAnimationFrame` with a `performance.now()` baseline — the timer always reflects wall-clock elapsed time, not accumulated intervals.

---

## File Structure

```
Day20/
├── day20.md          ← this file
└── face-puzzle-game.html  ← complete single-file application
```

---

## How to Run

1. Open `face-puzzle-game.html` in Chrome, Firefox, or Safari
2. Must be served over **HTTPS or localhost** for camera access
3. Allow webcam permission when prompted
4. Snap your photo, pick a difficulty, and solve!

> Tip: Use `npx serve .` or VS Code Live Server to run locally if opening the file directly doesn't allow camera access.

---

## Screenshots

> *(Add your screenshots here after playing the game)*

| Screen | Description |
|---|---|
| `screenshot-camera.png` | Live webcam view with face-oval guide |
| `screenshot-difficulty.png` | Photo preview + difficulty picker |
| `screenshot-puzzle.png` | Active puzzle with timer and stats bar |
| `screenshot-win.png` | Win overlay with results and leaderboard |

---

## What I Learned

- **`cloneNode` does not clone canvas pixel data** — always use `toDataURL()` or `drawImage()` to transfer canvas content
- **Touch events need `elementFromPoint`** for accurate drop targets — `e.target` is unreliable on `touchend`
- **`requestAnimationFrame` > `setInterval`** for any time-sensitive UI — no drift, pauses when tab is hidden
- **Single source of truth matters** — keeping all puzzle state in one `G.order[]` array eliminated entire classes of sync bugs between DOM and data
- **Fisher-Yates shuffle** is the correct algorithm for an unbiased random permutation — simple loop with random index is biased
- **CSS `backdrop-filter: blur()`** creates polished overlay effects with minimal code
- Prompting Claude with precise technical constraints (single file, no frameworks, specific APIs) produces much more usable output than vague requests