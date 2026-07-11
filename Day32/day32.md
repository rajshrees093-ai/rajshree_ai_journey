# Day 32 — Think Like a Marketing Strategist

## What I built
A single-file, offline HTML/React app called **"Think Like a Marketing Strategist: Grow This Brand."** It's an interactive simulator that walks through how a marketing strategist actually thinks — not just content generation.

The flow:
1. Choose a brand type: 🏢 Business, 🙋 Personal Brand, or 🎲 Random Client
2. Understand the target audience (and, for personal brands, "people you admire" instead of competitors)
3. Select marketing platforms, with explanations of why each is a strong, situational, or weak fit
4. Choose exactly 3 content pillars out of a larger set, each tagged with the goal it supports
5. Generate a 30-day roadmap organized by weekly strategic goals, not individual posts
6. Respond to a randomized "curveball" marketing event and see the consequence of the choice
7. Review a final Growth Report: audience understanding, platform strategy, content strategy, growth potential, best decision, biggest mistake, and three marketing lessons

Every section includes a "How to ask Claude" prompt card with a reusable, pre-filled prompt so the tool doubles as a prompt-engineering lesson.

**Tech constraints followed:** single HTML file, React via CDN + Babel JSX, no Tailwind/npm/backend/APIs, works offline once loaded, responsive, dark modern UI, fully replayable with randomized businesses.

## How to run it
Open `think-like-a-marketing-strategist.html` in any browser. It loads React, ReactDOM, and Babel from `cdnjs.cloudflare.com` the first time (needs an internet connection for that one-time load); after that, all logic runs locally in the browser with no server or API calls.

## Key learnings
- **Audience before platform.** Choosing a platform before understanding who you're actually speaking to is choosing blind — fit follows understanding, not the other way around.
- **Fewer, sharper pillars beat many inconsistent ones.** Forcing a choice of exactly three content pillars makes a brand's message recognizable instead of scattered.
- **A strategy needs a plan for the unexpected.** A plan that only works when nothing goes wrong isn't a strategy — building in how you'll *respond* matters as much as what you'll post.
- **For personal brands specifically:** authenticity, consistency, and niche clarity are the compounding levers — a personal brand can't outsource its story, and trying to appeal to everyone quietly makes you memorable to no one.

## Screenshots
_Add screenshots here from your own run-through, e.g.:_
- `screenshot-welcome.png` — Welcome screen
- `screenshot-audience.png` — Audience understanding
- `screenshot-platforms.png` — Platform selection with fit explanations
- `screenshot-pillars.png` — Content pillar selection
- `screenshot-roadmap.png` — 30-day roadmap
- `screenshot-event.png` — Randomized marketing event + response
- `screenshot-report.png` — Final Growth Report

## Files in this folder
- `think-like-a-marketing-strategist.html` — the complete app
- `day32.md` — this file
- screenshots (add your own)