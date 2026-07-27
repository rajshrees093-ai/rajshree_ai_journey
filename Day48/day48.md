# Day 48 — The Verdict Engine

**Decision:** Which city should a remote tech worker relocate to — Lisbon, Valencia, Berlin, or Tbilisi?

**Deliverable:** `verdict-engine-relocation.html` — a single-file HTML/CSS/JS app with live-adjustable criteria weights, a sourced-evidence table, a sources/exhibits panel, and a "how this was researched" panel documenting methodology and source conflicts.

---

## 1. Interview Summary

| Question | Answer |
|---|---|
| Category | Relocation — which city to move to |
| User & goal | A remote tech worker deciding on cost-of-living + lifestyle balance |
| Options compared | Lisbon (Portugal), Valencia (Spain), Berlin (Germany), Tbilisi (Georgia) |
| Criteria | Cost of Living, Internet Speed/Reliability, Visa/Residency Ease, Climate & Quality of Life |
| Data sourcing | Claude-researched, real named sources (Numbeo, Speedtest/Ookla, immigration guides, meteorological normals) |
| Weighting | User-adjustable live sliders, not a fixed ranking |

## 2. Sourced Data Report

### Cost of Living (estimated total monthly cost, single remote worker, incl. rent)
| City | Estimate | Status | Basis |
|---|---|---|---|
| Tbilisi | ~$1,150/mo | Sourced | GREM 2026 expat guide ($900–$1,400/mo range, midpoint) |
| Valencia | ~$1,790/mo | **Derived estimate** | No single Numbeo total figure exists for Valencia; derived from a sourced relative comparison ("Berlin ~33% pricier than Valencia," Homevested 2026) applied to Berlin's sourced total |
| Lisbon | ~$2,280/mo | Sourced | Numbeo Portugal national average ($770 excl. rent) + average city-center 1BR rent (~€1,400) |
| Berlin | ~$2,439/mo | Sourced | Numbeo Germany national average ($1,142.5 excl. rent) + average Berlin 1BR rent (~€1,200, 2026) |

### Internet Speed (median fixed broadband, Ookla Speedtest Global Index)
| City/Country | Value | Status |
|---|---|---|
| Valencia / Spain | 248.12 Mbps, global rank #14 | **Sourced** — the only figure directly confirmed in research |
| Lisbon / Portugal | ~180 Mbps | **Estimate** — no precise current Ookla figure was verifiable |
| Berlin / Germany | ~150 Mbps | **Estimate** — same limitation |
| Tbilisi / Georgia | ~100 Mbps | **Estimate** — city-level figure from a secondary nomad-guide source, not the primary Ookla dataset |

### Visa / Residency Ease (composite 0–100 score)
| City/Country | Score | Basis |
|---|---|---|
| Tbilisi / Georgia | 95 | "Remotely From Georgia" — near-instant online processing after arrival; many nationalities also get a 1-year visa-free stay |
| Valencia / Spain | 75 | Digital Nomad Visa — ~€2,850/mo threshold, 20–45 day processing, 5-year stay, 15% flat tax option (Beckham Law) |
| Lisbon / Portugal | 55 | D8 Digital Nomad Visa — €3,680/mo threshold (highest of the four), 4–7 month processing |
| Berlin / Germany | 35 | No dedicated digital nomad visa — Freiberufler (freelance) permit only, more document-heavy |

### Climate & Quality of Life (30-year average annual sunshine hours)
| City | Hours/year | Status |
|---|---|---|
| Lisbon | 2,800 | Sourced |
| Valencia | 2,690 | Sourced (also ranked #1 in Numbeo's 2025 Southern Europe Quality of Life index) |
| Tbilisi | 2,045 | Sourced |
| Berlin | 1,718 | Sourced |

**Default (equal-weight) verdict:** Valencia ranks first, followed by Tbilisi, Lisbon, then Berlin — driven by Valencia's balance of strong sourced internet speed, the easiest EU visa pathway, high sunshine hours, and mid-range cost.

Full citation list (20 exhibits) is in the app's "Sources / Exhibits" panel.

## 3. Conflicts Resolved

1. **Tbilisi cost of living** varied 2–3x across sources ($814 budget baseline vs. $1,190–$1,904 "comfortable" range). Used the GREM 2026 mid-range figure as most representative of a comfortable (not bare-minimum) remote-worker lifestyle.
2. **Valencia's total cost** had no direct Numbeo figure comparable to the country-level Portugal/Germany numbers — derived via a sourced relative comparison instead of inventing a number, and flagged as a derived estimate.
3. **Portugal & Germany internet speed** — no exact, current, attributable Ookla figure could be confirmed for either country in this research. Rather than fabricate false precision, both are shown as flagged directional estimates.
4. **Germany's visa** — there is no dedicated digital nomad visa, so the freelance (Freiberufler) permit was used as the closest comparable pathway, and scored lower for being less standardized than the other three.

## 4. Key Learnings

- **Not all "index" data is directly comparable.** Numbeo publishes different figures at the city vs. country level; reconciling them into one comparable metric required an explicit, documented derivation rather than silently picking a number.
- **Absence of data is itself a data point.** Two of four internet-speed figures (Portugal, Germany) couldn't be pinned to an exact current Ookla number during research — flagging that honestly (rather than guessing with false confidence) was more valuable to the end user than a clean-looking but fabricated table.
- **Weighting reveals the "why" behind a ranking**, not just the "what." The equal-weight default favors Valencia, but a user who cares most about visa ease and cost would land on Tbilisi — the interactive sliders make that trade-off visible instead of hiding it behind a single static score.
- **A transparency panel is a trust feature, not an afterthought.** Separating "sourced" from "estimated" data, and documenting exactly which sources conflicted and how they were reconciled, is what turns a plausible-looking tool into a defensible one.

## 5. Files in this submission

- `verdict-engine-relocation.html` — the working single-file application
- `day48.md` — this report
- `screenshots/` — screenshots of the app in use (weights adjusted, sources panel, research panel)