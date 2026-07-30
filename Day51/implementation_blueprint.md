# Implementation Blueprint — Days 2 to 10
## FocusFlow — AI-Powered Task Prioritization & Daily Planning Assistant

**Purpose:** This document is the single source of truth for building FocusFlow across the remaining 9 days of the capstone. Each day is self-contained enough that a fresh AI conversation can pick up exactly where the previous day left off without re-planning or re-architecting.

**Project recap:** A single-user web app where users type tasks in natural language, Claude parses/prioritizes them via the Claude API, and generates an ordered daily plan. No auth, no calendar sync, no notifications in v1.0. Full scope details are in the PRD.

---

## Day 2 — Tech Stack Selection, Architecture & Project Setup

### 🎯 Objective
Lock in the tech stack, define the system architecture, and get a working scaffolded project running locally with version control initialized.

### 📖 What I'll learn
- How to choose a pragmatic stack for a 10-day AI-powered project
- Basic full-stack project architecture (frontend/backend/API layer)
- Environment variable management for API keys

### 🛠 Features to build
- Empty but running project scaffold (frontend + backend)
- Environment configuration for the Claude API key
- Basic "Hello World" API route proving frontend-backend-Claude connectivity

### 📝 Step-by-step implementation plan
1. Choose stack: **React (Vite) frontend + Node.js/Express backend**, using the Claude API via a server-side route (never call the API directly from the browser — this protects the API key).
2. Initialize a monorepo-style structure with `/client` and `/server` folders.
3. Scaffold the React app with Vite; scaffold the Express server.
4. Set up `.env` for the Claude API key on the server side only; add `.env` to `.gitignore`.
5. Create one test API route (`POST /api/ping`) that calls Claude with a trivial prompt and returns the response, to confirm the full chain works end-to-end.
6. Initialize Git repo (if not already part of the challenge repo), commit the scaffold.
7. Set up basic README with run instructions.

### 📂 Files and folders to create or modify
```
/focusflow
  /client          (React + Vite app)
  /server
    /routes
      ping.js
    index.js       (Express entry point)
    .env           (not committed)
    .env.example   (committed, shows required var names)
  .gitignore
  README.md
```

### 🔗 APIs, libraries, services, or tools to integrate
- `@anthropic-ai/sdk` (Node) for server-side Claude API calls
- Express.js for the backend
- Vite + React for the frontend
- `dotenv` for environment variable loading

### 🧪 Testing tasks
- Confirm `npm run dev` starts both client and server without errors
- Confirm `/api/ping` returns a real Claude response in the terminal/Postman

### 🐞 Common issues and debugging tips
- **CORS errors**: enable `cors` middleware on Express during local dev.
- **API key not found**: confirm `.env` is in `/server` and loaded via `dotenv.config()` before any route uses it.
- **Port conflicts**: default client to `5173`, server to `3001`; document in README.

### ✅ End-of-day checklist
- [ ] Client and server both run locally
- [ ] `/api/ping` successfully returns a Claude response
- [ ] `.env` is gitignored; `.env.example` is committed
- [ ] Initial commit pushed

### 📸 Expected project state and screenshots to capture
- Terminal showing both servers running
- Browser/Postman screenshot of a successful `/api/ping` response
- Folder structure in your code editor

### ➡️ Handoff notes for Day 3
Stack is locked: React + Vite (frontend), Node/Express (backend), Claude API via `@anthropic-ai/sdk` server-side. Project runs locally on ports 5173 (client) / 3001 (server). Next: build the core task data model and CRUD API.

---

## Day 3 — Data Model & Backend Core (Task CRUD API)

### 🎯 Objective
Build the backend data model for tasks and full CRUD API endpoints, with in-memory or lightweight file-based storage for v1.0 simplicity.

### 📖 What I'll learn
- REST API design basics
- Structuring a simple backend data model without a full database
- Request validation basics

### 🛠 Features to build
- Task data model (id, title, category, urgency, estimatedTime, completed, createdAt)
- REST endpoints: create, read (all), update, delete task
- Basic in-memory (or JSON-file-backed) storage layer

### 📝 Step-by-step implementation plan
1. Define the `Task` schema/shape used across the app.
2. Build a storage module (`/server/store/taskStore.js`) using a simple JSON file or in-memory array (no database needed for v1.0 — keep it simple, this is a single-user app).
3. Implement REST routes:
   - `POST /api/tasks` — create a task
   - `GET /api/tasks` — list all tasks
   - `PATCH /api/tasks/:id` — update a task (e.g., mark complete)
   - `DELETE /api/tasks/:id` — delete a task
