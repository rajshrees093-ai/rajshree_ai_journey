# Day 30 — Supply Chain Optimizer

**Deliverable:** `supply-chain-builder.html` — a single-file React app that teaches supply chain
fundamentals by having the player build a chain for a randomly generated company, then scores
the result on an Overall Supply Chain Score dashboard.

## What the app does

1. **Welcome screen** — plain-language introduction to what a supply chain is and the six
   building blocks (Suppliers, Factory, Warehouse, Transport, Inventory, Trade-offs).
2. **Company generator** — randomizes an industry, 2 products, 2–4 countries served, and a
   demand pattern (Steady / Fast-Growing / Seasonal Spikes / Highly Volatile) on every playthrough.
3. **Five guided decisions**, each with a "what it means / why it matters" explainer before the
   choice, and a plain-English trade-off callout after it:
   - Supplier strategy (single vs. multiple)
   - Factory location (domestic / offshore / nearshore)
   - Warehouse strategy (centralized / regional / just-in-time)
   - Transportation method (road / rail / sea / air)
   - Inventory strategy (low / balanced / high)
4. **Live metrics panel** — Cost, Delivery Speed, Risk, Customer Satisfaction, and Sustainability
   update immediately after every decision with animated bars.
5. **Animated chain map** — a signature visual: a route line with a traveling light shows how far
   through the chain (Suppliers → Factory → Warehouse → Transport → Inventory → Customer) the
   player has progressed.
6. **Final dashboard** — an animated 0–100 Overall Supply Chain Score ring, computed strengths and
   weaknesses, a "Biggest Risk" callout that reads the actual combination of decisions made (e.g.
   single supplier + offshore factory = concentration risk), three tailored improvement
   recommendations, a recap of every decision, and a Replay button that regenerates a brand-new
   company.

## Tech notes

- Single HTML file. React 18 + ReactDOM 18 + Babel Standalone loaded via CDN `<script>` tags;
  everything else (styling, state, logic) is plain CSS and JS inside one `<script type="text/babel">`
  block — no build step, no npm install required to run it.
- State is managed with `useState` / `useMemo` / `useCallback`; no external state libraries.
- No images or external fonts — the visual identity (dark navy base, teal "route" accent, amber
  caution accent) is built entirely from CSS gradients, borders, and system font stacks.
- Before shipping, the JSX was transpiled and rendered headlessly (Babel Standalone + jsdom) and
  clicked through a full 5-decision playthrough end-to-end to confirm there were no runtime errors.

## Commands used

```bash
# Project folder
mkdir -p day30

# Local verification (optional — not required to run the app itself,
# only used during development to catch JSX/runtime errors before saving):
npm install --no-audit --no-fund @babel/standalone react@18 react-dom@18 jsdom
node verify-render.js   # transpiles app.jsx and does a headless click-through

# To actually run the app: just open the file, no server or build needed
open supply-chain-builder.html        # macOS
xdg-open supply-chain-builder.html    # Linux
start supply-chain-builder.html       # Windows

# Git — commit the Day 30 deliverable
git checkout -b day30-supply-chain-optimizer
mkdir -p Day30
cp supply-chain-builder.html Day30/
cp day30.md Day30/
# add screenshots taken from the browser into Day30/ as well, e.g.:
# Day30/screenshot-welcome.png
# Day30/screenshot-dashboard.png
git add Day30/
git commit -m "Day 30: Supply Chain Optimizer — single-file React simulator"
git push origin day30-supply-chain-optimizer
```

## Key learnings

- **Trade-offs are the whole lesson.** Every option in the simulator improves at least one metric
  while hurting another (e.g. air freight is the fastest transport mode but the most expensive and
  least sustainable). Making that trade-off explicit *before and after* each choice is what turns
  a set of buttons into an actual teaching tool.
- **A single score hides the story.** The 0–100 Overall Score is useful as a headline number, but
  the "Biggest Risk" and "Strengths/Weaknesses" sections — which read the *combination* of choices,
  not just the final metric values — are what make the feedback feel like real operations analysis
  rather than a generic quiz result.
- **Randomization needs guardrails.** Randomizing the company (industry, products, countries,
  demand pattern) keeps replay value high, but the decision *options* and their effects stay fixed
  so the underlying lesson about cost/speed/risk/sustainability trade-offs is consistent no matter
  which company you get.
- **Zero-dependency verification matters.** Since the deliverable has no build step, I verified it
  by transpiling the JSX with Babel Standalone and driving a full click-through in a headless DOM
  before considering it done — catching issues (like Babel's default JSX runtime injecting an
  `import` statement that breaks a plain `<script>` tag) that wouldn't have shown up from reading
  the code alone.