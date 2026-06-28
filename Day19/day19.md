# Day 19 — Football Intelligence Hub

> **ABTalks AI Challenge · Day 19**
> Build a Football Intelligence Hub using Claude + World Cup workbook data

---

## 🎯 Project Overview

This project transforms the ABTalks FIFA World Cup 2026 workbook into a fully interactive **Football Intelligence Experience** — combining AI-powered predictions, a live dashboard, and personalised personality assessments.

**Deliverables built:**
- Interactive Football Intelligence Hub (Claude-powered, 4-stage experience)
- PDF Portrait Dashboard (A4, dark-theme, player illustrations)
- Professional HTML Dashboard (full-featured, animated, responsive)
- This documentation file (`day19.md`)

---

---

## 🛠️ Tools & Stack

| Tool | Purpose |
|------|---------|
| Claude Sonnet 4.6 | AI analyst, quiz generator, personality assessor |
| Claude Artifacts | Interactive hub & HTML dashboard rendering |
| Python + ReportLab | PDF portrait dashboard generation |
| PIL / Pillow | Player portrait illustration creation |
| Google Fonts (Barlow Condensed + Inter) | Dashboard typography |
| ABTalks WC2026 Workbook | Primary data source |

---

## 🔁 Stage-by-Stage Experience

### Stage 0 — Knowledge Level Check

The experience opens with a knowledge calibration question:

> *"How familiar are you with football?"*

Options ranged from **"I know almost nothing"** to **"I actively follow football and major tournaments."**

Selected: **Football Follower** — adjusts terminology depth and example complexity throughout.

---

### Stage 1 — FIFA World Cup 2026 Prediction Report

Claude analysed historical performance data, current form scores, live 2026 results, and player ratings from the workbook to generate:

| Prediction | Team | Confidence | Key Evidence |
|-----------|------|-----------|-------------|
| 🏆 Winner | **Argentina** | 73% | FIFA #1, Form 92, 3–0 opener vs Algeria, Messi (Rating 96, 20G/12A) |
| 🥈 Runner-up | **France** | 61% | 2 back-to-back finals, Mbappé leads scorers (22G), Form 90 |
| 🌟 Dark Horse | **Morocco** | 38% | Best defensive record (6 GA), drew Brazil 1–1, FIFA #12 |

**Players to watch:**

| Player | Country | Goals | Assists | Rating |
|--------|---------|-------|---------|--------|
| Lionel Messi | Argentina | 20 | 12 | 96 |
| Kylian Mbappé | France | 22 | 8 | 95 |
| E. Haaland | Norway | 25 | 4 | 94 |
| C. Ronaldo | Portugal | 18 | 5 | 94 |
| J. Bellingham | England | 10 | 9 | 91 |

---

### Stage 2 — Football IQ Quiz

A 5-question multiple-choice quiz (mix of beginner, intermediate, and advanced):

| # | Level | Question | My Answer | Correct? |
|---|-------|----------|-----------|---------|
| 1 | Beginner | Players on a team? | 11 | ✅ |
| 2 | Beginner | Most World Cup wins? | Brazil | ✅ |
| 3 | Intermediate | 2022 Golden Ball winner? | Messi | ✅ |
| 4 | Intermediate | Germany 7-1 victim? | Brazil | ✅ |
| 5 | Advanced | Germany vs Curaçao 2026? | 7-1 | ✅ |

**Football Awareness Score: 100 / 100**
**Classification: ⚽ Football Expert**

---

### Stage 3 — Messi vs Ronaldo Personality Match

10-question personality assessment covering: Ambition, Creativity, Teamwork, Competitiveness, Discipline, Leadership, Risk-taking, Confidence, Work Ethic, and Learning Style.

**Results:**

| Legend | Compatibility |
|--------|-------------|
| 🐐 Lionel Messi | 58% |
| 💪 Cristiano Ronaldo | 42% |

**You resemble more: Lionel Messi**

> *Your instinctive creativity, collaborative spirit, and ability to elevate those around you echo Messi's game philosophy.*