4. Add basic request validation (reject empty titles, malformed payloads).
5. Test every endpoint manually with Postman or curl.

### 📂 Files and folders to create or modify
```
/server
  /store
    taskStore.js
    tasks.json          (if file-backed storage)
  /routes
    tasks.js
  index.js               (register /api/tasks routes)
```

### 🔗 APIs, libraries, services, or tools to integrate
- None new — pure Express + Node fs (if file-backed) or in-memory array

### 🧪 Testing tasks
- Create a task via POST, confirm it appears in GET
- Update a task's `completed` field via PATCH
- Delete a task via DELETE, confirm it's gone
- Test validation: empty title should be rejected with a clear error

### 🐞 Common issues and debugging tips
- **Data resets on server restart** if using in-memory storage only — this is acceptable for v1.0, but note it; switch to file-backed JSON if persistence across restarts matters for your demo.
- **Race conditions with file writes**: keep writes synchronous and simple since this is single-user, low-traffic.

### ✅ End-of-day checklist
- [ ] All four CRUD endpoints work and are tested
- [ ] Validation rejects malformed input
- [ ] Storage persists tasks during a session
- [ ] Commit pushed with working backend

### 📸 Expected project state and screenshots to capture
- Postman/curl screenshots for each of the 4 endpoints working
- `tasks.json` (if used) showing stored data

### ➡️ Handoff notes for Day 4
Backend CRUD API is complete at `/api/tasks` (GET, POST, PATCH, DELETE). Task shape: `{ id, title, category, urgency, estimatedTime, completed, createdAt }`. Next: integrate Claude API to parse natural-language input into this task shape.

---

## Day 4 — AI Integration: Natural Language Task Parsing

### 🎯 Objective
Build the core AI feature: send free-text task input to Claude and receive back structured, parsed tasks matching the data model from Day 3.

### 📖 What I'll learn
- Prompt engineering for structured JSON output
- Server-side AI integration patterns
- Handling and validating AI-generated structured data

### 🛠 Features to build
- `POST /api/parse-tasks` endpoint: accepts free text, returns structured task array
- Claude prompt that reliably extracts title/category/urgency/estimatedTime from messy text
- Basic validation/sanitization of the AI's JSON response before it touches the task store

### 📝 Step-by-step implementation plan
1. Design the parsing prompt: instruct Claude to return **only valid JSON**, an array of task objects matching the schema, inferring category (Work/Personal/Health/Errands/Other) and urgency (High/Medium/Low) from context and any deadline language.
2. Build `/server/routes/parseTasks.js` with a `POST /api/parse-tasks` route that takes `{ text: string }` and calls Claude.
3. Parse the Claude response as JSON; if parsing fails, retry once with a stricter prompt reminder, then fall back to an error response.
4. Return the structured array to the client (do not auto-save yet — Day 5 UI will let the user review first, per PRD FR-3).
5. Test with varied messy inputs: multiple tasks in one sentence, vague deadlines ("sometime"), mixed categories.

### 📂 Files and folders to create or modify
```
/server
  /routes
    parseTasks.js
  /lib
    claudeClient.js     (shared Anthropic SDK client instance)
    prompts.js           (parsing prompt template)
```

### 🔗 APIs, libraries, services, or tools to integrate
- `@anthropic-ai/sdk` — model call for parsing
- Recommended model: fast, cost-efficient model suitable for structured extraction (verify current model options/pricing via Claude API docs at build time)

### 🧪 Testing tasks
- Input: "finish report by Friday, call mom sometime, gym at 6am tomorrow, buy groceries" → confirm 4 distinct tasks returned with sensible categories/urgency
- Input: single vague task → confirm it still returns valid structured output
- Input: gibberish/empty string → confirm graceful error handling, not a crash

