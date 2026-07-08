# Day 29 — Operation Lifeline: Supply Chain Crisis Lab

## Overview

**Operation Lifeline** is a single-file, browser-based simulation that puts the
player in the role of Chief Supply Chain Officer at a randomly generated
company facing a randomly generated crisis. It was built as a single HTML
file using React (via CDN) and Babel JSX, with no backend, no build step, and
no external assets — it runs by opening the file directly in a browser.

- **App file:** `operation-lifeline.html`
- **Tech stack:** React 18 (CDN), Babel Standalone (CDN), plain CSS
- **Effort level used:** Low
- **Deliverable type:** Single-file interactive HTML application

## Simulation Flow

1. **Welcome Screen** — introduces the scenario and role.
2. **Company Profile** — randomly generates an industry, revenue, factory
   count, warehouse count, supplier count, inventory days, lead time, and
   countries of operation, shown as modern stat cards.
3. **Crisis Briefing** — randomly selects one of eight crisis types (factory
   fire, supplier bankruptcy, port strike, cyberattack, flood, raw material
   shortage, political conflict, shipping delay) with urgency level and a
   plain-language business impact explanation.
4. **War Room** — the player selects exactly 3 of 6 response actions. Each
   action has a stated trade-off; choices are simulated into animated bar
   changes across Cost, Inventory, Profit, Delivery Speed, and Customer
   Satisfaction.
5. **Supplier Negotiation** — 4 branching rounds. Each choice affects Trust,
   Price Favorability, and Lead Time, producing a Negotiation Score.
6. **CEO Boardroom** — 5 multiple-choice leadership questions, scored to
   produce a Leadership Score.
7. **AI Strategy** — the player picks 2 of 5 AI investments (Demand
   Forecasting, Inventory Optimization, Supplier Risk Monitoring, Warehouse
   Vision, Procurement Copilot), each with a stated expected impact.
8. **Executive Dashboard** — final Overall Crisis Score (0–100) plus six
   sub-scores (Leadership, Negotiation, Resilience, Cost Control, Risk
   Management, Customer Satisfaction), personalized feedback, biggest
   mistake, best decision, an expert recommendation, and lessons learned.

Every playthrough randomizes the company, the crisis, and — because outcomes
are driven by the player's own choices — the final scores.

## Screenshots

> Screenshots below were captured during a live playthrough of the simulator.


*(Replace the paths above with the actual screenshot filenames uploaded to
this folder.)*

## Key Learnings

- **Trade-off design beats "right answer" design.** The most useful part of
  building this lab was resisting the urge to make one obviously optimal
  path. Every War Room action, negotiation choice, and AI investment has a
  genuine cost, which is what makes the final scorecard feel earned rather
  than arbitrary.
- **State needs to flow forward, not just exist per screen.** Because the
  final dashboard depends on decisions made four screens earlier (War Room
  metrics, negotiation trust/price/lead time, leadership points, AI bonuses),
  the app's state had to be lifted to the top level and passed down/collected
  back up cleanly — a good reminder of why centralized state matters even in
  a "simple" single-file app.
- **A single low-cost action (transparent communication) can rival an
  expensive one (air freight) in impact.** Modeling this in the War Room
  made the underlying supply chain lesson tangible: speed isn't the only
  lever for customer satisfaction — clear communication is a cheap, high-leverage
  one.
- **Offline-friendly still means CDN-dependent.** Building this as a "no
  backend, no npm install" single file still meant relying on CDN-hosted
  React and Babel. The practical lesson: a fully offline-first version would
  need the libraries bundled directly into the file rather than fetched at
  runtime — worth remembering for any future single-file app that must work
  with zero internet access.
- **Diagnosability matters as much as functionality.** Early on, the app
  could fail silently (blank screen) if the CDN scripts didn't load. Adding
  a loading state and an on-page error message turned an invisible failure
  into an actionable one — a small addition that meaningfully improved the
  experience.

## How to Run

1. Download `operation-lifeline.html`.
2. Open it directly in Chrome, Edge, or Firefox.
3. Ensure the device has an internet connection the first time it opens
   (it loads React and Babel from a CDN).
4. Click **Start Simulation** and play through the eight stages above.
5. Use **Replay with a New Scenario** on the final dashboard to generate a
   new company and crisis.