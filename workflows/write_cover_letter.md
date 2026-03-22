# Workflow: Write cover letter

## When to run

- User asks for a **cover letter**, **letter of interest**, or **application letter** for a specific job.
- User is applying with a tailored resume and wants **prose** that complements `versions/{company}_{role}.tex` (or another version they name).
- After **tailor_for_role**, the user wants matching narrative for the same `{company}_{role}` slug.

## Steps

1. **Identify target role**
   - Prefer `roles/{company}_{role}.md` if it exists (same slug as the resume version).
   - If the user only pasted a JD, use that; optionally create or update `roles/{company}_{role}.md` for reuse.
   - Confirm output path: `versions/{company}_{role}_cover_letter.md` (e.g. `versions/google_youtube_xr_gaming_discovery_cover_letter.md`). If the resume uses a suffix like `_v2`, either align the slug with the user’s chosen filename or use `{base}_cover_letter.md` and state which resume it pairs with.

2. **Optional: addressee and constraints**
   - If the user named a hiring manager or recruiter, use it in the greeting; otherwise **Dear Hiring Manager,** or **Dear YouTube Hiring Team,** (only if accurate).
   - Capture word limit, tone, must-include themes, or topics to avoid (salary, relocation).

3. **Optional: persona**
   - If the user asks to “write for a hiring manager” or similar, load the matching file from `personas/` and bias tone (e.g. impact, tradeoffs, clarity).

4. **Run cover_letter skill**
   - Follow `skills/cover_letter.md`.
   - Inputs: role context from step 1, `data/profile.json`, `data/experiences.json`, `data/metrics.json`, optional `versions/{company}_{role}.tex` (or `_v2`) for consistency—**do not** add claims that are not in data or the resume.
   - Output: write `versions/{company}_{role}_cover_letter.md`.

5. **Confirm**
   - Tell the user the file path and that they can paste into a portal or export to PDF. Offer a shorter variant if they hit a character limit.

## Skills used

- `skills/cover_letter.md`

## Personas

- Optional: `personas/hiring_manager.md` (or others) when the user asks for a specific voice or emphasis.

## Related workflows

- **tailor_for_role** — produces the `.tex` resume this letter should align with.
- **review_resume** — for resume critique; does not replace human edit of the cover letter before send.
