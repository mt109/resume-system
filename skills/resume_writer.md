# Skill: Resume writer

## When to use

- User asks to **generate** or **write** a full resume (or a full section).
- Workflow **generate_resume** or **tailor_for_role** needs a complete .tex output.

## Inputs

- `data/profile.json` — name, contact, education, headline.
- `data/experiences.json` — roles, dates, bullets.
- `content/master_bullets.md` — optional pool to pull or adapt bullets.
- `resume_template.tex` — section order and LaTeX structure to follow.
- Optional: a target role from `roles/{company}_{role}.md` (for emphasis and ordering).
- Optional: a persona from `personas/` (for tone and emphasis when tailoring).

## Instructions

1. **Load** profile, experiences, and template. If a role file exists, load it for keywords and emphasis. If a persona is requested, load it and apply that perspective to ordering and emphasis.
2. **Section order:** Match `resume_template.tex` (typically: header → experience → education → skills or extras). Do not invent new sections unless the template has them.
3. **Length:** Aim for one page unless the user or role clearly needs two. Prefer 3–4 bullets per role; most recent role can have 4, earlier roles 2–3.
4. **Bullets:** Prefer bullets from `experiences.json` and `master_bullets.md`. If the target role is set, emphasize bullets that match role keywords and put the strongest fit first. If a persona is set, prioritize what that persona cares about (e.g. recruiter: keywords and one number per bullet; executive: scale and business outcome first).
5. **Output:** Valid LaTeX that compiles with the template. Use the same commands and section names as `resume_template.tex` (e.g. `\section`, `\subsection`, itemize). Do not change template macros unless the user asks.
6. **Write** the result to the path specified by the workflow (e.g. `versions/{company}_{role}.tex` or overwrite the template for a “base” output).

## Output

- A single .tex file (path given by the workflow or user) that is ready to compile.
