# Day 28 — Hospital Admission Readiness Simulator

**Category:** Healthcare Workflow Simulation
**Difficulty:** Intermediate
**Time Spent:** ~60 min
**Deliverable:** Single-file HTML app + this write-up

## What I Built

An interactive Hospital Admission Readiness Simulator where I play the role of a
Hospital Admission Coordinator. The app is a single self-contained HTML file
(Tailwind CSS via CDN + vanilla JavaScript, no backend) that walks a case from
intake through a final admit / not-ready decision.

**File:** `hospital-admission-readiness-simulator.html`

## Workflow Covered

1. **Setup / Intake** — Provider, Attending Physician, Diagnosis (Acute MI, CHF,
   Pneumonia, Elective Surgery, Hip Fracture), Admission Type (Inpatient,
   Observation, Emergency, ICU, Same-Day Surgery), Prior Authorization status,
   and Admission Date. All provider/physician names are labeled as illustrative
   training data.
2. **Initial Readiness Analysis** — generates status across PA, Insurance, Bed,
   Documentation, Physician Orders, and Consent, and produces an initial
   readiness score (30–60%) without revealing the final decision.
3. **Scoring Model** — weighted: PA 25% · Clinical Documentation 20% ·
   Physician Orders 20% · Insurance 15% · Consent 10% · Bed 10%. A hard rule
   caps readiness at 65% for a Denied PA + ICU admission, so admin tasks alone
   can't push it past the 70% mark.
4. **Prior Authorization Branches**
   - Approved → proceed directly.
   - Pending → Follow Up / Upload Docs / Contact Physician.
   - Denied → Review Reason / Contact Insurance / Submit Appeal (a successful
     appeal converts the case to Approved).
5. **Workflow Actions** — Assign Bed, Verify Insurance, Upload Documentation,
   Complete Consent, Contact Physician, Notify Nursing, Prepare Patient Arrival.
6. **Clinical Criteria Notes**
   - Acute MI / CHF trigger an InterQual/Milliman medical-necessity note.
   - Observation admissions always show the CMS 2-Midnight Rule / MOON
     notification notice.
7. **Timeline** — PA Review → Insurance Verification → Bed Assignment →
   Documentation → Consent → Patient Arrival → Registration → Clinical
   Assessment → Admission Complete.
8. **Care Coordination Cards** — Attending, Case Manager, Nursing, Utilization
   Review (explicitly names concurrent review, denial risk identification,
   InterQual, and Milliman), and Discharge Planner.
9. **Risk Tracking** — Documentation, Insurance, Bed, and Clinical Risk, with
   Clinical Risk weighted higher for Acute MI, CHF, and ICU cases.
10. **Governance Snapshot** — appears once readiness reaches 75%, showing
    illustrative industry benchmarks (PA turnaround, denial rate, PA rework
    cost).
11. **Final Decision**
    - ≥ 90% → ✅ Admit, with a full case summary.
    - < 90% → ⚠ Not Ready, listing missing items, required actions, and
      remaining risks.

## Scenarios Tested

- **Acute MI, ICU, PA Denied** — confirmed the readiness cap held below 70%
  until the appeal succeeded; clinical risk showed as elevated throughout.
- **CHF, Inpatient, PA Pending** — followed up and uploaded docs until PA
  converted to Approved, then cleared remaining admin tasks to reach Admit.
- **Elective Surgery, Same-Day Surgery, PA Approved** — fastest path to
  readiness since PA carried no risk; bottleneck was consent and bed
  assignment.
- **Pneumonia, Observation** — verified the CMS 2-Midnight Rule / MOON notice
  displayed correctly and stayed visible throughout the workflow.

## Key Learnings

- **Prior Authorization is the single highest-leverage lever** in the scoring
  model (25% weight) — a denial cascades through the whole readiness picture,
  especially combined with a high-acuity admission type like ICU.
- **Admin tasks can't fully substitute for clinical/payer resolution.** The
  Denied PA + ICU cap was a useful reminder that in real hospital operations,
  no amount of bed assignment or consent paperwork offsets an unresolved
  payer denial on a high-acuity case.
- **Observation status has real downstream billing consequences** (2-Midnight
  Rule, MOON notice) that are easy to overlook if you only think in terms of
  "admitted vs. not admitted."
- **Utilization Review's job is concrete and named**, not abstract: concurrent
  review and denial-risk identification against InterQual/Milliman criteria —
  building the UI card forced me to be specific about what that role actually
  checks.
- **Designing the readiness score as a weighted composite** (rather than a
  single number) made it much clearer which category to act on next, and
  mirrors how case managers likely triage real admission queues.

## Screenshots

_See attached screenshots in this folder:_


## Files in this folder

- `hospital-admission-readiness-simulator.html` — the generated simulator
- `day28.md` — this write-up
- screenshots (as listed above)