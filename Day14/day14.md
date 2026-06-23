# Day 14 — AI Job Red Flag Detector

> **30 Days of AI Challenge**
> Analyze job opportunities before investing your time.

---

## What Is the AI Job Red Flag Detector?

The AI Job Red Flag Detector is a prompt-based tool that uses Claude to analyze a job description and company information, then generates a structured risk report. It identifies unrealistic requirements, toxic workplace signals, misleading remote claims, hiring red flags, and company stability concerns — helping job seekers make smarter decisions before applying.

---

## Objective

Use Claude to analyze **AI Engineer** roles at **6 major companies** and generate risk reports for each, including:

- Overall Risk Score (0–100)
- Top Red Flags with severity ratings
- Positive Signals
- Risk Breakdown by category
- Final Verdict (Apply / Apply with Caution / Avoid)
- 5 Smart Interview Questions per company

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Claude (claude.ai) | AI analysis engine |
| Effort Level | Low |
| Output Format | Structured risk reports |
| Deliverable | HTML report + Markdown summary |

---

## Prompt Template Used

```
You are an AI Red Flag Detector for job seekers.
Analyze the Job Description and Company Information.

Identify:
1. Unrealistic Requirements
   - Excessive experience for the role
   - Too many skills/responsibilities
   - Contradictory expectations

2. Toxic Workplace Signals
   - Burnout indicators
   - 'Wear many hats'
   - 'Fast-paced', 'rockstar', 'hustle culture'
   - Poor work-life balance signals

3. Remote Job Authenticity
   - Hidden office requirements
   - Relocation expectations
   - Misleading remote claims

4. Hiring Risks
   - Missing salary information
   - Vague responsibilities
   - Excessive qualifications
   - Suspicious hiring practices

5. Company Risks
   - Reputation concerns
   - Stability concerns
   - Growth or layoff indicators

Output:
## Overall Risk Score (0-100)
### Top Red Flags — List with severity (1-10)
### Positive Signals — List positives
### Risk Breakdown Table (Requirements / Culture / Remote / Hiring / Company)
### Final Verdict: Apply / Apply with Caution / Avoid
### 5 Smart Interview Questions

Job Description: [AI ENGINEER]
Company Information: [COMPANY NAME]
```

---

## Companies Analyzed

| # | Company | Risk Score | Verdict |
|---|---------|-----------|---------|
| 1 | Google | 32 / 100 | ⚠️ Apply with Caution |
| 2 | OpenAI | 58 / 100 | ⚠️ Apply with Caution |
| 3 | Amazon | 55 / 100 | ⚠️ Apply with Caution |
| 4 | IBM | 62 / 100 | ❌ Avoid |
| 5 | Accenture | 50 / 100 | ⚠️ Apply with Caution |
| 6 | Deloitte | 52 / 100 | ⚠️ Apply with Caution |

---

## Report 1 — Google

**Risk Score: 32 / 100 | ⚠️ Apply with Caution**

### Top Red Flags

| Flag | Severity |
|------|---------|
| Requirement inflation — PhD or 8+ years expected for mid-level roles | 7/10 |
| Brutally long hiring loop — 5–7 rounds over 3–4 months, high ghosting rate | 6/10 |
| Vague scope — "cutting-edge AI" with no clear team charter | 5/10 |
| Internal politics — large org reduces visibility for new joiners | 5/10 |

### Positive Signals

- World-class compute, data, and research infrastructure
- Transparent salary bands on levels.fyi; strong equity
- Genuine remote/hybrid flexibility
- Strong publication culture — real foundational research is possible

### Risk Breakdown

| Category | Risk Level |
|----------|-----------|
| Requirements | High |
| Culture | Moderate |
| Remote Authenticity | Low |
| Hiring Process | High |
| Company Stability | Low |

### 5 Smart Interview Questions

1. What does the first 90-day roadmap look like — is there a defined project or is scope still being shaped?
2. How does the team handle priority conflicts between research goals and product deadlines?
3. What percentage of engineers on this team have been here longer than two years?
4. Are publications and open-source contributions encouraged, or does IP policy limit them?
5. How is performance evaluated — research output, product impact, or a combination?

---

## Report 2 — OpenAI

**Risk Score: 58 / 100 | ⚠️ Apply with Caution**

### Top Red Flags

