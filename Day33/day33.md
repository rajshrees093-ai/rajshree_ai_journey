# Day 33 — Media Integrity Analyzer

**Challenge:** Build a Media Integrity Analyzer
**Goal:** Learn to evaluate information before believing it
**Deliverable:** Single-file offline HTML app + this write-up

---

## What I built

A single-file, offline, vanilla HTML/CSS/JS app called **Media Integrity Analyzer**, styled as an investigative "case file" — dossier cards, redaction-style dividers, exhibit tags, and a signature semicircle **credibility gauge** on the final dashboard.

**File:** [`media-integrity-analyzer.html`](./media-integrity-analyzer.html)

### Flow
1. **Theme picker** — 4 palettes to choose from, including Claude Orange, Forensic Green, Crimson Alert, and Midnight Newsroom.
2. **Exhibit A — Headline Detective** — a randomly generated fictional headline + article. You decide whether you'd click it, name what feels exaggerated, then reveal a Headline Accuracy Score, the specific mismatches between claim and evidence, a plain-language explanation of the technique used, and a fair rewritten headline.
3. **Exhibit B — Emotion Detector** — a randomly generated fictional post/reel caption. You name the feeling it produced and the exact words that caused it, then reveal the target audience, intended emotional response, manipulation technique, the phrases highlighted in the original text, and a neutral rewrite.
4. **Live metrics dock** (sticky, visible throughout) — Headline Accuracy, Source Reliability, Emotional Manipulation, and Audience Targeting update in real time as each exhibit is completed.
5. **Media Integrity Dashboard** — an overall integrity score on a semicircle gauge, a summary of what was learned, the biggest red flag from the session, three practical media-literacy habits, and a **Replay** button that reloads new randomized scenarios (5 headlines × 5 posts, non-repeating until exhausted).

### Build notes
- Pure vanilla HTML/CSS/JS in one file — no frameworks, no CDNs, no network calls, no images (all visuals are CSS/SVG).
- Themes are implemented as CSS custom-property sets swapped via a `data-theme` attribute on `<body>`.
- Verified the embedded `<script>` block parses cleanly (`new Function(...)` syntax check) and that all `<div>`/`</div>` tags balance before shipping.

---

## Key learnings

- **Headlines are optimized for clicks, not accuracy.** The gap between a headline's claim and the article's actual evidence is often wide — hedge words like "could" or "may" get dressed up as warnings, and small numeric changes ("4 to 9 incidents") get reframed as dramatic trends ("skyrocketing").
- **Emotion is the delivery mechanism for manipulation, not a side effect of it.** Posts that spread fastest tend to trigger fear, outrage, or urgency *before* the reader can evaluate the underlying claim. Naming the specific words that caused the feeling is what breaks the spell.
- **Vague sourcing and manufactured urgency are red flags on their own** — "sources say," "before this gets taken down," and "they don't want you to see this" are all designed to short-circuit verification, independent of whatever claim follows.
- **A single overall "integrity score" is more persuasive than four separate metrics**, which is exactly why the dashboard's gauge is the most memorable part of the experience — it mirrors how real audiences often want one number to trust, rather than reading the details.

---

## Screenshots



