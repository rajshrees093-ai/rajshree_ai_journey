# Day 47 — Content Intelligence Studio

## What I built

An AI-powered **Content Analysis Platform** — a single self-contained HTML file (vanilla HTML/CSS/JS, no external libraries) that acts as an AI content consultant. It accepts an Instagram caption and an optional image/thumbnail, then runs the content through a five-stage panel of specialized AI reviewers (Intake & Classification → Visual Composition Reviewer → Copywriting & Hook Reviewer → Engagement Psychology & Algorithm Strategist → Final Synthesis Editor), each implemented as a live `fetch` call to the Claude Messages API (`https://api.anthropic.com/v1/messages`, model `claude-sonnet-4-6`, no API key required in this environment).

Every score, insight, and recommendation shown in the dashboard is generated live by Claude — there is no hardcoded scoring logic or canned feedback. Image uploads are sent as base64 image blocks so Claude's vision analyzes the actual uploaded visual.

## Interview inputs used to configure this build

| Question | Answer |
|---|---|
| Content type | Social media post/caption |
| Platform | Instagram |
| Primary goal | Maximize engagement |
| Upload type | Both text and image together |
| Review strictness | Expert-level — pre-launch audit |

## Key features delivered

- **Upload interface**: caption textarea + drag-and-drop image dropzone with live preview, platform/goal/strictness selectors.
- **Live multi-stage reviewer pipeline**: animated stage list (pending → active → done) alongside a real-time terminal-style activity log.
- **Content Health Orb**: animated circular score gauge (0–100) plus category breakdown bars (Hook Strength, Visual Impact, Copy Quality, Engagement Potential, Platform Fit).
- **Tabbed report**: Overview (executive summary + before/after caption comparison), Strengths & Weaknesses & Missed Opportunities, Rewrite & Alternative Hooks, Publishing Checklist (interactive checkboxes), Predicted Performance (clearly labeled as an AI estimate, not a guarantee), and a Full Report tab showing every reviewer's raw output.
- **No-JSON output protocol**: all API responses use a custom plain-text labeled-section format (e.g. `OVERALL_SCORE:`, `STRENGTHS:`) parsed with string/regex splitting in JavaScript — this avoids the `expected '{' or '('` class of JSON-parsing errors entirely.
- **Robust error handling**: automatic one-time retry on API failure, visible error banner with a manual retry button, loading/disabled states on the run button, and a live log line for every retry or failure.
- **Design**: dark-mode-only premium SaaS aesthetic — near-black background, violet-to-pink gradient accent, monospace type for data/log/score elements, animated pipeline connectors and score fills, fully responsive down to mobile.

## How it works (architecture)

1. User fills in the caption, platform, goal, strictness, and optionally uploads an image (converted to base64 via `FileReader`).
2. Clicking **Run AI Content Audit** kicks off `runAudit()`, which iterates through the `STAGES` array sequentially.
3. Each stage builds its own system prompt (a distinct expert persona) and user prompt, optionally attaching the image block for vision-capable stages (Intake, Visual Reviewer).
4. `callClaude()` posts to the Messages API and retries once on failure before surfacing an error.
5. The **Final Synthesis Editor** stage receives all prior stage outputs as context and returns one authoritative plain-text report using fixed section headers.
6. `parseFinalReport()` splits that text into fields by locating each header and slicing until the next one, then the UI renders scores, bars, lists, and text into the dashboard.

## Key learnings

- Avoiding JSON as the interchange format between the LLM and the frontend eliminates an entire category of brittle parsing failures (`expected '{' or '('`, trailing commas, truncated objects) — a fixed plain-text labeled-section protocol with a positional parser is far more resilient to minor formatting drift from the model.
- Chaining reviewer stages and passing each prior stage's output forward as context produces a noticeably more coherent final synthesis than asking one prompt to do everything at once — each specialist stays narrow and the editor stage gets to do real synthesis instead of speculation.
- Vision analysis needs to be scoped carefully: only the Intake and Visual Reviewer stages needed the image attached, which kept the later stages faster, cheaper, and focused on text.
- Framing the "Predicted Performance" section explicitly as an AI estimate (with a visible disclaimer) is important so the tool doesn't overstate confidence about real-world outcomes it can't actually measure.
- Building the reviewer pipeline as data (an array of stage objects with a `build()` function) instead of hardcoding five near-identical blocks made the whole workflow much easier to extend to other content types and platforms later.

## Files in this folder

- `content-intelligence-studio.html` — the complete, working single-file application
- `day47.md` — this file
- `screenshots/` — screenshots of the app in use (upload screen, live pipeline, and final report)

## How to run it

1. Download `content-intelligence-studio.html`.
2. Open it directly in any modern browser (double-click, or drag into a browser window).
3. Fill in a caption, optionally upload an image, and click **Run AI Content Audit**.
4. Watch the live reviewer pipeline, then review the generated Content Health Report.