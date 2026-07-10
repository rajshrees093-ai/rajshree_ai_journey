# Day 31 — AI Supply Chain Control Tower

## Overview
Built an interactive single-file HTML/CSS/JS simulation game where the player acts as
Head of Operations, triaging live supply chain disruptions (port congestion, supplier
delays, stockouts, demand spikes, etc.) under a 3-minute countdown, while managing
Service Level, Customer Satisfaction, Inventory Health, Transportation Efficiency,
Operating Cost, Revenue Protected, and Score.

- **Tool used:** Claude (effort level: Low)
- **Output file:** `control-tower.html`
- **Type:** Single self-contained HTML file — no frameworks, no backend, works offline

## Screenshots


## How I Ran It
1. Opened Claude, set effort level to Low, started a new conversation.
2. Pasted the AI Supply Chain Control Tower prompt.
3. Claude generated a complete single-file HTML application.
4. Saved the file locally and opened it directly in the browser — no server needed.
5. Played a full 3-minute shift, reacting to alerts as they streamed in.
6. Replayed once to compare strategies and improve the final score.

## Key Learnings
- **Prioritization under time pressure is the real skill being tested** — critical alerts
  (like a factory machine failure) need to be triaged before medium-priority ones, even
  if the medium one appeared first.
- **Every action has a tradeoff.** The "safe" generic response (e.g., Air Freight) isn't
  always correct — using it on a local truck breakdown wastes cost instead of fixing the
  problem. Matching the action to the actual root cause mattered more than reacting fast.
- **Ignoring alerts is expensive.** Letting a timer run out consistently produced the
  worst KPI and score penalties, reinforcing that in real operations, indecision is
  itself a costly decision.
- **Difficulty scaling changed my strategy.** As alert frequency increased late-game, I
  had to shift from "solve everything perfectly" to "protect the biggest KPI risks first
  and accept smaller losses elsewhere" — a realistic tradeoff for an ops leader.
- **Prompting takeaway:** A single, highly structured prompt (explicit KPIs, alert types,
  action consequences, difficulty curve, and end-game requirements) let Claude generate a
  fully playable, self-contained simulation in one pass with no follow-up debugging needed.

## Files in this folder
- `control-tower.html` — the generated game (open directly in any browser)
- `day31.md` — this write-up
- `screenshots/` — gameplay screenshots