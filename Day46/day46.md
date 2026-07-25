# Day 46 — Build Autonomous Agent Studio

**Track:** Autonomous AI Systems
**Deliverable:** Multi-agent AI system design + working single-page app

## What I built

**Autonomous Agent Studio** — a single self-contained HTML file (`autonomous-agent-studio.html`) that runs a real, live multi-agent orchestration pipeline against the Claude API. No backend, no build step — open the file in a browser, drop in an Anthropic API key, describe a task, and the agent team plans, executes, evaluates, critiques, remembers, and improves a real deliverable in an actual loop until a stop condition fires.

### Interview / setup answers used for this run

| Question | Answer |
|---|---|
| 1. Workflow domain | Blog / article draft |
| 2. Specific task | Iteratively drafted and improved a short blog intro on autonomous AI agents for small businesses |
| 3. Success criteria | Overall quality score |
| Target score | 92 / 100 |
| 4. Stopping condition | All three checked every round: plateau → threshold → hard cap (safety net) |
| Plateau delta | 2 points, 2 consecutive rounds |
| Hard iteration cap | 8 rounds |
| 5. Agent team | Auto-designed: Safety Monitor, Planner, Executor, Evaluator, Critic, Memory Manager, Improver, Final Reviewer |

## Agent roles

- **Safety Monitor** — one-time pre-check on the task brief before any work starts.
- **Planner** — turns the raw task into a concrete working brief (goal, audience, structure, length).
- **Executor** — produces the first real draft from the brief.
- **Evaluator** — re-runs *every* round, scores the current draft 0–100 against the chosen rubric, live.
- **Critic** — re-runs *every* round, goes deeper than the score to name the 2–3 highest-impact fixes.
- **Memory Manager** — re-runs *every* round, distills one lesson to carry into future rounds.
- **Improver** — re-runs *every* round, rewrites the full draft using that round's evaluation + critique + all memory so far.
- **Final Reviewer** — runs once, after a stop condition fires, and signs off on the final deliverable.

## Why it's a real loop, not a fixed pipeline

- The round portion is an actual JavaScript `while(true)` loop, not a hardcoded 3-step or 5-step sequence — the number of rounds is unknown until the stop-check decides.
- Every score, critique, and memory note shown in the UI is the literal text parsed from that round's live `fetch` call to `https://api.anthropic.com/v1/messages` — nothing is computed with regex or canned strings.
- State threads forward explicitly: each Improver call receives the prior round's full evaluation JSON, the Critic's text, and the running memory array; each Evaluator call receives the current draft plus the rubric.
- Every round checks, in fixed order: **(1) plateau** (score gain under the configured delta for 2 straight rounds), **(2) threshold** (score ≥ target), **(3) hard iteration cap** (safety fallback only). Whichever fires first is logged and shown by name in the final summary.

## How the stop-check governs information flow

The stop-check sits between Critic/Memory Manager and Improver each round. If nothing fires, the Improver gets called with everything accumulated so far and the loop continues with an incremented round counter. If something fires, the Improver is skipped entirely and the current draft, full round history, and memory log are handed straight to the Final Reviewer — the branch shown in the workflow diagram as a separate path off the Evaluator node rather than a continuation of the main cycle.

## Execution notes from the run

- The dashboard shows the loop as a real cycle (SVG diagram with a return arrow from Improver back into Evaluator, and a dashed branch from Evaluator to Final Reviewer), the currently active agent, live activity log, iteration history with round-over-round score deltas, memory updates, and execution stats (rounds, API calls, retries, elapsed time, start/final score).
- The round indicator reads as open-ended ("Round 3 — checking stop condition…") rather than "Round 3 of 5," matching the fact that the loop has no pre-set length.
- Retry logic: up to 3 attempts per API call with exponential backoff; failures are logged and surfaced, and a hard pipeline error halts gracefully with a visible message instead of hanging.

## Key learnings

1. **Stop conditions are the real design surface.** Once plateau/threshold/cap are defined precisely (and checked in a fixed order every round), the rest of the orchestration is just "call the next agent with more context." Most of the design effort went into making the stop-check unambiguous rather than into the agents themselves.
2. **State threading matters more than agent count.** The Improver is only as good as what it's handed — feeding it the Evaluator's structured JSON *and* the Critic's free-text *and* the memory log (rather than just the raw score) visibly changed how targeted its rewrites were.
3. **Structured output from the Evaluator needs defensive parsing.** Even with an explicit "respond only with JSON" instruction, occasional code-fenced or lightly-annotated responses came back — the app strips fences and falls back gracefully rather than crashing the loop.
4. **A dashboard that shows *why* the loop stopped is as important as showing that it stopped.** Naming the exact condition (plateau vs. threshold vs. cap) makes the difference between "the agent gave up" and "the agent converged" legible to a non-technical viewer.
5. **Running this fully client-side means the API key lives in the browser tab.** Fine for a personal demo/local run; a production version would need a thin backend proxy so the key never touches the client.

## Files in this submission

- `autonomous-agent-studio.html` — the full working application
- `day46.md` — this file
- `screenshots/` — dashboard mid-run, iteration history, final summary
- `execution-log.md` — downloaded run log from an actual session (via the app's "Download run log" button)