| Flag | Severity |
|------|---------|
| Extreme hustle culture — "move fast", "high urgency", burnout-culture language | 9/10 |
| Org instability — leadership drama (Nov 2023), rapid headcount changes | 8/10 |
| Wear many hats — research, infra, deployment, and safety reviews simultaneously | 7/10 |
| Complex equity structure — profit participation units hard to value | 6/10 |

### Positive Signals

- Unmatched AI brand name — transformative resume credential
- Direct access to frontier models and cutting-edge research
- Competitive top-of-market compensation for AI talent

### Risk Breakdown

| Category | Risk Level |
|----------|-----------|
| Requirements | High |
| Culture | Very High |
| Remote Authenticity | Moderate |
| Hiring Process | Moderate |
| Company Stability | High |

### 5 Smart Interview Questions

1. How does the team protect focus time given the intensity of public product launches?
2. What is the average tenure on this team, and what causes most departures?
3. How is safety and alignment review integrated into day-to-day engineering work?
4. Can you explain how the profit-participation equity units are structured and when they vest?
5. What does work-life balance look like on weeks with major model releases?

---

## Report 3 — Amazon

**Risk Score: 55 / 100 | ⚠️ Apply with Caution**

### Top Red Flags

| Flag | Severity |
|------|---------|
| 5-day RTO mandate — older "flexible remote" JDs are now misleading | 8/10 |
| Stack ranking and PIP culture — well-documented, creates anxiety | 8/10 |
| Unclear on-call scope — "you build it, you run it" rarely disclosed at interview | 7/10 |
| Salary opacity — most JDs list no salary; RSUs are back-weighted | 6/10 |

### Positive Signals

- AWS AI infrastructure scale is genuinely unmatched globally
- Strong internal mobility across orgs and teams
- Leadership Principles create a clear, learnable evaluation framework

### Risk Breakdown

| Category | Risk Level |
|----------|-----------|
| Requirements | Moderate |
| Culture | Very High |
| Remote Authenticity | Very High |
| Hiring Process | High |
| Company Stability | Low |

### 5 Smart Interview Questions

1. What is the current in-office expectation for this specific team and location?
2. What does the on-call rotation look like, and how many incidents does the team handle monthly?
3. How does the team use performance improvement plans, and what is the typical path out of one?
4. Can you walk me through the RSU vesting schedule and how compensation is benchmarked annually?
5. How does responsible AI deployment fit into the engineering workflow on this team?

---

## Report 4 — IBM

**Risk Score: 62 / 100 | ❌ Avoid (unless enterprise consulting is your goal)**

### Top Red Flags

| Flag | Severity |
|------|---------|
| Ongoing layoffs — 3,900+ cut in 2024, roles replaced by AI automation | 9/10 |
| Skill list inflation — 10+ tools listed for one role (Watson, COBOL, Python, cloud) | 8/10 |
| Hidden consulting delivery pressure — AI roles are often billable client projects | 7/10 |
| Legacy-heavy environment — mainframe work bundled into "AI" titles | 6/10 |

### Positive Signals

- WatsonX platform growing in enterprise market
- Strong benefits, pension scheme, and global mobility options
- Good entry point for enterprise AI consulting career track

### Risk Breakdown

| Category | Risk Level |
|----------|-----------|
| Requirements | Very High |
| Culture | High |
| Remote Authenticity | Moderate |
| Hiring Process | Moderate |
| Company Stability | Very High |

### 5 Smart Interview Questions

1. Is this role internal product work or client-billable delivery — and what is the expected travel percentage?
2. How is this team protected from the ongoing workforce restructuring programmes?
3. What percentage of the day-to-day work involves modern AI stacks versus legacy IBM systems?
4. What does the career progression path look like for an AI engineer here over 3 years?
5. How does IBM ensure engineers stay technically current given the pace of change in the field?

---

## Report 5 — Accenture

**Risk Score: 50 / 100 | ⚠️ Apply with Caution**

### Top Red Flags

| Flag | Severity |
|------|---------|
| Hidden travel demands — "AI Engineer" often means Mon–Fri at client site | 8/10 |
| Impossible skill breadth — all cloud providers + ML frameworks + domain expertise | 7/10 |
| Revenue-first culture — growth tied to billability; learning time competes with delivery | 6/10 |
| Relocation risk — project assignments can shift you to different cities with little notice | 5/10 |

### Positive Signals

