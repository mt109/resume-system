# Skill: PDF ingest

## When to use

- User provides a **resume or CV as PDF** and wants it reflected in this repo’s **`data/`** and **`content/`** files.
- User asks to **import**, **migrate**, or **extract** resume content from a PDF into `profile.json`, `experiences.json`, `metrics.json`, and/or `content/master_bullets.md`.
- You need a **structured intermediate** (markdown or JSON) before merging into canonical files.

## Inputs

- Path to one or more **PDF files** (resume, CV, or exported LinkedIn PDF).
- Optional: user preference for **output first** — `markdown` (human-friendly), `json` (machine-friendly), or **direct merge** into repo files.
- Existing repo files to **preserve or merge with**: `data/profile.json`, `data/experiences.json`, `data/metrics.json`, `content/master_bullets.md` (read before overwriting).

## Target shapes (must match repo)

Use these as the merge targets; do not invent new top-level keys unless the user asks to extend the schema.

- **`data/profile.json`** — object with `name`, `email`, `phone`, `location`, `linkedin`, `headline`, `education` (array of `{ degree, school, year }`). See current file for example.
- **`data/experiences.json`** — JSON array of `{ company, title, dates, bullets[] }`. Bullets are strings (one achievement per string).
- **`data/metrics.json`** — object with `impact` and `scale` arrays of `{ label, value, context }`. Pull numbers and scope from bullets when obvious; leave arrays empty or minimal if the PDF has no quantified facts (user can fill later).
- **`content/master_bullets.md`** — bullets as prose lines separated by `---`, optional tag line under each bullet (e.g. `#metrics #launch`). Follow `content/master_bullets.md` style.

## Instructions

1. **Extract text from the PDF**
   - Prefer **local extraction** (no upload of personal data unless the user explicitly allows a cloud OCR/API).
   - Try in order, stopping when output is usable:
     - `pdftotext -layout path.pdf -` (poppler) — preserves rough layout.
     - `python3` with **pypdf** or **pdfplumber** if installed — good for multi-column or messy layout.
   - **Scanned PDFs** (image-only): say that text extraction will fail or be empty; offer OCR only if the user approves (e.g. Tesseract + `ocrmypdf`, or a tool they choose). Do not claim full accuracy for OCR.
   - If extraction is garbled, note which sections are unreliable and ask the user to paste those sections or provide a `.docx`/`.txt` export.

2. **Normalize to an intermediate representation**
   - Build a **structured outline**: header/contact, headline/summary, experience blocks (company, title, dates, bullets), education, skills (if present).
   - Optionally write a **draft markdown** file (e.g. `imports/{basename}_extracted.md`) with that outline for the user to correct before JSON merge — use when the PDF is messy or the user asked for review first.

3. **Map fields**
   - **Profile:** map contact lines and headline; map education entries to `education[]`.
   - **Experiences:** one object per role; **chronological order** with most recent first (match typical resume order).
   - **Bullets:** split stacked lines into separate bullets; strip page numbers and repeated headers/footers.
   - **Metrics:** extract `%`, `$`, counts, team sizes, time ranges into `metrics.json` **only when tied to a clear label**; avoid duplicating every bullet — prefer distilled “impact” and “scale” facts.

4. **Merge into repo files**
   - **Read** current `data/*.json` and `content/master_bullets.md` first.
   - If the user did not ask to **replace everything**, **merge**: keep existing entries unless the PDF clearly supersedes them; dedupe bullets (same meaning).
   - If replacing, confirm explicitly (or use a draft path like `imports/{basename}_profile.json`) before wiping canonical files.
   - **Validate JSON** after writing (parseable arrays/objects, required keys for each experience object).

5. **Confirm**
   - List which files were created or updated.
   - Call out **anything uncertain** (dates, one ambiguous role, missing metrics) so the user can fix in source.

## Output

- Updated or new **`data/profile.json`**, **`data/experiences.json`**, **`metrics.json`**, and/or **`content/master_bullets.md`**, and/or intermediate **`imports/*_extracted.md`** / **`imports/*_draft.json`** when the user wants a review step.
- Short summary of what was imported and what needs human verification.

## Optional: staging folder

If the repo has no `imports/` folder yet, create it for one-off extracts. Do not treat `imports/` as canonical — merge into `data/` and `content/` after user approval when using a two-step flow.
