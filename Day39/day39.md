# Day 39 — PDF Splitter & Merger ("Leaflet")

**Deliverable:** `pdf-splitter-merger.html` — a single-file, fully client-side PDF utility.

## What it does

**Leaflet** is a premium PDF utility with two tools, both running entirely in the browser (no file ever touches a server):

### Splitter
- Upload one PDF → automatic page-count detection + lazy-loaded thumbnail grid (via `pdf.js`)
- Four split methods: **Custom ranges**, **Every N pages**, **Split after specific pages**, **Extract selected pages** (click thumbnails)
- Multiple ranges per operation, live validation with inline error highlighting
- Per-page **rotate** (90° increments) and **exclude/delete** directly from the thumbnail grid
- Live "output preview" showing exactly which files will be produced and how many pages each contains
- Optional **compression** (rasterizes pages to optimized JPEG via canvas) before download
- Per-file preview + download, or **Download all as .zip** (via `JSZip`)

### Merger
- Drag-and-drop or multi-select upload
- Sortable file list (native HTML5 drag-and-drop) with per-file thumbnail + page count
- Live summary bar: total files, total pages, estimated output size
- Optional **page numbers** (4 position choices) and **diagonal watermark** text, both drawn with `pdf-lib`
- Optional **compression** with a quality slider
- Single merged PDF with instant preview + download

### Cross-cutting features
- Dark mode (persisted via `localStorage`, respects `prefers-color-scheme`)
- Keyboard shortcuts: `1`/`2` switch tools, `Ctrl/⌘+O` open file, `Ctrl/⌘+Enter` run, `D` toggle theme, `?` shortcuts help, `Esc` close dialogs
- Toast notifications, processing overlay with progress bar, empty/error states
- Fully responsive layout, visible focus states, `prefers-reduced-motion` respected
- Works fully offline after the first load (all processing is local; only the three CDN libraries need to load once)

## Tech stack

| Purpose | Library |
|---|---|
| Page rendering / thumbnails | [pdf.js](https://mozilla.github.io/pdf.js/) |
| Split / merge / rotate / watermark / page numbers | [pdf-lib](https://pdf-lib.js.org/) |
| Zip packaging for bulk downloads | [JSZip](https://stuffit.com/jszip/) |
| Fonts | Fraunces (display), Inter (UI), JetBrains Mono (data) |

No backend, no build step, no npm install — just one `.html` file.

## Design approach

Instead of a generic dashboard look, the UI leans into the subject matter: a paper/stationery aesthetic (cream paper background, folder-tab style navigation between "Split" and "Merge", a subtle dot-grain paper texture, perforated dashed lines on the split icon). Cobalt blue was chosen as the accent instead of the more common warm terracotta/cream combination, to avoid the templated "AI generated" look while staying legible and calm for a utility tool.

## Key learnings

1. **Client-side PDF work is very capable now** — `pdf-lib` + `pdf.js` cover reading, rendering, page copying, rotation, drawing text/images, and re-saving without ever leaving the browser, which is exactly what a "your files never leave your device" promise requires.
2. **Buffer detachment is a real gotcha.** Passing the same `ArrayBuffer`/`Uint8Array` into both `pdf.js` and `pdf-lib` (or reusing it across multiple `PDFDocument.load()` calls) can cause "detached ArrayBuffer" errors once a worker transfers it. Always `.slice(0)` a fresh copy per consumer.
3. **True client-side compression is a trade-off.** `pdf-lib` alone can't meaningfully shrink text-based PDFs. The practical answer is rasterizing pages to JPEG at a controllable quality — great for scanned/image-heavy files, but it sacrifices selectable text, so it's offered as an explicit opt-in with that trade-off stated in the UI copy rather than a silent default.
4. **Lazy-rendering thumbnails matters for large PDFs.** Rendering every page eagerly on load would freeze the UI for big documents; an `IntersectionObserver` on the thumbnail grid keeps the initial load fast and only renders pages as they scroll into view.
5. **Overlapping click targets are an easy accessibility bug.** An early version stacked a transparent `<input type="file">` directly over a clickable dropzone `<div>` with its own click handler — that combination can fire the native file picker twice and creates duplicate tab stops. Moving the input off-screen and routing all interaction through the dropzone's own click/keydown handlers fixed both issues.

## How to run

1. Save `pdf-splitter-merger.html` anywhere on disk.
2. Open it directly in any modern browser (Chrome, Edge, Firefox, Safari) — no server required.
3. Use the **Split** or **Merge** tab to get started.