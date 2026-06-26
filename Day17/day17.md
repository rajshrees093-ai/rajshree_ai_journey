# Day 17 — AI Vehicle Cost & Fuel Analysis Dashboard

## 🚗 Vehicle Details
| Field | Value |
|---|---|
| Vehicle | Hyundai i20 |
| Fuel Type | Petrol (E20) |
| Usage Pattern | Mixed |
| Monthly Distance | 1,000 km/month |
| Car Age | 3 years |

---

## 📊 Dashboard Overview

Built a fully interactive HTML dashboard from a 52-record CSV dataset covering 5 fuel types: **Petrol (E20), E85 (Flex-Fuel), Diesel, CNG, and Electric (EV)**.

**Tech stack:** Pure HTML · CSS glassmorphism · Pure SVG charts · Vanilla JS — zero CDN dependencies.

---

## 🔢 Key Metrics (Computed from CSV)

### Cost per km by Fuel Type
| Fuel | Avg ₹/km | CO₂/km (kg) | Maint/km | Refuel Time |
|---|---|---|---|---|
| ⚡ EV | ₹1.75 | 0.091 | ₹0.23 | 45 min |
| 💨 CNG | ₹3.32 | 0.125 | ₹0.66 | 8 min |
| 🛢 Diesel | ₹4.67 | 0.179 | ₹1.00 | 5 min |
| ⛽ **Petrol ★ (mine)** | **₹6.15** | **0.171** | **₹0.47** | **5 min** |
| 🌽 E85 | ₹6.37 | 0.070 | ₹0.46 | 5 min |

### My Monthly Cost (1,000 km)
- **Petrol:** ₹6,154/month
- **E85:** ₹6,374/month (+₹220 more)

---

## ⚡ The E85 Paradox

| Metric | Value |
|---|---|
| Pump Price Saving | 18.0% (₹82 vs ₹100/L) |
| Running Cost Penalty | +3.57% per km |
| Break-even E85 Price | ₹79.11/L |
| Current E85 Price | ₹82.00/L |

**Verdict:** E85 is ₹18/L cheaper at the pump but delivers ~21% lower mileage (12.87 vs 16.27 km/L), meaning you actually pay *more* per km. E85 would only break even if priced at ≤ ₹79.11/L — it currently isn't.

---

## 🌡️ E85 Score: 5.71 / 10

| Dimension | Weight | E85 Score | Notes |
|---|---|---|---|
| Cost efficiency | 4 pts | 0.00 / 4 | Most expensive per km |
| CO₂ emissions | 3 pts | 3.00 / 3 | Best in class — 0.070 kg/km |
| Refuel time | 2 pts | 2.00 / 2 | Fast 5-min fill |
| Maintenance | 1 pt | 0.71 / 1 | Slightly better than Petrol |

---

## 📈 Age-based Cost Trend (Petrol)

| Age Bucket | Cost/km | Maint/km |
|---|---|---|
| New (0–2y) | ₹5.85 | ₹0.57 |
| **Mid-life (3–5y) ★ YOUR CAR** | **₹5.85** | **₹0.57** |
| Aged (6–9y) | ₹6.33 | ₹0.41 |

Petrol running cost rises ~8.2% as the vehicle moves from mid-life to aged bracket.

---

## 💡 Analysis Findings

1. **EV is the clear economic winner** at ₹1.75/km — 72% cheaper than Petrol — but 45-min charging and infrastructure gaps make it impractical for mixed use today.
2. **CNG is the best petrol alternative** at ₹3.32/km (-46%) with good CO₂ performance, if a conversion kit and station network are acceptable trade-offs.
3. **The E85 Paradox is real:** the 18% pump saving is entirely erased by lower fuel efficiency. Net result: ₹220/month *more* expensive than Petrol.
4. **Diesel has the highest CO₂** (0.179 kg/km) and maintenance cost (₹1.00/km) — unsuitable for city mixed use.
5. **Petrol at age 3** is still in its most efficient window; cost/km rises meaningfully after year 6.

---

## 🛠️ What I Built

- **Header** — Vehicle identity banner with name, fuel, age, monthly km
- **5 KPI cards** — Petrol cost/km, E85 cost/km, E85 premium, break-even price, monthly spend
- **SVG bar chart** — Cost/km per fuel with hover labels; Petrol highlighted with glow border
- **SVG doughnut chart** — CO₂/km share per fuel type with legend
- **SVG line chart** — Cost/km vs vehicle age (0–12y) for all fuels; vertical marker at age 3
- **CSS-animated gauge** — E85 score /10 with per-dimension breakdown
- **Fuel cards (×5)** — Pros ✅ cons ❌ best-for 🚗 for every fuel; Petrol card glows
- **E85 Paradox section** — Pump saving vs running penalty vs break-even

---

## 📚 Learnings

- **Prompt engineering for data tasks:** Providing a structured role + explicit formula definitions (`Cost/km = Fuel_Cost ÷ Distance`) eliminated hallucination of metrics — Claude computed exact numbers from CSV rows.
- **SVG-only charts:** No chart library needed; viewBox + coordinate math produces clean, responsive, themeable visuals with zero external dependencies.
- **The E85 paradox** is a great real-world example of why pump price ≠ running cost — mileage efficiency must always be factored in.
- **Glassmorphism dashboards** work well in dark-navy palettes; `backdrop-filter: blur()` + `rgba` borders create depth without heavy CSS frameworks.
- **Low effort level** on Claude still produced a complete, accurate single-file dashboard — showing that well-structured prompts reduce the need for model compute.

---