### 🐞 Common issues and debugging tips
- **Claude returns JSON wrapped in markdown code fences**: strip ```` ```json ```` fences before `JSON.parse()`.
- **Occasional malformed JSON**: implement a retry with an explicit "respond with ONLY valid JSON, no explanation" instruction.
- **Overly generic categories**: refine the prompt with explicit category examples if results are inconsistent.

### ✅ End-of-day checklist
- [ ] `/api/parse-tasks` reliably returns structured, valid JSON
- [ ] Tested against at least 3 varied inputs
- [ ] Error handling in place for malformed AI responses
- [ ] Commit pushed

### 📸 Expected project state and screenshots to capture
- Postman screenshot: messy text in → structured JSON tasks out
- Screenshot of an intentional edge case (vague/empty input) handled gracefully

### ➡️ Handoff notes for Day 5
`/api/parse-tasks` accepts `{ text }` and returns an array of structured task objects (not yet saved to the store). Next: build the frontend UI for input, review, and adding parsed tasks to the task list.

---

## Day 5 — Frontend UI: Task Input & Review

### 🎯 Objective
Build the primary user-facing input experience: a text box for free-text task entry and a review screen showing AI-parsed tasks before they're added.

### 📖 What I'll learn
- React component structure and state management basics
- Connecting a frontend to a custom backend API
- Building clean, functional forms and list UIs

### 🛠 Features to build
- Task input text area with submit button
- Loading state while AI parses
- Review list of parsed tasks (editable title, category, urgency before confirming)
- "Add to my tasks" action that POSTs each confirmed task to `/api/tasks`

### 📝 Step-by-step implementation plan
1. Build `<TaskInput />` component: textarea + submit button, calls `/api/parse-tasks`.
2. Show a loading spinner/state while awaiting the AI response.
3. Build `<ParsedTaskReview />` component: renders returned tasks as editable cards/rows.
4. Allow inline edits (title text, category dropdown, urgency dropdown) before confirming.
5. On "Confirm & Add," POST each task individually to `/api/tasks` (from Day 3's API).
6. On success, clear the input and show a success state.
7. Apply clean, intentional visual styling (per frontend-design principles — avoid a bare unstyled form).

### 📂 Files and folders to create or modify
```
/client/src
  /components
    TaskInput.jsx
    ParsedTaskReview.jsx
  /api
    client.js          (fetch wrapper for backend calls)
  App.jsx               (wire components together)
  App.css / index.css
```

### 🔗 APIs, libraries, services, or tools to integrate
- Existing backend endpoints only (`/api/parse-tasks`, `/api/tasks`)

### 🧪 Testing tasks
- Submit varied free text, confirm parsed review list renders correctly
- Edit a parsed task's category before confirming, verify the edit persists
- Confirm tasks and verify they appear via a subsequent `GET /api/tasks` call
- Test empty submission is blocked with a friendly message

### 🐞 Common issues and debugging tips
- **State not updating after async POSTs**: ensure task list state refreshes (re-fetch or optimistic update) after confirming tasks.
- **Layout breaking on long task titles**: use `text-overflow` / wrapping styles, test with a long input string.
- **Multiple rapid submits**: disable the submit button while a request is in flight.

### ✅ End-of-day checklist
- [ ] User can type free text and see parsed tasks returned
- [ ] User can edit parsed tasks before confirming
- [ ] Confirmed tasks are saved via the backend API
- [ ] UI has intentional styling, not default browser form look
- [ ] Commit pushed

### 📸 Expected project state and screenshots to capture
- Screenshot of the input screen
- Screenshot of the parsed-task review screen with edits
- Screenshot confirming tasks were saved (task list visible)

### ➡️ Handoff notes for Day 6
Input → AI parse → review → confirm → save flow is fully working end-to-end in the UI. Task list state lives in `App.jsx` (or lifted context if refactored). Next: build the "Today's Plan" AI-generated view and the main dashboard.

---

## Day 6 — Daily Planning View & Dashboard

### 🎯 Objective
Build the "Today's Plan" feature: send the current task list to Claude, receive back a prioritized daily plan with reasoning, and display it as the primary dashboard view.

### 📖 What I'll learn
- Designing a second, distinct AI prompt for a different purpose (planning vs. parsing)
- Building a dashboard-style primary UI view
- Displaying AI reasoning/explanations in a user-friendly way

### 🛠 Features to build
- `POST /api/generate-plan` endpoint: takes current incomplete tasks, returns an ordered plan with brief reasoning per task
- `<TodaysPlan />` dashboard component as the app's main/landing view
- Navigation between "Today's Plan" and "All Tasks" views

### 📝 Step-by-step implementation plan
1. Design the planning prompt: given the list of incomplete tasks (with category/urgency/estimatedTime), instruct Claude to return an ordered array with a one-sentence reasoning string per task (e.g., "Do this first — hard deadline today").
2. Build `/server/routes/generatePlan.js` with `POST /api/generate-plan`, reusing the shared Claude client from Day 4.
3. Build `<TodaysPlan />` on the frontend: fetches incomplete tasks, calls `/api/generate-plan`, renders the ordered list with reasoning text under each task.
4. Add simple top-level navigation/tabs: "Today's Plan" (default view) and "All Tasks."
5. Make this the new default landing view (replace or supplement Day 5's raw input as the app's home).

### 📂 Files and folders to create or modify
```
/server
  /routes
    generatePlan.js
  /lib
    prompts.js            (add planning prompt alongside parsing prompt)
