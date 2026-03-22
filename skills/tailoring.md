# Skill: Tailoring

## When to use

- User asks to **tailor** or **adapt** the resume for a specific role or company.
- Workflow **tailor_for_role** is run.

## Inputs

- Current resume: `resume_template.tex` or an existing `versions/{company}_{role}.tex`.
- Target role: `roles/{company}_{role}.md` (preferred) or job description + notes from the user.
- `data/experiences.json`, `data/profile.json`, `content/master_bullets.md`.
- Optional: persona from `personas/` (e.g. “tailor as a senior recruiter”).

## Instructions

1. **Load role context:** From `roles/{company}_{role}.md` if it exists; otherwise from the user’s message. Extract: job title, required/mentioned skills, keywords, and any emphasis notes (e.g. “stress leadership,” “focus on metrics”).
2. **Load persona (if any):** If the user asked to tailor “as a recruiter” or “as a hiring manager,” load the matching file from `personas/` and use it to decide what to emphasize and how to order bullets.
3. **Match keywords:** Identify 5–10 terms from the job description that should appear in the resume (e.g. “roadmap,” “stakeholder,” “A/B test,” “metrics”). Ensure they appear naturally in the tailored version; do not keyword-stuff.
4. **Select and order bullets:** From the current resume and `master_bullets.md`, choose bullets that best match the role. Put the strongest match first in each section. Drop or shorten bullets that don’t support the target role. If a persona is set, order and emphasize according to that persona (e.g. recruiter: clarity and one number per bullet; hiring manager: impact and scope).
5. **Adjust emphasis:** Align headline and (if present) summary with the target role. Ensure experience section titles and bullets reflect the role’s level and domain.
6. **Output:** Produce a complete .tex file. Write to `versions/{company}_{role}.tex`. If the role file doesn’t specify company/role name, use a slug from the job title (e.g. `acme_senior_pm.tex`).

## Output

- A single .tex file written to `versions/{company}_{role}.tex`, ready to compile. Optionally, a short note listing which bullets were emphasized and which keywords were added.
