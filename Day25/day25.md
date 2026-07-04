# Day 25 — AI Shark Tank Simulator

## What I Built
A single-page HTML/CSS/JS app that simulates pitching a startup to a panel of 4 AI "shark" judges — a Venture Capitalist, a Founder, a Customer, and an Angel Investor — each with a different lens (market size, execution, usefulness, profitability). The app runs a full pitch round, scores the startup across 5 dimensions, and delivers an investment decision with valuation and reasoning.

**File:** [`shark-tank-simulator.html`](./shark-tank-simulator.html)

## Features Implemented
- Startup input form (name, problem, solution, revenue model, target audience, funding ask)
- 4 AI judges, each asking 2 tailored questions (8 total)
- Live Q&A transcript with dynamic judge reactions to each answer
- Scorecard across Market Potential, Innovation, Business Model, Execution, and Investment Worthiness (0–100)
- Investment decision: Invest / Acquire / Come Back Later / Reject — with suggested valuation, funding amount, equity %, and reasoning
- Dark "tank" themed UI with animated bubbles, sonar-style judge indicators, and animated scorecards
- Confetti animation on Invest/Acquire outcomes
- Downloadable PDF pitch report (via jsPDF)
- Persistent leaderboard (localStorage) ranking past pitches by score
- Share Result button (Web Share API with clipboard fallback)

## My Test Pitch

| Field | Value |
|---|---|
| Startup Name | _fill in_ |
| Problem | _fill in_ |
| Solution | _fill in_ |
| Revenue Model | _fill in_ |
| Target Audience | _fill in_ |
| Funding Ask | _fill in_ |

### Scorecard Results
| Metric | Score |
|---|---|
| Market Potential | _/100_ |
| Innovation | _/100_ |
| Business Model | _/100_ |
| Execution | _/100_ |
| Investment Worthiness | _/100_ |

### Final Verdict
- **Decision:** _Invest / Acquire / Come Back Later / Reject_
- **Valuation:** _$_
- **Funding Offered:** _$_
- **Reasoning:** _paste the reasoning shown in the app_

## Screenshots
_Add screenshots below (drag into GitHub or reference image files in this folder)_

1. Setup screen — startup input
2. Pitch + judges panel
3. Q&A round with a judge reaction
4. Scorecard
5. Investment decision screen
6. Leaderboard
7. Downloaded PDF report

## What I Learned
- _e.g. How to simulate "AI" judge personalities with weighted keyword/heuristic scoring instead of a live API_
- _e.g. How to structure a multi-screen single-file app with vanilla JS state management_
- _e.g. Working with jsPDF in-browser to generate downloadable reports_
- _e.g. Using localStorage for a lightweight persistent leaderboard_
- _Add your own reflections here_

## Challenges & Fixes
_Optional: note anything that didn't work as expected and how you resolved it_