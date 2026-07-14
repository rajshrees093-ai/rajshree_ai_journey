# Day 35 — Prompt Puzzle: Master AI Prompting Through Play

**Category:** Intermediate | **Time:** 75 min | **Deliverable:** GitHub commit URL

## Overview

Today's build is a single-file HTML/CSS/JavaScript game — **🧩 Prompt Puzzle** — that teaches prompt engineering through interactive play instead of reading theory. It runs entirely offline (no CDN, no build step, no network calls) and works by simply double-clicking the HTML file.

- **Domain practiced:** Creative Writing
- **Difficulty:** Intermediate
- **Scenario pool:** 6 randomized creative-writing scenarios (fantasy fiction, flash fiction, poetry, screenplay dialogue, children's stories, horror micro-fiction)
- **Challenge types (3 per playthrough, randomly assigned scenarios):**
  1. **Build the Prompt** — drag correct instruction blocks into the right order while ignoring distractor blocks
  2. **Clean the Prompt** — sort an over-engineered, contradiction-riddled prompt into "Keep" (essential) vs. "Trash" (fluff)
  3. **Choose the Best Prompt** — pick the strongest of three prompts (Weak / Optimized / Over-Engineered) for a given desired output

## How the Prompt Was Used

The provided "Prompt Puzzle" master prompt was pasted into Claude with effort set to **Low**. Claude asked exactly the two required onboarding questions before generating anything:

1. *Which domain would you like to practice prompting for?* → **Creative Writing**
2. *Choose your difficulty.* → **Intermediate**

Claude then generated the complete single-file HTML application per the spec — no React CDN dependency was used (to guarantee offline reliability), so the app was built in vanilla HTML/CSS/JS instead, per the prompt's own fallback instruction.

## Live Scoring System

Each playthrough tracks, in real time:

| Metric | What it measures |
|---|---|
| Accuracy | Average correctness across all 3 rounds |
| Time | Total seconds elapsed |
| Moves | Every drag/click interaction |
| Wrong Placements | Distractors placed, fluff kept, essentials trashed, wrong prompt chosen |
| Hints Used | Number of hints requested (costs score) |
| Optimization Bonus | Awarded for flawless, hint-free rounds |

## Prompt Performance Report

At the end of the 3 rounds, a full report is generated:

- **Prompt Score** (0–1000, animated count-up)
- **Rating** (Prompt Novice → Apprentice → Adept → Architect → Grandmaster)
- **Rank** (D / C / B / A / S)
- **Prompt DNA** — a 5-trait radar-style bar visualization: Clarity, Specificity, Structure, Constraint-Setting, Efficiency
- **Personalized feedback** based on accuracy, hint usage, and wrong-placement patterns
- **Next milestone** — points at the single weakest DNA trait to improve
- **Final optimized prompt reference** — a gold-standard example prompt to study

Replay is supported and reshuffles a new set of 3 scenarios from the pool of 6, with all metrics reset.

## Key Learnings

1. **Specificity beats vagueness, every time.** Across every scenario, the "optimized" prompt won not because it was longer, but because it named exact constraints (word count, audience, technique, ending behavior) instead of leaving them open.
2. **Over-engineering is not the opposite of a weak prompt — it's a different failure mode.** Padding a prompt with hedges like "maybe X, maybe Y, your choice" creates contradictions that force the model to guess, producing inconsistent output despite the extra words.
3. **Negative constraints are underused.** Telling the model what *not* to do (e.g., "not abstract emotion words," "not explicit gore") sharpened creative output as much as positive instructions did.
4. **Naming the craft technique, not just the topic, matters.** "Use subtext" or "build dread through implication" gave the model a method, not just a subject — this consistently separated optimized prompts from merely correct-but-generic ones.
5. **Order and structure carry meaning.** In the "Build the Prompt" challenge, block sequence (format → subject → technique → constraint) mattered — scrambled correct blocks still lost points, reinforcing that prompt structure itself is a signal.
6. **Gamifying prompt critique makes the lesson stick.** Actively sorting fluff from substance (Clean the Prompt) built a much faster intuition for spotting bloated prompts than reading about it would have.

## Files in this folder

- `prompt-puzzle.html` — the complete, offline-playable application
- `day35.md` — this file
- `screenshots/` — gameplay screenshots (start screen, each challenge type, and the final Prompt Performance Report)

## Replay Notes

A second playthrough was run via the in-app **Replay with New Scenarios** button, which reshuffled a new combination of 3 scenarios (out of the 6-scenario pool) across the same three challenge types, confirming the randomization and scoring reset correctly.