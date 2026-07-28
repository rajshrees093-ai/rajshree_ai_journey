# Day 49 — Build Personal AI Playbook: Submission Guide

This file has two parts:
1. **Terminal commands** to create the folder, add your files, and push to GitHub.
2. **A ready-to-fill `day49.md` template** to paste into your repo.

---


## `day49.md` template

Paste this into `Day49/day49.md` and fill in the bracketed parts.

```markdown
# Day 49 — Personal AI Playbook

## What I built
A personalized Personal AI Playbook web app focused on my actual AI habits:
personalizing outreach/pitch emails at scale while staying consistent with my
own tone and voice.

## My profile (from the interview)
- Role: Marketing / Content / Copywriting
- Primary use case: Email, outreach & client communication
- Biggest time sink: personalizing the same pitch for different people
- Biggest bottleneck: getting the tone/voice right consistently
- Model used: Claude
- Experience level: Beginner
- Desired outcome: sound more consistent & on-brand

## Workflow categories generated
1. Personalized Outreach — cold pitch personalizer, warm intro, social DM opener
2. Voice & Tone Consistency — Voice Profile Builder, Tone Consistency Check, Rewrite in My Voice
3. Follow-Ups & Re-engagement — cold lead follow-up, meeting recap, dormant client re-engagement
4. Client Communication — thread summarizer, status update, pushback response

## Files in this folder
- `personal-ai-playbook.html` — the full generated app (open directly in a browser)
- `personal-ai-playbook-backup.json` — exported workflow library backup
- `screenshots/` — screenshots of the Dashboard, Workflow Library, Prompt Builder,
  and Loop Builder in use

## What I did with the app
- [ ] Explored the personalized workflow library
- [ ] Assembled a prompt block-by-block in the Prompt Builder
- [ ] Converted a prompt into an autonomous loop in the Loop Builder
- [ ] Saved, favorited, and searched my own workflows
- [ ] Exported my workflow library as a backup file

## Key learnings
- [What surprised you about seeing your own AI habits laid out as a system?]
- [Which workflow do you think you'll actually reuse, and why?]
- [What did building the Voice Profile once change about how you'd prompt going forward?]
- [Anything about the Prompt Builder / Loop Builder blocks that changed how you think about prompting?]

## Screenshot links
| Screenshot | Description |
|---|---|
| screenshots/01-dashboard.png | Dashboard with personalized categories |
| screenshots/02-workflow-library.png | Workflow Library, filtered/searched |
| screenshots/03-prompt-builder.png | Prompt assembled block-by-block |
| screenshots/04-loop-builder.png | Prompt converted into an autonomous loop |
```

---

## Notes

- The HTML file is fully self-contained (no external libraries, no internet
  connection required) — you can open it directly by double-clicking it, or
  via `File → Open` in your browser.
- Your workflow data is stored in that browser's local storage. Use the
  **Backup & Export** tab inside the app *before* clearing browser data or
  switching browsers/machines, and commit that exported `.json` alongside the
  HTML file so your work isn't lost.