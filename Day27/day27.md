# Day 27 — Prior Authorization Story Simulator

## What I Built
A single-file HTML application (HTML + Tailwind CSS via CDN + vanilla
JavaScript) that teaches the Prior Authorization (PA) workflow through an
8-chapter interactive story rather than a drag-and-drop board.

The chat feed is **append-only**: every new line is created with
`document.createElement` and added with `appendChild`. `innerHTML` is never
assigned on the chat container — it's only used once, to clear the small
progress-bar chrome, which is explicitly outside the chat feed.

### Design pass
The UI was refined into a more polished, editorial "clinical education"
look rather than a generic chat template:
- Deep navy header with a gradient brand mark, an eyebrow-style current
  chapter label, and a dot-and-line progress tracker (instead of plain
  bars) that fills in teal as chapters complete
- Circular avatars next to every bubble (Rahul in slate, Priya in teal)
  with small-caps name labels above each message
- Refined color system — navy for structure, teal for the guide character
  and primary actions, soft slate background for the feed so bubbles have
  contrast — with a muted blue tone reserved for the player's own choice
  echoes
- Subtle bubble entrance animation, hover states on choice buttons, and a
  persistent footer disclaimer clarifying StarCare Health is a fictional,
  illustrative payer

## Characters
- 👦 **Rahul** — the patient, appears in bubbles on the left
- 👧 **Priya** — a healthcare operations specialist, appears in bubbles on
  the right, and acts as the guide who explains each stage in plain language
- **Narrator** and **Dr. Patel** appear only as centered italic text, never
  as chat bubbles, to visually separate scene-setting/clinical dialogue from
  the two main conversational characters

## The 8 Chapters
1. **Doctor Visit** — Dr. Patel diagnoses Rheumatoid Arthritis and prescribes
   Humira at City Medical Center
2. **Insurance Roadblock** — Provider submits the PA directly to StarCare
   Health (used throughout as an illustrative example payer); flow shown as
   Provider → PA Request → Payer, with no pharmacy involvement at this stage
3. **What is PA?** — Priya explains step therapy and cites the AMA 2023 PA
   Survey finding that PA causes treatment delays in the majority of cases,
   and why that matters more for aggressive diagnoses
4. **Insurance Review** — Priya walks through the four things StarCare Health
   checks: eligibility, clinical documentation, ICD-10 diagnosis match, and
   step therapy history, explaining why each one matters
5. **Denial** — The PA is denied for missing step therapy documentation;
   Priya reassures that denial isn't permanent and shares the system-side
   cost (2+ staff hours per denial to resolve)
6. **Appeal** — Gathering supporting documents, drafting a Letter of Medical
   Necessity, and formally filing the appeal
7. **Approval** — PA approved, saved on file permanently, reference number
   issued, no repeat PA needed for future Humira refills
8. **Takeaways** — Two closing perspectives: what Rahul (the patient)
   learned, and how health systems track denial rate, appeal rate, and
   resolution time on the system side

Every chapter (except the final takeaways) ends with **two dialogue
choices** that change what Rahul asks next and Priya's response, while the
underlying story always converges back to the same 8-chapter arc. A
progress bar across the header fills in as each chapter is completed.

## What I Learned
- **PA delays are a clinical issue, not just an administrative one.** For
  aggressive diagnoses, the time lost to review cycles can affect disease
  progression — this reframes "paperwork" as something with real patient
  impact.
- **Denials are usually about missing information, not ineligibility.**
  Rahul's case was denied purely for missing step therapy documentation —
  a fixable, procedural gap, not a coverage exclusion.
- **The appeal path has real structure**: supporting documentation, a
  formal Letter of Medical Necessity, and a resubmission — each step
  exists because the original submission didn't fully answer the payer's
  criteria.
- **Systems measure this at scale.** Denial rate, appeal rate, and
  resolution time are the metrics health organizations track to know
  whether their PA process is working — turning individual frustration
  (like Rahul's) into an operational signal that can be improved.
- **Building append-only chat UIs** reinforced a clean separation of
  concerns: the chat feed only ever grows (via `createElement`/`appendChild`),
  while the footer "controls" area is the one region that's allowed to be
  rebuilt on every state change.

## Files in This Folder
- `prior-auth-story-simulator.html` — the complete, runnable story simulator
- `screenshots/` — key scenes (doctor visit, denial, appeal, approval,
  takeaways)
- `day27.md` — this file