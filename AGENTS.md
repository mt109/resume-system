# Agent instructions

This repo is for **resume updates**. Use it to generate, tailor, or improve a resume quickly for any role.

- **Skills** (how to do tasks): `skills/` — resume_writer, bullet_generator, tailoring, cover_letter (role-targeted letter → `versions/{company}_{role}_cover_letter.md`), pdf_ingest (PDF → markdown/JSON → `data/` + `content/master_bullets.md`), role_fit (evaluate whether a role is a good fit before tailoring).
- **Workflows** (what to run end-to-end): `workflows/` — generate_resume, tailor_for_role, write_cover_letter, evaluate_role_fit (fit assessment + probing questions before tailoring), improve_bullet, review_resume, extract_learnings, update_learnings.
- **Job context** (what to tailor to): `roles/` — one file per target (e.g. `google_pm.md`). Each has job description and optional keywords/emphasis.
- **Personas** (whose perspective to use): `personas/` — senior_recruiter, hiring_manager, executive, interviewer. When the user asks to “tailor as a recruiter” or “review as a hiring manager,” load the matching persona and apply that perspective when selecting/rewriting bullets and when giving feedback.
- **Data**: `data/` (experiences.json, metrics.json, profile.json). **Content**: `content/master_bullets.md`.
- **Output**: Write tailored resumes to `versions/{company}_{role}.tex`. Base template: `resume_template.tex`. Cover letters: `versions/{company}_{role}_cover_letter.md` (see `skills/cover_letter.md`).
- **Reviews**: Write critiques to `reviews/{company}_{role}_review.md`.
- **Learnings (durable memory)**: `learnings/` contains distilled, reusable rules. **Do not write to `learnings/` directly from a raw review.**
- **Staging area**: `proposed_learnings/` is where extracted learnings are proposed for human approval.

When the user asks to tailor for a role, prefer reading `roles/{company}_{role}.md` if it exists; otherwise use the job description they provide in chat.

## Trust rules (important)

- **Never** mutate `learnings/` as a side-effect of `review_resume`.
- `extract_learnings` must write only to `proposed_learnings/`.
- `update_learnings` may update `learnings/` **only** using items the user has approved in `proposed_learnings/` (and should deduplicate/merge cleanly).