/client/src
  /components
    TodaysPlan.jsx
    NavTabs.jsx
  App.jsx                 (add routing/tab state)
```

### 🔗 APIs, libraries, services, or tools to integrate
- Existing Claude client; no new external services

### 🧪 Testing tasks
- Generate a plan with 5+ mixed-urgency tasks, confirm sensible ordering
- Generate a plan with zero incomplete tasks, confirm a friendly "nothing to plan" state instead of an error
- Confirm reasoning text is concise and renders cleanly in the UI

### 🐞 Common issues and debugging tips
- **Plan ignores urgency/category context**: make sure the full task metadata (not just titles) is included in the prompt payload.
- **Reasoning text too long, breaking layout**: cap prompt instruction to "one short sentence" and truncate defensively in the UI as a backstop.
- **Empty task list edge case crashing the AI call**: short-circuit on the frontend/backend before calling Claude if there are no incomplete tasks.

### ✅ End-of-day checklist
- [ ] "Today's Plan" generates and displays a sensible ordered list with reasoning
- [ ] Empty-state handled gracefully
- [ ] Navigation between Today's Plan and All Tasks works
- [ ] Commit pushed

### 📸 Expected project state and screenshots to capture
- Screenshot of a generated Today's Plan with multiple tasks and reasoning
- Screenshot of the empty state ("no tasks" plan view)
- Screenshot of navigation between views

### ➡️ Handoff notes for Day 7
Core AI loop is complete: input → parse → review → save → generate plan → view. App now has two main views (Today's Plan, All Tasks). Next: add task completion interactions, streak tracking, and visual polish.

---

## Day 7 — Task Completion, Streaks & Visual Polish

### 🎯 Objective
Add the interactive completion flow, a simple progress/streak tracker, and a real visual design pass so the app looks like a finished product, not a prototype.

### 📖 What I'll learn
- Building satisfying micro-interactions (checkbox/complete states)
- Simple streak/progress logic
- Applying a cohesive visual design system (color, type, spacing)

### 🛠 Features to build
- Mark-complete interaction on both Today's Plan and All Tasks views
- Delete task interaction
- Streak counter (e.g., consecutive days with at least one task completed)
- Full visual design pass: consistent color palette, typography, spacing, empty/loading states

### 📝 Step-by-step implementation plan
1. Add complete/incomplete toggle UI (checkbox or button) wired to `PATCH /api/tasks/:id`.
2. Add delete action wired to `DELETE /api/tasks/:id`, with a confirmation step to prevent accidental deletion.
3. Implement streak logic: track `lastCompletionDate` and `streakCount` (simple server-side logic incrementing when a task is completed on a new calendar day, resetting if a day is missed).
4. Build a small `<StreakBadge />` component showing current streak on the dashboard.
5. Do a full design pass: pick a real color palette and type scale (not default browser styles), ensure consistent spacing, add subtle empty/loading states throughout, verify mobile responsiveness.

### 📂 Files and folders to create or modify
```
/server
  /store
    taskStore.js          (add streak tracking logic)
  /routes
    streak.js              (GET /api/streak)
/client/src
  /components
    StreakBadge.jsx
  App.css / theme.css      (design system pass)