- Broad cross-industry exposure — healthcare, finance, retail AI
- Access to proprietary AI tools and Accenture AI Labs
- Strong certification budget — Microsoft, AWS, Google
- Huge alumni network with strong consulting exit opportunities

### Risk Breakdown

| Category | Risk Level |
|----------|-----------|
| Requirements | High |
| Culture | Moderate |
| Remote Authenticity | Very High |
| Hiring Process | Low |
| Company Stability | Low |

### 5 Smart Interview Questions

1. What percentage of time will I spend at client sites versus home or Accenture offices?
2. How much dedicated learning time is protected from client delivery each month?
3. Will I be staffed on one long-term engagement or rotated across projects?
4. What AI tools and proprietary platforms will I actually use day to day?
5. How does Accenture differentiate AI engineering roles from general data or cloud consulting?

---

## Report 6 — Deloitte

**Risk Score: 52 / 100 | ⚠️ Apply with Caution**

### Top Red Flags

| Flag | Severity |
|------|---------|
| Consulting grind culture — "client-first" language; 50–60 hr weeks common | 8/10 |
| AI title washing — many "AI Engineer" JDs are rebranded Power BI or data analyst roles | 7/10 |
| Compensation opacity — salary rarely disclosed; bonus tied to utilisation rate | 6/10 |
| Slow hierarchy-based progression — AI specialisation paths are unclear | 5/10 |

### Positive Signals

- Deloitte AI Institute — genuine research investment and thought leadership
- Excellent training budget; cloud and ML certifications strongly encouraged
- Global secondment opportunities across the Deloitte network
- Structured mentoring and strong graduate pipeline

### Risk Breakdown

| Category | Risk Level |
|----------|-----------|
| Requirements | Moderate |
| Culture | High |
| Remote Authenticity | High |
| Hiring Process | Low |
| Company Stability | Low |

### 5 Smart Interview Questions

1. What does a typical week look like — hours, location, and team structure on a live engagement?
2. How is the AI Engineer role differentiated from data engineering or analytics consulting?
3. What tools is the team actually deploying — LLMs, RAG pipelines, fine-tuning, or primarily BI?
4. How is utilisation rate calculated, and does it affect performance review or bonus?
5. What career path does someone in this role typically follow over 2–3 years?

---

## Interactive Report

A fully interactive HTML report with score rings, risk bar charts, and tabbed company navigation is available here:

👉 [View Full Interactive Report](./day14.html)

---

## Key Learnings

1. **IBM is the highest risk** (62/100) due to ongoing structural layoffs and extreme skill inflation in JDs — AI roles are often legacy consulting in disguise.

2. **Consulting firms (Accenture, Deloitte) hide travel demands** — "remote" or "hybrid" claims in JDs often mean full-time client site work. Remote authenticity is their biggest red flag category.

3. **Amazon's 5-day RTO** makes any flexible remote claim in older JDs actively misleading — always verify the current policy directly.

4. **OpenAI has the strongest culture risk** — hustle-culture language, rapid org changes, and complex equity structures make it high risk despite the brand appeal.

5. **Google is the safest pick** (32/100) but the hiring loop (5–7 rounds, 3–4 months) and extreme requirement inflation make entry very difficult.

6. **Smart interview questions are the most powerful tool** — they surface what JDs hide: on-call expectations, actual travel %, equity structure, and whether the "AI" title is real.

7. **No company scored below 30** — every major tech and consulting employer has at least moderate red flags for AI Engineer roles. Informed application beats blind applying.

8. **AI title washing is real** — especially at IBM and Deloitte, where "AI Engineer" often means rebranded data analyst or legacy systems work with AI buzzwords added.

---

## Process Followed

1. Read the provided resources and challenge brief
2. Set Claude effort level to Low
3. Gathered AI Engineer as the target job description
4. Selected 6 companies: Google, OpenAI, Amazon, IBM, Accenture, Deloitte
5. Applied the Red Flag Detector prompt template for each company
6. Generated risk scores, red flags, positive signals, risk breakdowns, verdicts, and interview questions
7. Built an interactive HTML report (`day14.html`) with tabbed navigation and score ring visualizations
8. Documented findings in this `day14.md` file
9. Committed both files to the `Day14/` folder in the GitHub repository

---

*Day 14 of 30 · 30 Days of AI Challenge · Role: AI Engineer · Companies: Google · OpenAI · Amazon · IBM · Accenture · Deloitte*