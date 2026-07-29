# Day 50 — Defend Your Experience

**Challenge:** Build an AI-Powered Adaptive Interview Defense Simulator
**Deliverable:** Single self-contained HTML app + this write-up

## What this is

`defend-your-experience.html` is a single-file HTML/CSS/JS application, styled as an editorial "case file" / cross-examination dossier. It is **not** a resume reviewer — it extracts every meaningful claim from an uploaded document and then cross-examines the user on each claim, one adaptive question at a time, using the Anthropic Messages API directly from the browser (as required by the prompt — no backend, no API key entry).

## How it works

1. **Onboarding** — explains the tool's purpose and offers to resume a saved session (via `localStorage`).
2. **Exhibit upload** — drag-and-drop a `.txt`/`.md` file or paste text directly (resume section, README, portfolio write-up, performance review, startup narrative, etc.).
3. **Claim extraction** — one API call extracts every meaningful, defensible claim from the document into a structured "docket" (JSON: id, text, category, risk level).
4. **Adaptive cross-examination** — the app alternates between two API calls:
   - generate the next question, given the full claim docket + running transcript (so questions get more specific and pointed as the session goes on)
   - evaluate the user's answer for specificity, evidence, and ownership, updating that claim's status to `untested → holding / weak / defended`
5. **Docket sidebar** — live status "stamps" per claim (Untested / Holding / Weak / Defended) plus a progress bar.
6. **Defense Report** — a final API call synthesizes the whole transcript into an overall score (radial gauge), strengths, weaknesses, per-claim recommendations, and prioritized next steps before the real interview.
7. **Resilience** — all API calls retry on `429` rate limits with backoff, surface a dismissible error banner with a manual retry button on failure, and never lose the user's typed answer.
8. **Export** — Print/PDF, JSON export, and plain-text transcript export. Session state persists in `localStorage` so a refresh doesn't lose progress.

## Design direction

Editorial / premium style (per my own design preference, selected via MCQ): warm ivory paper background, Fraunces (display serif) + Source Serif 4 (body) + IBM Plex Mono (data/labels), burgundy/forest/brass accent system. Signature element: claims are rendered as case-file "exhibit" cards with rotated status stamps, reinforcing the courtroom cross-examination metaphor the whole tool is built around.

## Key learnings

- Splitting the AI's job into **three narrow, single-purpose calls** (extract → ask → evaluate → summarize) produced far more reliable structured JSON than one big "run the whole interview" prompt — smaller, well-scoped system prompts with a strict JSON schema were much easier to parse and recover from.
- Feeding the **entire running transcript** back into the "next question" prompt (not just the current claim) is what made follow-ups feel adaptive instead of like a fixed questionnaire — the model naturally chose to dig deeper on weak answers and pivot away from strong ones.
- Graceful degradation matters as much as the happy path: rate-limit backoff, a visible retry affordance, and never clearing the user's answer on a failed request made the tool feel trustworthy rather than fragile.
- A visual metaphor grounded in the tool's actual purpose (a legal "docket" / cross-examination) gave the UI a distinct identity for free — status stamps and case-file language did more work than generic dashboard styling would have.

## Screenshots

_Add screenshots here: onboarding screen, upload screen, interview/docket in progress, and the final Defense Report._

- `screenshots/01-onboarding.png`
- `screenshots/02-upload.png`
- `screenshots/03-interview.png`
- `screenshots/04-report.png`

## Files in this folder

- `defend-your-experience.html` — the complete, self-contained application
- `defense-report-sample.json` / `.txt` — exported Defense Report from a practice session
- `screenshots/` — screenshots from a practice run
- `day50.md` — this file