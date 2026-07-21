# Day 42 — Personal Financial Command Center

## Overview
Built an AI-powered financial dashboard using Claude, tailored for a **Business Owner / Investor** managing a growing company with multiple revenue streams, while balancing personal finances alongside the business.

**Deliverable:** [`financial-command-center.html`](./financial-command-center.html) — a single self-contained HTML/CSS/JS app called **"The Ledger Room."**

## My Profile Inputs (via Claude's interview)
| Question | My Answer |
|---|---|
| Who is this dashboard for? | Business Owner / Investor |
| Primary financial goal | Balance business + personal finances |
| Business setup | Growing company with multiple revenue streams |
| Investments held? | Just starting to invest |
| Debt / loans? | No debt currently |
| Module design | Auto-design (Claude selected modules) |

## Modules Generated
- **Overview Dashboard** — financial health score, cash flow trend, revenue mix, business vs. personal spend
- **Revenue Streams** — editable table + 6-month trend chart across multiple income lines
- **Personal Income** — owner draws and other personal earnings
- **Expenses** — tagged business/personal, category breakdowns
- **Budgets** — category ceilings vs. actuals with progress bars
- **Cash Flow** — combined net position + 6-month projection
- **Savings & Reserve** — separate business and personal emergency funds with months-covered tracking
- **Investing Starter** — beginner contribution planner with compound growth projection and a suggested starter portfolio mix
- **Goals** — business and personal milestones tracked side by side
- **AI Insights** — rule-based recommendations generated live from the data (revenue concentration risk, reserve gaps, savings rate, budget overruns)
- **What-If Simulator** — sliders for revenue growth, expense change, new investment, new hire cost, with live score/net impact
- **Reports** — printable snapshot summary
- **Tips & Resources** — checklist + suggested Claude prompts for continued financial literacy

## Key Learnings
1. **Structured interviews improve personalization** — answering MCQ-style questions one at a time let Claude tailor modules (e.g., "Investing Starter" instead of a full portfolio tracker, since I'm new to investing) rather than generating a generic template.
2. **Separating business and personal finances visually** (tags, split charts, split reserves) made it much easier to see where the two overlap and where they don't — a common blind spot for business owners.
3. **The financial health score formula** (revenue diversity + savings rate + reserve coverage + cash flow positivity) turned scattered numbers into one trackable metric.
4. **The What-If Simulator** was the most useful module for decision-making — instantly seeing how a new hire's cost affects the health score is more actionable than a static budget.
5. **Single-file HTML apps with localStorage** are a fast way to prototype internal tools without needing a backend — good pattern for future personal tooling.

## Screenshots
See `/screenshots` folder in this Day42 directory.

## How to Run
1. Download `financial-command-center.html`
2. Open it directly in any modern browser (no server needed)
3. All data is editable inline and persists via localStorage