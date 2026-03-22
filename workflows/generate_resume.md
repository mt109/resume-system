# Workflow: Generate resume

## When to run

- User asks to **generate**, **create**, or **build** a resume (from scratch or a fresh version).
- User has updated `data/` or `content/` and wants a new full resume.

## Steps

1. **Gather inputs**
   - Read `data/profile.json`, `data/experiences.json`, `data/metrics.json`.
   - Read `content/master_bullets.md`.
   - Read `resume_template.tex` for section order and LaTeX structure.
   - If the user specified a target role (e.g. “for Google PM”), read `roles/{company}_{role}.md` if it exists.
   - If the user asked for a persona (e.g. “as a recruiter would see it”), read the matching file in `personas/`.

2. **Run resume_writer skill**
   - Follow the instructions in `skills/resume_writer.md`.
   - Pass: profile, experiences, master_bullets, template, optional role, optional persona.
   - Output path: if a role was specified, write to `versions/{company}_{role}.tex`; otherwise write to `versions/base.tex` or a name the user provides.

3. **Emit and confirm**
   - Write the generated .tex to the chosen path.
   - Tell the user where the file was written and that they can compile it (e.g. `pdflatex versions/foo.tex`).

## Skills used

- `skills/resume_writer.md`

## Optional

- If experiences or master_bullets are thin, suggest running **improve_bullet** for key roles before or after generating.
