# Day 34 — Become a Marketing Detective

## Overview
Built a single-file HTML/CSS/JS interactive game called **Marketing Detective**. Players accept a randomized fictional marketing case, investigate evidence pinned to a corkboard (campaign brief, budget, metrics, customer comments, social performance), uncover three supporting clues, and submit a verdict identifying the campaign's primary marketing mistake. The app then delivers a "Case Closed" verdict, an expert explanation, suggested improvements, and a cumulative Learning Report across replays.

- **File:** [`marketing-detective.html`](./marketing-detective.html)
- **Tech:** Vanilla HTML/CSS/JavaScript (no frameworks, no backend, no external assets — runs fully offline as a standalone file)
- **Theme:** Midnight Emerald (deep green corkboard with brass accents), with 3 additional selectable presets (Claude Orange, Crimson Noir, Blueprint Blue)
- **Cases:** 10 fully detailed fictional marketing mysteries spanning skincare, gaming, CPG, fitness, electronics, local retail, apparel, food delivery, insurance, and B2B SaaS

## User Flow Implemented
1. **Theme Selection** — pick a color preset before entering the agency
2. **Case Assignment** — a "scanning records" decrypt animation reveals a new randomized case file
3. **Investigation Board** — drag (or tap, for mobile) evidence cards from the Evidence Locker onto a textured corkboard; a progress tracker shows how many of the 5 evidence categories have been examined
4. **Clue Reveal** — once all evidence is pinned, 3 supporting clues animate onto the board
5. **Solve the Case** — choose the primary mistake from 4 multiple-choice options (1 correct + 3 distractors pulled from other cases)
6. **Case Closed** — a stamped verdict (Case Closed / Case Reopened) with the expert explanation and suggested improvements
7. **Learning Report** — running accuracy stats and a per-case results chart, with the option to take on a new randomized case or change the theme

## Key Learnings
- **Constraint-driven prompting works well for scoped apps.** Explicitly banning Tailwind, npm, backend, APIs, images, and external assets forced a genuinely portable single-file deliverable that opens directly from disk with zero setup.
- **Data modeling before UI.** Structuring each case as a consistent object (objective, audience, channels, budget, metrics, comments, social performance, primary mistake, 3 clues, explanation, improvements) made it possible to drive every screen — evidence cards, clue reveals, multiple-choice generation — from one array instead of hand-building each case's UI.
- **Auto-generating distractors from sibling cases** (rather than writing custom wrong answers per case) kept the dataset compact while still producing plausible, non-repetitive multiple-choice options on every replay.
- **Progressive disclosure sustains curiosity.** Gating the supporting clues behind "examine all evidence first" — instead of showing everything at once — turned a data-dashboard into something closer to an actual investigation.
- **Design restraint mattered more than extra animation.** A single signature moment (the corkboard + push-pin evidence board) carried the aesthetic; keeping buttons, type, and transitions simple and consistent avoided the app feeling like a generic AI dashboard.
- **Reliability over framework novelty.** Choosing vanilla JS over React-via-CDN removed any risk of CDN failures or Babel transpilation issues when the file is opened locally offline — a good reminder that "impressive tech" isn't the goal when "runs reliably everywhere" is the actual requirement.

## Screenshots
> Screenshots of the completed investigation (theme picker, corkboard investigation, case-closed verdict, and learning report) should be captured locally after opening `marketing-detective.html` in a browser, then added to this folder and referenced below.

- `screenshot-theme-picker.png`
- `screenshot-investigation-board.png`
- `screenshot-case-closed.png`
- `screenshot-learning-report.png`

## How to Run
1. Download `marketing-detective.html`
2. Open it directly in any modern browser (double-click or drag into a browser window) — no server or install required
3. Choose a theme, accept a case, and start investigating