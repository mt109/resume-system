# Workflow: Improve bullet

## When to run

- User asks to **improve**, **rewrite**, or **strengthen** one or more bullets.
- User highlights a bullet and asks for alternatives.
- Workflow **tailor_for_role** suggests adding or improving a bullet.

## Steps

1. **Get the bullet and context**
   - Input: the exact bullet text (or the role + “generate a bullet for X”).
   - Optional: target role from `roles/` (for keywords and emphasis).
   - Optional: persona from `personas/` (e.g. “improve for a hiring manager”).

2. **Run bullet_generator skill**
   - Follow the instructions in `skills/bullet_generator.md`.
   - Pass: the bullet to improve (or theme/role for new bullets), `data/experiences.json`, `data/metrics.json`, `content/master_bullets.md`, optional role, optional persona.
   - Get back 1–2 proposed bullets.

3. **Present options**
   - Show the user the 1–2 bullet options with a brief note on what changed (e.g. “Added metric,” “Aligned with role keyword X”).

4. **Optional: update content**
   - If the user chooses one option and wants it saved, append it to `content/master_bullets.md` with an optional tag (e.g. `#metrics`). If the bullet was from a specific role in `experiences.json`, note that the user can paste it there when they update their data.

5. **Optional: update a version**
   - If the user wants the new bullet in a specific `versions/*.tex` file, apply the replacement and save the file.

## Skills used

- `skills/bullet_generator.md`

## Personas

- If the user says “improve this for an executive” (or recruiter, hiring manager, interviewer), load the matching persona and pass it to the bullet_generator skill so the proposed bullets match that perspective.
