# Claude Code instructions

Read `AGENTS.md` for full agent instructions, then follow the skills and workflows defined there.

## Quick start

1. Read `AGENTS.md` — it lists all skills, workflows, personas, data paths, and trust rules.
2. Read `data/profile.json`, `data/experiences.json`, and `content/master_bullets.md` to understand the candidate.
3. When the user asks to tailor for a role, check `roles/` for an existing file first.
4. When generating output, write resumes to `versions/{company}_{role}.tex` and cover letters to `versions/{company}_{role}_cover_letter.md`.

## Trust rules

- Never write to `learnings/` directly. Use `proposed_learnings/` and wait for approval.
- Never invent metrics, titles, or credentials not in the data files.
- Use honest scope verbs: "own" for current FT work, "led" for end-to-end, "contributed to" for intern work.
