# Day 44 — Build an AI-Powered LinkedIn Profile Optimizer

**Track:** AI Career Tools
**Deliverable:** `linkedin-optimizer.html` (interactive, self-contained, no build step)

## What this is

A single-file HTML/CSS/JS app that walks a user through the "LinkedIn Optimization
Expert" prompt end to end, in-browser:

1. **Path choice** — "I already have a LinkedIn" vs. "I don't have one yet," each
   routing to its own 5-question interview (asked one at a time, matching the
   prompt's original interview flow).
2. **Part 1 — The Roast**: a Profile Report Card scoring Headline, About (hook),
   About (full), Experience, and Skills out of 10 each, an overall score out of
   100, and an expandable ❌ problem / 🧠 why it hurts / 🔍 invisible cost
   breakdown per section — quoting the user's own words back at them.
3. **Part 2 — The Rebuild**: 3 headline options (keyword / value-prop / authority),
   a full About section rewrite (hook → story → proof → CTA) with embedded
   keywords, before/after bullet rewrites for the top experience entry, and
   skills to add / remove / pin.
4. **Part 3 — Scorecard**: before vs. after score table per section plus overall.
5. **Part 4 — 7-Day Activation Plan**: expandable day-by-day cards, including
   drafted posts (with live character counts), a connection-request template,
   and the "Agree + Add Insight + Ask a Question" value-comment formula.
6. **Part 5 — Shareable Summary Card**: a screenshot-ready recap (before/after
   score, top 3 mistakes, single biggest lever) with a one-click copy button.

## How the scoring works

This build runs as a **rules-based heuristic engine in the browser** (regex and
keyword-list checks for generic phrasing, action verbs, presence of numbers,
CTA language, word counts, etc.) rather than a live call to the Claude API. That
was a deliberate choice so the exported HTML file works fully offline, opened
directly from disk, with zero API key and zero network dependency — which
matches the task's "save it, open it locally" step. The prompt's structure,
scoring rubric (`/10` per section, `/100` overall), and every section of the
5-part output format were preserved exactly from the source prompt.

## Files in this folder

| File | Purpose |
|---|---|
| `linkedin-optimizer.html` | The full interactive app — open directly in any browser |
| `day44.md` | This write-up |
| `screenshots/` | Add your own screenshots here (see below) |

## How to test it

1. Open `linkedin-optimizer.html` in a browser (double-click, or `open linkedin-optimizer.html`).
2. Choose a path (has a profile / doesn't have one yet).
3. Answer the 5 questions — try it once with a deliberately weak, generic
   profile (e.g. headline: "Marketing Coordinator," about: empty, a bullet like
   "Responsible for managing social media") to see the roast hit hard, and once
   with a stronger input to see the scores shift up.
4. Review all 5 parts, expand a couple of the day-plan cards, and try the
   "Copy summary text" button on the final card.

## Screenshots to add

This repo folder needs 3–4 screenshots dropped into `screenshots/` before
committing, since they depend on your own test run:

1. The intake wizard (Question 1 of 5)
2. The Profile Report Card (Part 1) with an expanded ❌🧠🔍 detail panel
3. The Before/After scorecard (Part 3)
4. The Shareable Summary Card (Part 5)

## Key learnings

- **Structure > cleverness.** The original prompt's value is almost entirely
  in its rubric and 5-part output shape (Roast → Rebuild → Scorecard → Plan →
  Summary Card). Porting that structure faithfully into a UI mattered more
  than the specific scoring logic underneath it.
- **Heuristics can stand in for "AI" convincingly for a demo tool**, as long as
  the checks are grounded in real signal (generic phrases, action verbs,
  presence of numbers/CTAs) — but they're not a substitute for an actual model
  call when nuance matters, which is worth flagging honestly to users rather
  than presenting canned logic as if it "understood" the profile.
- **Asking one question at a time**, even in a static form, keeps the
  interaction closer to the original conversational prompt than a single long
  form would — it also makes each answer feel considered rather than rushed.
- **A self-contained file (no backend, no API key) is a real constraint** worth
  designing around from the start once "open it locally" is a requirement —
  it shaped the decision to keep everything client-side.

## Deliverable

GitHub commit URL: _add after pushing this folder to your repo_