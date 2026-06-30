# Day 21 — Digital Privacy Intelligence Dashboard

## Overview
Built an interactive, single-file HTML dashboard that turns a self-reported list of 15 apps into a privacy/exposure report. The dashboard separates **Facts** (direct counts from the service list) from **Estimates** (reasoned inferences about typical data practices), and never claims access to private databases or certainty about inferred traits.

## Input Dataset
Apps: Instagram, Snapchat, TikTok, YouTube, Discord, WhatsApp, iMessage, Spotify, Roblox, PUBG Mobile, Amazon, Meesho, Google Search, Google Pay, Google Photos

## Key Outputs

### Digital Footprint Score: 72/100 — 🟠 Significant
- Total Services Used: 15
- Parent Companies: 11
- Ecosystem Concentration: ~27% Google (4 of 15 services)
- Estimated Tracking Surface: High

### Privacy Score: 38/100 — 🟠 Fair
- 8 of 15 apps are free/ad-supported
- 2 apps touch payments directly (Google Pay, and indirectly Amazon/Meesho)
- Messaging fragmented across 3 apps (WhatsApp, iMessage, Discord)

### Exposure Heatmap
Highest exposure: TikTok, Instagram, Google Search, Amazon, PUBG Mobile.
Lowest exposure: iMessage, Spotify, Discord.

### Company Exposure Ranking
1. Alphabet (Google) — 4 services (27%): Search, Pay, Photos, YouTube
2. Meta — 2 services (13%): Instagram, WhatsApp
3. All other companies (Snap, ByteDance, Discord Inc., Apple, Spotify AB, Roblox Corp., Krafton/Tencent, Amazon, Meesho) — 1 service each

### Risk Radar (top 3 risks, Estimates)
1. Ad Profiling — 82/100
2. Identity Linkage (cross-app, Google ecosystem) — 76/100
3. Social Graph Exposure — 70/100

### Digital Twin Profile (Estimates only)
Sketches a likely young/mobile-first, socially active persona based on app overlap (Roblox + PUBG + Discord + Snapchat), with shopping behavior inferred from Amazon + Meesho + Google Pay. Mobility/travel and income bracket were explicitly marked **"Not enough information provided"** since the dataset gives no basis to infer them.

### Most Valuable Data Assets (ranked)
1. Cross-Platform Identity Graph
2. Purchase + Payment Behavior
3. Entertainment Preference Profile
4. Social Graph / Contacts
5. Device & Usage Metadata
6. Search Intent History

### Privacy Improvement Simulator
Interactive sliders let the user simulate the projected effect of: limiting ad tracking, reducing shopping app permissions, consolidating messaging apps, and enabling 2FA — showing a directional (not guaranteed) projected Privacy Score increase.

### Final Verdict
Footprint sits in the **Significant** band while the Privacy Score is only **Fair** — exposure currently outpaces protective settings. Recommended first action: reduce ad-tracking permissions on social and shopping apps.

## Learnings
- Separating Facts from Estimates throughout the UI (not just in a disclaimer) makes the report feel trustworthy rather than overconfident.
- Concentration risk isn't just about installing many apps — it's about how many distinct parent companies and ecosystems end up holding correlated data (Google's 27% share here is the single biggest linkage risk).
- A simple radar chart + heatmap pairing communicates exposure faster than tables alone.
- Explicitly stating "Not enough information provided" instead of guessing builds more credibility than forcing an inference.

## Files in this folder
- `digital-privacy-dashboard.html` — the full interactive dashboard (open in any browser)
- screenshots of each dashboard section (to be added)