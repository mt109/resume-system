# Workflow: Tailor for role

## When to run

- User asks to **tailor**, **adapt**, or **customize** the resume for a specific job, company, or role.
- User provides a job description or points to a file in `roles/`.

## Steps

1. **Identify target role**
   - If user said “for Google PM” or “for roles/google_pm.md,” use `roles/google_pm.md` (or the path they gave).
   - If user pasted a job description, use that; optionally create or update a file in `roles/` with the description and extracted keywords (e.g. `roles/acme_senior_pm.md`) for future runs.
   - Determine output filename: `versions/{company}_{role}.tex` (e.g. `versions/google_pm.tex`).

2. **Optional: choose persona**
   - If user said “tailor as a senior recruiter” (or hiring manager, executive, interviewer), load `personas/senior_recruiter.md` (or the matching persona). Otherwise skip.

3. **Run tailoring skill**
   - Follow the instructions in `skills/tailoring.md`.
   - Inputs: current resume (e.g. `resume_template.tex` or latest `versions/*.tex`), role context from step 1, optional persona from step 2, plus `data/` and `content/master_bullets.md`.
   - Output: write to `versions/{company}_{role}.tex`.

4. **Optional: suggest bullet improvements**
   - If the tailoring skill or persona suggests gaps (e.g. “add a metric here”), run **improve_bullet** for that bullet or role and offer to add the result to the tailored version and/or `master_bullets.md`.

5. **Confirm**
   - Tell the user where the tailored resume was written and, if used, which persona was applied.

## Skills used

- `skills/tailoring.md`
- Optionally: `skills/bullet_generator.md` (via improve_bullet workflow or skill)

## Personas

- Optionally adopt a persona from `personas/` when the user asks (e.g. “tailor as a hiring manager”). Pass the persona into the tailoring skill so it can reorder and emphasize accordingly.
