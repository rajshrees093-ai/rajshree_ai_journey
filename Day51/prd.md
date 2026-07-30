# Product Requirements Document (PRD)
## FocusFlow — AI-Powered Task Prioritization & Daily Planning Assistant

**Version:** 1.0
**Date:** July 30, 2026
**Capstone Day:** Day 1 of 10 — AB Talks 60-Day Claude AI Challenge
**Status:** Approved for Implementation

---

## 1. Executive Summary

FocusFlow is a single-user, AI-powered productivity web application that eliminates the friction of task management. Users type their tasks in plain, messy, natural language — the way they'd actually think them — and Claude parses, categorizes, prioritizes, and organizes them into a clear, actionable daily plan. The product directly addresses decision fatigue: the mental cost of figuring out "what do I actually need to do today" before any real work begins.

## 2. Problem Statement

Most task management tools require users to manually structure their own thoughts — set priority levels, pick categories, estimate time, and reorder lists by hand. This structuring overhead is exactly the kind of low-value cognitive work people avoid, so tasks pile up unsorted or people abandon the tool entirely. The result is decision fatigue at the start of every day and a nagging sense of being behind.

**Core insight:** People are good at *describing* what they need to do in natural language. They are bad at, and dislike, *structuring* that list themselves. AI can bridge that gap.

## 3. Target Users

| Persona | Description | Key Need |
|---|---|---|
| **The Overwhelmed Multitasker** | Juggles work, personal errands, and commitments with no single organizing system | Wants one place to dump everything and get clarity fast |
| **The Chronic Procrastinator** | Knows what needs doing but struggles to know where to start | Wants the decision of "what's next" made for them |
| **The Efficiency Seeker** | Already uses to-do apps but is frustrated by manual tagging/sorting | Wants automation to remove busywork from planning |

## 4. Goals & Success Metrics

### Product Goals
- Reduce the time and mental effort required to go from "messy thoughts" to "clear daily plan" to under 30 seconds.
- Demonstrate a real, working, deployed integration of Claude's API solving an everyday problem.
- Ship a fully functional, polished v1.0 within the 10-day capstone window.

### Day 10 Success Criteria
- A live, publicly accessible deployed URL.
- A user can type an unstructured list of tasks in natural language and receive back an AI-organized, prioritized daily plan within seconds.
- Tasks can be marked complete and persist across a session.
- The app has no critical bugs, loads without errors, and looks intentionally designed (not a bare prototype).

## 5. Scope

### 5.1 In Scope (v1.0)
1. **Natural language task input** — free-text box where users type tasks in any format, mixed together.
2. **AI task parsing** — Claude API extracts individual tasks from free text, along with inferred deadlines, urgency, and category (e.g., Work, Personal, Health, Errands).
3. **AI-generated daily plan** — Claude organizes parsed tasks into a prioritized "Today's Plan," ordered by urgency/importance, with brief reasoning shown to the user.
4. **Task management** — mark tasks complete, delete tasks, view all tasks vs. today's plan.
5. **Progress tracking** — simple streak counter / completion stats to reinforce daily usage.
6. **Responsive web UI** — works cleanly on desktop and mobile browsers.
7. **Single-user session** — no login required for v1.0; data persists locally/in a lightweight backing store for the session or browser.

### 5.2 Explicitly Out of Scope (v1.0)
- Multi-user accounts, authentication, or user profiles.
- Calendar integrations (Google Calendar, Outlook, etc.).
- Native mobile apps (iOS/Android).
- Push notifications or reminders.
- Team/collaboration or task-sharing features.
- Recurring tasks / habit scheduling logic.
- Offline mode.

These are explicitly deferred to a post-capstone "v2.0" roadmap to protect the 10-day timeline.

## 6. Functional Requirements

| ID | Requirement | Priority |
|---|---|---|
| FR-1 | User can input free-text describing one or more tasks | Must |
| FR-2 | System sends input to Claude API and receives structured task data (title, category, urgency, estimated time) | Must |
| FR-3 | Parsed tasks are displayed in a reviewable list before being added to the plan | Must |
| FR-4 | User can request an AI-generated "Today's Plan" ordering tasks by priority | Must |
| FR-5 | User can mark a task complete | Must |
| FR-6 | User can delete a task | Must |
| FR-7 | System displays a simple completion streak/progress indicator | Should |
| FR-8 | System persists tasks across page reloads within a session | Should |
| FR-9 | UI is responsive across desktop and mobile viewport sizes | Must |
| FR-10 | System gracefully handles AI API errors (timeout, malformed response) with a user-facing fallback message | Must |

## 7. Non-Functional Requirements

- **Performance:** AI response for task parsing/plan generation should return within ~5 seconds under normal conditions.
- **Reliability:** No unhandled crashes; API failures degrade gracefully.
- **Security:** No API keys exposed client-side; secrets managed via environment variables.
- **Cost:** No paid tools/services required beyond the Claude API usage already part of the challenge.
- **Usability:** A first-time user should be able to use the core flow (type tasks → get plan) with zero instructions.
- **Deployability:** Must be deployable to a free hosting platform (e.g., Vercel/Netlify) with a public URL.

## 8. User Flow (v1.0)

1. User lands on FocusFlow homepage.
2. User types free-text tasks into an input box (e.g., "finish report by Friday, call mom sometime, gym at 6am tomorrow, buy groceries").
3. User submits — Claude parses this into discrete, categorized, prioritized tasks.
4. Parsed tasks appear in a review list; user can edit/confirm.
5. User clicks "Generate Today's Plan."
6. Claude returns an ordered daily plan with brief reasoning per task.
7. User works through the day, marking tasks complete.
8. Progress/streak indicator updates.

## 9. Risks & Mitigations

| Risk | Mitigation |
|---|---|
| AI misparses ambiguous input | Show parsed tasks for user review/edit before finalizing |
| API latency/downtime | Add loading states and graceful error handling |
| Scope creep during build | Blueprint enforces one feature set per day; excluded features documented and deferred |
| Tech stack decisions stall progress | Stack finalized early (Day 2) as a dedicated Setup phase |

## 10. Open Questions for Future Versions
- Should v2.0 support recurring tasks or habit tracking?
- Should calendar sync be the first post-v1.0 feature?
- Is multi-user support needed, or does this stay a personal tool?

---
*End of PRD — FocusFlow v1.0*