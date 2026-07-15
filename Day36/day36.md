# Day 36 — Explore Your Thinking Patterns

## Overview
Built **Cognitive Pattern Explorer**, a single-file, offline HTML/CSS/JavaScript app that walks through a psychology-inspired self-reflection experience. The app explores five thinking tendencies — Analytical Thinker, Emotional Intuitive, Overthinking Loop Style, Action-First Decision Maker, and Balanced Reflective Thinker — through three interactive chapters and a personalized Reflection Journal.

The app is explicitly educational and reflective only: it never diagnoses or clinically assesses mental health, and uses reflective language ("you often...", "this suggests...") rather than absolute labels.

## What the app includes
- **Start screen** with Calm Mode / Stress Mode selection
- **Chapter 1 — Discover Your Thinking Style**: five everyday scenarios (phrased differently depending on mode) with four response choices each
- **Chapter 2 — Choose Your Priorities**: drag-and-drop ranking of five decision-making priorities
- **Chapter 3 — Map Your Thinking**: drag-and-drop sequencing of a personal decision timeline
- **Reflection Journal**: percentage breakdown across all five tendencies, a radial "thought orbit" SVG visualization, personalized insight text, and a mode-comparison view after replaying
- Native HTML5 drag-and-drop with a touch-event fallback and full keyboard support (space to grab, arrow keys to move, space to drop)
- Progress indicator, smooth transitions, ambient background animation, and `prefers-reduced-motion` support
- Fully responsive layout, works completely offline (no external requests, no fonts/CDN dependencies)

## Process
1. Read through the task resources and prompt template.
2. Generated the complete single-file HTML application using vanilla JS only (no frameworks), following the provided Cognitive Pattern Explorer prompt.
3. Verified the embedded JavaScript for syntax errors and confirmed the HTML document structure was well-formed.
4. Opened the generated file in a browser, completed both Calm Mode and Stress Mode runs, and reviewed the Reflection Journal and thinking profile for both.
5. Captured screenshots of the Reflection Journal and thinking profile for documentation.

## Key learnings
- **Reflective vs. evaluative framing matters.** Small language choices ("you often...", "this suggests...") change how a self-assessment tool feels — supportive and exploratory rather than clinical or judgmental.
- **Mode framing changes the same content's meaning.** Re-using identical scenarios with just a shift in urgency (Calm vs. Stress phrasing) is an efficient way to explore how context affects reported instincts, without needing entirely separate content trees.
- **Accessible drag-and-drop needs three input paths.** Supporting real usage meant implementing native HTML5 drag events for desktop, touch events for mobile, and a full keyboard-operable alternative (grab/move/drop) — not just one interaction model.
- **Weighted scoring across multiple interaction types** (single-choice scenarios, ranked priority cards, and ordered timeline steps) can be combined into one normalized percentage breakdown, giving a more rounded personalized profile than any single chapter alone.
- **Single-file, offline-first constraints** (no external fonts, no CDN, no frameworks) push toward system font stacks and hand-rolled SVG visualizations, which turned out to be lightweight and fully portable.

## Files in this folder
- `cognitive-pattern-explorer.html` — the generated single-file application
- `day36.md` — this file
- Screenshots of the Reflection Journal and thinking profile (Calm Mode and Stress Mode)