```

### 🔗 APIs, libraries, services, or tools to integrate
- None new — refining existing stack

### 🧪 Testing tasks
- Complete a task, confirm it moves out of Today's Plan and streak updates
- Delete a task, confirm removal and confirmation prompt works
- Test streak logic across a simulated day change (manually adjust date logic if needed to verify)
- Resize browser to mobile width, confirm no layout breakage

### 🐞 Common issues and debugging tips
- **Streak logic off-by-one errors around date boundaries**: use consistent date-only comparisons (strip time component) to avoid timezone bugs.
- **Deleting a task breaks an in-progress plan view**: re-fetch or filter local state immediately after delete.
- **Inconsistent spacing/colors**: define a small set of CSS variables (palette + spacing scale) and reuse everywhere rather than one-off values.

### ✅ End-of-day checklist
- [ ] Complete/delete interactions work end-to-end
- [ ] Streak counter updates correctly
- [ ] App has a cohesive, intentional visual design
- [ ] Mobile responsiveness verified
- [ ] Commit pushed

### 📸 Expected project state and screenshots to capture
- Screenshot of completing a task (before/after state)
- Screenshot of the streak badge
- Screenshot of the app on a mobile viewport width

### ➡️ Handoff notes for Day 8
All core features are functionally complete: parse, review, save, plan, complete, delete, streak, and a real visual design. Next: dedicated testing pass and bug fixing before deployment.

---

## Day 8 — Testing & Bug Fixing

### 🎯 Objective
Systematically test the full application, fix bugs, and harden error handling before deployment.

### 📖 What I'll learn
- Manual QA and edge-case testing methodology
- Basic error boundary / defensive coding patterns
- How to prioritize bug fixes under a hard deadline

### 🛠 Features to build
- No new features — this is a stabilization day
- Error boundaries/fallback UI for unexpected failures
- A short internal test checklist covering the full user flow

### 📝 Step-by-step implementation plan
1. Write out a manual test checklist covering the entire user flow from Day 2–7 (input → parse → review → save → plan → complete → delete → streak).
2. Walk through every item on real and edge-case data (empty inputs, very long inputs, special characters, rapid clicking, network throttling).
3. Add a React error boundary around the main app to prevent a single component crash from white-screening the whole app.
4. Add user-facing error messages for all API failure points (parse failure, plan generation failure, save failure).
5. Fix all bugs found, re-test after each fix.
6. Do a final cross-browser check (Chrome + at least one other browser) if possible.

### 📂 Files and folders to create or modify
```
/client/src
  /components
    ErrorBoundary.jsx
  App.jsx                 (wrap main views in ErrorBoundary)
/docs
  test-checklist.md         (optional but recommended artifact)
```

### 🔗 APIs, libraries, services, or tools to integrate
- None new

### 🧪 Testing tasks
- Full end-to-end walkthrough at least twice
- Deliberately trigger API failures (e.g., temporarily use a bad API key) to confirm graceful error UI, then restore the key
- Test on a slow/throttled network (browser dev tools) to confirm loading states hold up
- Test rapid double-submits and rapid clicking on complete/delete

### 🐞 Common issues and debugging tips
- **Silent failures**: add console logging on the server for every caught error so issues are traceable, not invisible.
- **Error boundary swallowing useful info**: log the actual error object, not just a generic message, during development.
- **"Works on my machine" bugs**: test with a fresh browser profile / incognito window to rule out cached state issues.

### ✅ End-of-day checklist
- [ ] Full test checklist completed and passed
- [ ] Error boundary in place
- [ ] All known bugs fixed and re-tested
- [ ] App is stable under edge-case and failure conditions
- [ ] Commit pushed

### 📸 Expected project state and screenshots to capture
- Screenshot of the completed test checklist
- Screenshot of a graceful error state (intentionally triggered)
- Screenshot of the app functioning normally after fixes

### ➡️ Handoff notes for Day 9
App is functionally stable and tested. All known bugs are resolved. Next: deploy to a live, public URL.

---

## Day 9 — Deployment

### 🎯 Objective
Deploy FocusFlow to a live, publicly accessible URL with the backend securely configured (API key never exposed client-side).

### 📖 What I'll learn
- Deploying a full-stack app (separate frontend/backend deploy or combined)
- Managing environment variables/secrets in a hosting platform
- Basic production readiness checks

### 🛠 Features to build
- No new product features — deployment configuration only
- Production build of the frontend
- Backend deployed with environment-secured API key

### 📝 Step-by-step implementation plan
1. Choose free hosting: e.g., **Vercel** for frontend (React/Vite build) and **Render** or **Railway** (or Vercel serverless functions) for the backend — pick whichever keeps setup simplest given the Day 2 stack.
2. Create a production build of the client (`npm run build`) and verify it locally with a static preview.
3. Configure the backend for production: set `PORT` from environment, ensure CORS allows the deployed frontend's domain.
4. Add the Claude API key as a secret/environment variable directly in the hosting platform's dashboard — never commit it.
5. Deploy backend first, confirm its public API URL works (test `/api/tasks` via the live URL).
6. Point the frontend's API base URL to the deployed backend URL, rebuild, deploy frontend.
7. Do a full smoke test on the live deployed URL: complete the entire user flow end-to-end in production.

### 📂 Files and folders to create or modify
```
/client
  .env.production          (VITE_API_BASE_URL pointing to deployed backend)
