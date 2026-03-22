# Workflow: Evaluate role fit

## When to run

- User asks "is this role a good fit?", "should I apply?", "evaluate this JD for me," or similar.
- User pastes a job description or references a `roles/{company}_{role}.md` file and wants a fit assessment before committing to tailoring.
- Before running `tailor_for_role`, to decide whether the time investment is worthwhile.

## Steps

### 1. Load or create the role file

- If `roles/{company}_{role}.md` exists for this role, read it.
- If the user pasted a raw JD, create `roles/{company}_{role}.md` with the standard structure (summary, qualifications, keywords, emphasis, gap notes) so future workflows can reuse it.
- Confirm the slug with the user if the company/role name is ambiguous.

### 2. Load candidate data

- Read `data/profile.json`, `data/experiences.json`, `data/metrics.json`, `content/master_bullets.md`.
- Optionally read `learnings/tailoring_rules.md` and `learnings/company_patterns/{company}.md` if they exist.

### 3. Quick-scan and ask probing questions

- Run a fast pass of the role_fit skill's "Map candidate strengths" and "Identify gaps" steps to understand where the unknowns are.
- Select the **3–5 most relevant probing questions** from `skills/role_fit.md` based on the specific role and gaps identified.
- Present the questions to the user and **wait for answers** before proceeding. Do not guess.

### 4. Run role_fit skill (full evaluation)

- With the user's answers incorporated, follow `skills/role_fit.md` end to end.
- Score all eight dimensions, list gaps with classifications, and produce a verdict.

### 5. Present the assessment

- Deliver the structured fit assessment inline:
  - **Dimension table** (8 rows, rated and explained).
  - **Gap analysis** (bridgeable / learnable / hard).
  - **Verdict** (Strong fit / Worth a shot / Stretch / Poor fit) with reasoning.
  - **Next steps** — what to do based on the verdict.
- If verdict is "Strong fit" or "Worth a shot," ask whether the user wants to proceed to `tailor_for_role` and/or `write_cover_letter`.

### 6. Optional: save assessment

- If the user asks, write the assessment to `reviews/{company}_{role}_fit.md`.

## Skills used

- `skills/role_fit.md`

## Personas

- Not used by default. If the user asks "would a recruiter think I'm a fit?" or similar, load the relevant persona from `personas/` and bias the competitive-positioning and verdict toward that perspective.

## Related workflows

- **tailor_for_role** — natural next step if the verdict is positive.
- **write_cover_letter** — often paired with tailoring after a positive fit assessment.
- **review_resume** — useful after tailoring to validate the result.
