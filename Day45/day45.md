# Day 45 — Build an AI Decision Strategist

## What this is
A single-file, self-contained HTML app (`decision-strategist.html`) that walks a user through the same 4-question interview a Decision Strategist would ask, then generates a full interactive **Decision Report** — matrix scoring, premortem, 7-day test plan, verdict, and shareable cards — entirely in the browser. No server, no API key, no build step: open the file and it works.

## How it works
1. **Setup screen** — user names Option A, Option B, and (optionally) Option C.
2. **4-question interview**, one screen at a time, matching the original prompt exactly:
   - What's the decision, and why is it hard?
   - What's the goal and timeline?
   - What does your gut say, and what's stopping you?
   - What are you most afraid of getting wrong, and is it reversible?
3. On submit, a lightweight in-browser **rule engine** (not a live LLM call — pure JS heuristics on keywords like *risk, safe, reversible, stress, passion, regret*) scores each option across 7 dimensions (Life/Career Upside, Financial Safety, Growth & Learning, Stress Level, Reversibility, Long-term Alignment, Regret Risk) out of 10 each, 70 total.
4. The report renders all 8 required sections — Real Decision, Case for Each Option, Assumption Buster, animated Decision Matrix, Premortem for the top 2 options, 7-Day Test Plan, Verdict, and 3 shareable mini-cards — styled to the dark, card-based design spec (Inter typeface, CSS-variable palette, animated gradient bars, glowing gold verdict card).

## Key learnings
- **Escaping strings inside template-literal-heavy JS is a real trap.** My first draft used `\'` inside single-quoted JS strings that were *also* embedded inside an HTML template literal — that double layer of escaping broke parsing. Switching those specific strings to double quotes (so the apostrophe didn't need escaping at all) fixed it. Lesson: when generating JS strings with contractions ("don't", "it's"), prefer double-quoted strings over escaped single quotes, or a syntax checker will catch it in seconds — which it did here (`node --check`).
- **A rule-based "AI" is a legitimate substitute for a live model call in a client-only artifact.** Since this file has to run standalone in a browser with no backend, the "intelligence" is a transparent keyword-scoring heuristic instead of a real Claude API call. It's honest about that trade-off rather than pretending to be a live model.
- **Following a detailed design spec literally (exact hex values, exact border-left accent colors per section, exact animation timing) produces a far more polished, consistent result** than improvising a similar-looking palette — worth the extra care to match values precisely (e.g. `--accent-gold: #fbbf24` for the verdict card glow) rather than eyeballing "something gold-ish."
- **Testing generated code before calling it done matters even for "just HTML."** Extracting the embedded `<script>` block and running `node --check` against it caught a syntax error that would otherwise have silently broken the entire report-generation step for every user.

## Files in this folder
- `decision-strategist.html` — the working app (open directly in any browser)
- `day45.md` — this writeup
- `screenshots/` — add your own screenshots of the intake flow and the generated report here before committing