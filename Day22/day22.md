# Day 22 — Validate Your Startup Idea Like a VC

**Task:** Turn startup assumptions into evidence-based insights using an AI-powered VC-style validation framework.
**Tool used:** Claude (effort level: High)
**Deliverable:** Startup Validation Report (PDF + DOCX)

---

## 1. My Startup Idea (Discovery Answers)

| Question | Answer |
|---|---|
| **Startup Idea** | DeskDoc — an AI-powered tool that automatically generates and maintains internal documentation (SOPs, onboarding guides, process docs) by observing how a team actually works: Slack threads, meeting transcripts, and tool usage — instead of requiring anyone to write or update docs manually. |
| **Problem Being Solved** | Growing startups constantly lose institutional knowledge. Documentation goes stale the moment it's written, new hires ramp up slower because tribal knowledge lives in people's heads, and knowledge walks out the door whenever a senior employee leaves. |
| **Target Customers** | B2B — Ops leads, Heads of People/HR, and founders at Series A–B startups (15–100 employees), especially remote-first companies. |
| **Why I Want to Build It** | I was an Ops lead at two startups and personally lived this pain — onboarding new hires with zero usable documentation, and watching knowledge disappear when senior people left. |
| **Existing Validation** | No product yet. Ran 12 informal interviews with Ops/People leads: 9 of 12 confirmed documentation as a top-3 operational pain point; 5 of 12 said they'd pay for a solution today. No waitlist or prototype yet. |
| **Target Market / Country** | United States (remote-first tech startups) first, expanding to UK and Canada later. |
| **Startup, Business, or Side Project?** | Startup — intending to raise a pre-seed round, aiming for venture-scale growth. |

---

## 2. Full Report

The complete VC-style validation report (Executive Summary, Founder-Market Fit, TAM/SAM/SOM, Competitor Analysis, Market Gap, ICP, Buyer Persona, Risk Assessment, Go/No-Go, 30-Day Action Plan) is attached:

- 📄 [DeskDoc_Startup_Validation_Report.pdf](./DeskDoc_Startup_Validation_Report.pdf)
- 📝 [DeskDoc_Startup_Validation_Report.docx](./DeskDoc_Startup_Validation_Report.docx)

---

## 3. Key Insights (Screenshots)

> Replace these with your actual screenshots from the PDF, saved into a `screenshots/` folder.


---

## 4. Summary of Findings

| Dimension | Result |
|---|---|
| **Overall Verdict** | Conditional Go — strong problem signal, thin solution-stage evidence |
| **Founder-Market Fit** | 7.5 / 10 — strong domain expertise, first-time-founder gap |
| **Market Size** | TAM ~$10.1B · SAM ~$410M · SOM (Yr 3) ~$8.6M ARR |
| **Biggest Strength** | Personally lived the problem twice; 75% pain-confirmation rate in interviews |
| **Biggest Risk** | Reliable auto-synthesis from unstructured conversation data is a hard technical problem; validation sample is small (12 interviews, no prototype/paid pilot) |
| **Recommended Next Step** | Run a scoped 30-day validation sprint (more interviews + narrow prototype + paid pilot) before committing full-time or fundraising |

---

## 5. Key Learnings

- **A strong "pain" score doesn't mean a strong "willingness to pay" score.** 75% of people confirming the problem is real is very different from 42% saying they'd pay for it today — the report forced me to separate these two signals instead of blending them into one vague "validated" label.
- **TAM/SAM/SOM math is only as good as its assumptions.** Seeing the company-count and ACV assumptions spelled out (rather than just a big dollar figure) made me realize I need to verify those numbers against a real data source (e.g., Crunchbase/LinkedIn firmographics) before using them in front of investors.
- **Founder-Market Fit isn't just "do I understand the problem."** The framework broke it into domain expertise, network, technical capability, and track record separately — and flagged my weakest link (technical build capability / first-time-founder risk) instead of letting my strong domain score paper over it.
- **The Go/No-Go wasn't binary.** Instead of a flat yes/no, the "Conditional Go" framing pushed me toward a specific, time-boxed next step (30-day validation sprint) rather than either over-committing or abandoning the idea prematurely.
- **Competitor analysis revealed a real wedge, not just noise.** Every adjacent tool (Notion, Guru, Tettra, Scribe, Otter) solves half the problem — either storage or capture, never automatic synthesis into maintained docs. That gap is the actual thing worth testing first, not the product as a whole.

---

## 6. Tools & Process

1. Opened Claude, set effort level to High.
2. Started a new conversation and pasted the Startup Validation prompt.
3. Answered the 7 discovery questions (see Section 1 above).
4. Reviewed the generated report section by section (Founder-Market Fit → TAM/SAM/SOM → Competitors → Market Gap → ICP → Risk → Go/No-Go → 30-Day Plan).
5. Exported the report as PDF and DOCX.
6. Took screenshots of the key sections.
7. Compiled this `day22.md` with the findings and reflections.
8. Committed and pushed to GitHub.