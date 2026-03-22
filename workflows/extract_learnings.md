# Workflow: Extract learnings

## When to run

- User asks to **extract learnings** or **pull patterns** from one or more review files.
- After running **review_resume**, the user wants durable rules proposed (but not yet merged).
- User wants to stage insights for approval before updating `learnings/`.

## Steps

1. **Identify source review(s)**
   - Input: one or more files in `reviews/` (e.g. `reviews/google_pm_review.md`).
   - If the user doesn’t specify, use the most recent review or ask which to use.

2. **Load existing learnings**
   - Read `learnings/writing_rules.md`, `learnings/tailoring_rules.md`, and any files in `learnings/company_patterns/`.
   - Use these to **deduplicate** — do not propose something that’s already captured.

3. **Extract with filters**
   - Read the review(s) and identify patterns that are:
     - **Reusable** — Applies beyond this single resume version.
     - **Actionable** — The agent or user can do something with it.
     - **Likely to matter again** — Will help future tailoring or writing.
     - **Not already in learnings/** — Skip duplicates.
   - Ignore one-off comments unless they imply a broader rule (e.g. “this bullet needs a number” → “Include at least one concrete metric per major role where possible”).
   - If confidence is low, mark the item as **tentative** in the output.

4. **Categorize**
   - Sort extracted items into:
     1. **Writing learnings** — General rules about bullets and structure (e.g. “Start bullets with strong action verbs,” “Show impact before implementation detail”).
     2. **Tailoring learnings** — Rules for adapting to roles (e.g. “Match 5–10 keywords from the job description naturally”).
     3. **Role/company-specific learnings** — Rules for a specific company or role family (e.g. “Google PM resumes should foreground scale, experimentation, and metrics”).

5. **Write to proposed_learnings**
   - Output path: `proposed_learnings/{source}_learnings_proposed.md` (e.g. `proposed_learnings/google_pm_review_learnings_proposed.md`).
   - Use clear headings for each category.
   - **Do not** write to `learnings/` directly.
   - Each proposed item should be a concise, actionable bullet.

6. **Confirm**
   - Tell the user where the proposal was written and that they can edit/approve before running **update_learnings**.

## Output

- A markdown file in `proposed_learnings/` with candidate learnings, categorized and ready for human approval.

## Trust rule

- This workflow writes **only** to `proposed_learnings/`. Merging into `learnings/` happens via **update_learnings** after the user approves.