**Personality Archetype: Creative Playmaker**

> Vision, flair, and genius in every touch. You see plays others miss. Traits: Visionary · Intuitive · Unpredictable

**Recommendations:**
- 👤 Player to follow: **Lionel Messi**
- 🏟️ Club to explore: **Inter Miami**
- 🌍 National team: **Argentina**
- ⚔️ Rivalry: **Messi vs Ronaldo GOAT debate**

---

### Final Output — Football Intelligence Profile

| Section | Result |
|---------|--------|
| 🏆 Predicted Winner | Argentina (73%) |
| 🥈 Runner-up | France (61%) |
| 🌟 Dark Horse | Morocco (38%) |
| 📊 Awareness Score | 100 / 100 |
| 🏷️ Fan Classification | Football Expert |
| 🐐 Messi Match | 58% |
| 💪 Ronaldo Match | 42% |
| 🎭 Archetype | Creative Playmaker |
| ⭐ Recommended Player | Lionel Messi |
| 🏟️ Recommended Club | Inter Miami |

---

## 📊 Dashboards Built

### 1. Interactive Intelligence Hub (Claude Artifact)

A 4-stage interactive Claude-powered app built directly in the artifact, featuring:
- Stage navigation with auto-progression
- Animated confidence bars
- Interactive quiz with scoring
- Personality matching algorithm
- Full Intelligence Profile generation

### 2. PDF Portrait Dashboard (`WC2026_Dashboard_Portrait.pdf`)

A4 dark-theme professional PDF featuring:
- Gold ticker-style header
- 5 KPI metric chips
- Player portrait cards with jersey-colour silhouettes and stats
- 3-way prediction panel with confidence bars
- Contender form score chart (7 teams)
- Live group stage results grid (9 matches)
- Historical win rates (6 nations)
- Dark footer with attribution

### 3. HTML Dashboard (`wc2026_dashboard.html`)

Full-featured standalone HTML file featuring:
- Live scrolling gold ticker with tournament headlines
- Sticky header with live badge and pulsing dot
- 5 KPI cells with hover accent animations
- Player cards — jersey SVG silhouettes, stat pills, WC goal dots, rating bars
- **Clickable player cards → modal popup** with full attributes (Pace, Dribbling, Passing, Shooting, Vision, Leadership)
- Prediction cards with gradient accents and risk notes
- Animated contender form chart
- Match results grid (colour-coded: green = win, purple = draw)
- Group A standings table
- Historical win rate bars
- Scroll-triggered reveal animations on all sections

**Typography:** Barlow Condensed (display) + Inter (body) + JetBrains Mono (data)
**Palette:** Deep navy `#080E17` · Electric blue `#0A84FF` · Gold `#F5C400` · Emerald `#00C97A` · Crimson `#FF3B5C`

---

## 💡 Key Learnings

1. **Prompt engineering matters** — the 3-stage prompt design with a knowledge-level check before scoring was key to making the experience feel personalised rather than generic.

2. **Data-driven storytelling** — grounding every prediction in workbook statistics (form scores, historical win %, FIFA rankings, live match results) made outputs feel credible and evidence-based.

3. **Claude in artifacts** — Claude can run multi-turn interactive experiences entirely within an artifact, handling state, scoring, and branching logic without a backend.

4. **Design intentionality** — using Barlow Condensed for the "jersey number energy" feel and a stadium-dark colour palette gave the HTML dashboard a broadcast-quality aesthetic rooted in the subject matter.

5. **Layer your outputs** — delivering the same data across three formats (interactive hub, PDF, HTML) demonstrates how a single data source can serve very different use cases (exploration, print, web).

---

## 🔗 Resources

- [ABTalks AI Challenge](https://abtalks.com)
- [Claude.ai](https://claude.ai)
- [FIFA World Cup 2026](https://www.fifa.com/en/tournaments/mens/worldcup/canadamexicousa2026)
- [Anthropic Prompt Engineering Guide](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview)

---

*Generated with Claude Sonnet 4.6 · June 2026 · ABTalks Day 19*