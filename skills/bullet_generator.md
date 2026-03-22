# Skill: Bullet generator

## When to use

- User asks to **improve**, **rewrite**, or **generate** one or a few bullets.
- Workflow **improve_bullet** or **tailor_for_role** needs new or stronger bullets.

## Inputs

- The bullet(s) to improve or replace (or a theme/role if generating from scratch).
- `data/experiences.json` — for context on the role and company.
- `data/metrics.json` — for numbers and outcomes to weave in.
- `content/master_bullets.md` — for style and existing phrasing.
- Optional: target role from `roles/` (for keywords and emphasis).
- Optional: persona from `personas/` (for tone and what to emphasize).

## Instructions

1. **Understand the ask:** Is this rewriting one bullet, or generating 1–2 new bullets for a role/theme? If rewriting, keep the same role and fact base; if generating, use experiences + metrics for that role or theme.
2. **Style:** Start with a strong action verb. Include at least one concrete number or outcome (from metrics.json or the experience). Prefer result → method (e.g. “Increased X by Y by doing Z”). Keep to one line when possible; two only if needed for clarity.
3. **STAR-style:** Situation/result should be clear; method can be one phrase. Avoid vague words (“helped,” “supported”) unless the role was explicitly supporting.
4. **Role/persona fit:** If a target role is provided, mirror important keywords. If a persona is provided, emphasize what they care about (e.g. recruiter: one clear number; hiring manager: scope and tradeoff; executive: business impact).
5. **Output:** Propose 1–2 bullet options. If the user or workflow asks to update `content/master_bullets.md`, append the chosen bullet with an optional tag (e.g. `#metrics`).

## Output

- 1–2 bullet strings, and optionally a patch or instruction to add the chosen one to `master_bullets.md`.
