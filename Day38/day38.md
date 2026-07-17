# Day 38 — Typing Speed Studio

**Deliverable:** Premium single-page typing platform, "Lexicon Studio," built as one self-contained HTML file (HTML + CSS + JS, no external libraries).

## Interview answers used to generate this build

1. **Typing experience:** Business / Academic / Medical / Legal / Creative Writing — a multi-domain platform where the user switches between professional text categories from a domain selector.
2. **Feature selection:** Auto-decide — Claude chose the full premium feature set described in the prompt template rather than a custom subset.

## What was built

- **8 typing modes:** Time (15/30/60/120s), Word Count (25/50/100/250), Quote, Programming (JS, Python, HTML, CSS, Java, C++, SQL), Custom Text, Adaptive (difficulty responds to your rolling accuracy), Focus (single active line), and Zen (untimed, distraction-free).
- **5 domain passage banks** (Business, Academic, Medical, Legal, Creative Writing) with hand-written, non-repeating passages per category — no single hardcoded paragraph reused across modes.
- **Live stats bar:** WPM, Raw WPM, CPM, Accuracy, Elapsed Time, Mistake Count, Current Streak, Remaining Time/Words, and Completion % with a real-time progress bar.
- **Character-level feedback:** correct / incorrect / extra / current-cursor highlighting with smooth transitions.
- **Post-session analytics dashboard:** WPM & Raw WPM, Accuracy, Consistency (derived from WPM sample variance), full character breakdown (correct/incorrect/extra/missed), an error heatmap of commonly mistyped keys, WPM-over-time and accuracy-over-time canvas charts, personal bests, an estimated percentile, unlockable achievement badges, and a generated performance summary with strengths/weaknesses and targeted suggestions.
- **Local session history** stored in `localStorage` (last 200 sessions) — reviewable in a history table with personal-best tags, no account required.
- **Realistic-value safeguards:** rate calculations floor the time denominator at 1 second and cap displayed WPM at a realistic ceiling so the app never reports absurd values like 20,000 WPM from a burst of fast keystrokes at session start.
- **Extras:** optional sound effects (Web Audio beeps), keyboard shortcuts (`Tab` restart, `Esc` pause/resume, `Enter` new passage), pause/resume, font size control, dark/light theme toggle, caps-lock indicator, and a responsive layout down to mobile.

## Key learnings

- **WPM math needs guardrails.** A naive `(chars/5) / minutesElapsed` formula spikes wildly in the first fraction of a second of a session. Flooring the elapsed-minutes denominator at 1 second (while still measuring true accuracy/mistakes immediately) keeps early readings sane without breaking the running calculation once real time has passed.
- **Domain-specific content generation matters more than it first appears.** Writing five distinct passage banks (rather than one generic paragraph reused everywhere) is what makes the "Business vs. Medical vs. Legal" premise actually land — the practice text has to sound like the profession it claims to represent.
- **Defensive coding around browser APIs pays off.** Wrapping canvas chart rendering in a try/catch meant a charting failure never blocked the rest of the analytics dashboard (character breakdown, badges, summary) from displaying — verified by headless testing where the sandbox's Node environment had no real `<canvas>` implementation.
- **Headless testing with jsdom caught a real bug before it shipped**: an unguarded `canvas.getContext("2d")` call was throwing and silently preventing the results dashboard overlay from ever opening after a completed session — a hard-to-notice failure in a quick manual click-through, but obvious once the full keystroke sequence was scripted end-to-end.

## Files in this folder

- `typing-speed-studio.html` — the complete, self-contained application.
- Screenshots of the app in use (typing modes + analytics dashboard) — add after running locally per the task checklist.