/server
  (ensure PORT and CORS origin are environment-driven, not hardcoded)
README.md                   (add live URL + deployment notes)
```

### 🔗 APIs, libraries, services, or tools to integrate
- Vercel (or chosen frontend host)
- Render/Railway (or chosen backend host) — free tier only, per capstone rules

### 🧪 Testing tasks
- Full user flow test on the live production URL (not localhost)
- Confirm no console errors related to CORS or missing environment variables
- Confirm API key is not visible anywhere in browser dev tools/network tab

### 🐞 Common issues and debugging tips
- **CORS errors in production**: explicitly set the deployed frontend's exact URL as the allowed CORS origin on the backend, not `*`, for correctness.
- **Environment variable not picked up**: most platforms require a redeploy after adding/changing env vars — trigger a fresh deploy after setting them.
- **Backend free-tier cold starts**: some free hosts spin down idle services; note this in your demo notes so a first request delay isn't mistaken for a bug.

### ✅ End-of-day checklist
- [ ] Backend deployed and publicly reachable
- [ ] Frontend deployed and publicly reachable
- [ ] Full user flow works on the live URL
- [ ] No secrets exposed client-side
- [ ] Live URL documented in README
- [ ] Commit pushed

### 📸 Expected project state and screenshots to capture
- Screenshot of the live deployed app (with URL bar visible)
- Screenshot of a completed end-to-end flow on the live URL
- Screenshot of hosting dashboard showing successful deploy

### ➡️ Handoff notes for Day 10
App is live at a public URL with the full feature set working in production. Next: final polish, documentation, and demo/pitch preparation for capstone submission.

---

## Day 10 — Final Polish, Documentation & v1.0 Release

### 🎯 Objective
Apply final polish, complete project documentation, and formally close out v1.0 as a demo-ready, submission-ready product.

### 📖 What I'll learn
- Writing clear product documentation for an outside reader
- Preparing a project for demonstration/presentation
- Reflecting on and articulating what was built and learned

### 🛠 Features to build
- No new functional features — polish and documentation only
- Final UI polish pass (copy, spacing, empty states, favicon/branding touches)
- Complete README and project write-up

### 📝 Step-by-step implementation plan
1. Do a final walkthrough of the live app as a first-time user would experience it; fix any remaining rough edges (copy, spacing, obvious gaps).
2. Add small branding touches: app name/logo text, favicon, page title.
3. Write a complete README: what the app does, tech stack, how to run locally, live URL, screenshots.
4. Write a short project retrospective: what worked, what was challenging, what you'd build next (v2.0 ideas from the PRD's open questions).
5. Confirm the PRD, Implementation Blueprint, and Pitch Deck are all present in the repo alongside the code.
6. Do a final end-to-end demo run-through and capture final screenshots for submission.
7. Tag/mark this as the v1.0 release (e.g., a Git tag `v1.0` or a clear commit message).

### 📂 Files and folders to create or modify
```
README.md                    (final, complete version)
/docs
  retrospective.md
CHANGELOG.md (optional)
```

### 🔗 APIs, libraries, services, or tools to integrate
- None new

### 🧪 Testing tasks
- Full final smoke test of the live production app
- Proofread all user-facing copy for typos/clarity
- Verify all links in README (live URL, repo links) work

### 🐞 Common issues and debugging tips
- **Last-minute changes breaking production**: make final polish changes locally first, test thoroughly, then deploy — don't edit directly against a live/critical demo state without testing.
- **README out of sync with actual app behavior**: write the README last, after the app is finalized, not before.

### ✅ End-of-day checklist
- [ ] Final polish pass complete
- [ ] README complete with live URL and screenshots
- [ ] Retrospective written
- [ ] All three Day 1 deliverables (PRD, Blueprint, Pitch Deck) present in repo
- [ ] v1.0 tagged/marked as complete
- [ ] Final commit pushed

### 📸 Expected project state and screenshots to capture
- Screenshot of the final polished app (multiple views)
- Screenshot of the completed README
- Screenshot/confirmation of the v1.0 tag or final commit

### ➡️ Project complete
FocusFlow v1.0 is live, deployed, documented, and demo-ready — a complete 10-day journey from idea to shipped AI-powered product.

---
*End of Implementation Blueprint*