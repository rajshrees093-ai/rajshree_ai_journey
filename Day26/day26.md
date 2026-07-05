# Day 26 — Prior Authorization Workflow Simulator

## What I Built
A single-file, self-contained HTML application (HTML + CSS + vanilla JavaScript,
no frameworks, no CDNs, no localStorage) that gamifies the US healthcare Prior
Authorization (PA) process as an interactive drag-and-drop simulation.

The simulator models three workflow lanes — **Patient**, **Provider**, and
**Payer** — and lets you drag a patient case through the real PA lifecycle:

1. Case Intake (Patient)
2. Medical Necessity Review (Provider)
3. Document Collection (Provider)
4. Submit to Payer (Provider)
5. Payer Review (Payer)
6. Decision — Approved / Pended / Denied (Payer)
7. Peer-to-Peer Review (Payer, if pended)
8. Appeal Submitted (Provider, if denied)
9. Patient Notified (Patient)

## Features Implemented
- 3 workflow lanes with drag-and-drop case movement, gated so a case can only
  move to a valid next stage (invalid drops shake and explain why)
- 4 patient scenarios stored in an editable array: elective knee surgery,
  lumbar spine MRI, specialty biologic medication, inpatient admission
- Medical necessity evaluation step tied to each scenario's clinical criteria
- Document collection checklist (different required docs per scenario)
- Submission to payer, with a review step that randomly resolves to
  Approval / Pend / Denial based on a per-scenario "payer difficulty"
- Pend → Peer-to-Peer Review branch; Denial → Appeal branch
- Educational explanation panel that updates after every action, describing
  what just happened in real-world PA terms
- Top progress tracker bar, days-elapsed counter, and efficiency score
  (penalized by pends, denials, peer-to-peer calls, and appeals)
- Confetti celebration animation on approval
- End-of-workflow summary modal with full case history, days elapsed,
  efficiency score, and whether peer-to-peer/appeal were used
- Working Restart / New Patient button that resets all in-memory state

## What I Learned
- **Sequence matters.** Real PA requests can't skip steps — necessity has to
  be established and documentation completed *before* submission, or the
  payer will bounce the request. Modeling this as gated drag targets made
  the "why" behind the paperwork burden concrete.
- **Pends and denials aren't dead ends — they're detours.** A pend usually
  means the payer needs more clinical context (resolved via Peer-to-Peer),
  while a denial has a formal appeal path with new evidence. Both add real
  time and cost, which is exactly why "efficiency score" drops when they
  happen.
- **Documentation completeness is the biggest lever.** Every scenario's
  required-document list ties directly into how likely the payer is to
  approve on first pass — mirroring how incomplete charts are the most
  common real-world cause of PA delay.
- **State management without persistence.** Keeping the entire workflow
  state in a single JS object (no localStorage) forced a clean separation
  between "what stage is the case in" and "what UI is rendered," which made
  the drag-and-drop validation logic much simpler to reason about.

## Files in This Folder
- `prior-auth-simulator.html` — the complete, runnable simulator
- `screenshots/` — gameplay screenshots (scenario picker, in-progress board,
  outcome screen, workflow summary)
- `day26.md` — this file