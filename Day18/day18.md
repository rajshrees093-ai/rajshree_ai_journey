# Day 18 — Brain Dump Action Planner Skill

## What I built

A custom Claude Skill called **brain-dump-action-planner** that transforms messy notes, meeting transcripts, voice memos, and brainstorming sessions into structured, interactive HTML dashboards — without inventing or assuming any missing information.

---

## Skill details

| Field | Value |
|---|---|
| Skill name | `brain-dump-action-planner` |
| Mode used | Transcript Mode |
| Output format | Self-contained interactive HTML artifact |
| Speakers | Raj, Ankit |
| Deadline identified | July 5 |
| Conflicts found | 2 |

---

## How the skill works

The skill takes raw, unstructured notes and produces a full dashboard with these sections:

1. **Summary** — Short overview of the meeting or brain dump
2. **Key Takeaways** — Structured highlights with color-coded cards
3. **Action Items** — Interactive table with task, owner, deadline, priority, and status
4. **Speaker Summary** — Per-speaker breakdown (Transcript Mode)
5. **Open Questions** — Unresolved topics marked with ❓
6. **Risks / Blockers** — Dependencies and concerns marked with ⚠️
7. **Conflicts** — Conflicting deadlines, owners, or decisions highlighted prominently
8. **Additional Notes** — Supporting context that doesn't fit elsewhere

### Status badges used
- 🔴 High Priority
- 🟠 Medium Priority
- ⚠️ Conflict
- ❓ Open Question
- ⏳ Pending

---

## Meeting notes used for testing

```
Raj:
Need landing page completed by July 5.

Ankit:
Backend API still pending.

Discussion:
Marketing campaign launch depends on landing page.

Action:
Raj to finish UI.
Ankit to finish APIs.

Concern:
API integration may delay launch.
```

---

## Dashboard output

The skill generated a dark-themed professional dashboard with:

- **Header** with participant count and deadline chips
- **Summary + Key Takeaways** in a two-column grid
- **Speaker cards** for Raj, Ankit, and Group
- **Action items table** with color-coded priority and status pills
- **Open questions** panel (3 questions extracted)
- **Risks/Blockers** panel with red border styling
- **Conflicts section** with amber border, dark background, and individual conflict cards — making scheduling gaps and circular dependencies immediately visible
- **Additional Notes** for context that didn't fit elsewhere

---

## Key learnings

- Claude Skills allow you to save complex prompt instructions once and reuse them across sessions without re-entering the setup
- The skill strictly avoids inventing information — missing fields display "Not specified" rather than guessed values
- Transcript Mode adds speaker-level attribution, making ownership of actions and decisions clear
- The conflict detection surfaced two issues from just six lines of notes: a missing API deadline vs. the July 5 cutoff, and a circular dependency between launch, landing page, and API
- The dashboard design (dark theme, colored borders, amber conflict cards) makes high-priority issues immediately visible without reading all text
- Interactive HTML artifacts can be saved as `.html` files and opened in any browser — no tool dependency required

---

## Files in this folder

| File | Description |
|---|---|
| `day18.md` | This file — summary, learnings, and documentation |
| `brain-dump-dashboard.html` | Full standalone dark dashboard generated from meeting notes |

---

## Steps followed

1. Read the skill prompt template (name, description, instructions)
2. Opened Claude and navigated to Skills → New Custom Skill
3. Set skill name as `brain-dump-action-planner`
4. Added the description and pasted the instructions
5. Saved the skill
6. Triggered it with `/brain-dump-action-planner` followed by meeting notes
7. Reviewed the generated dashboard sections
8. Iterated on the design — improved conflict visibility with dark amber styling
9. Exported the final HTML file
10. Created this `Day18/` folder and committed all outputs