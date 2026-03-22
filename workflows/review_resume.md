# Workflow: Review resume

## When to run

- User asks to **review**, **critique**, or **evaluate** a resume version.
- After running **tailor_for_role**, the user wants feedback on the output.
- User wants to see how a specific persona (recruiter, hiring manager, etc.) would react.

## Steps

1. **Identify target resume**
   - Input: path to a resume in `versions/` (e.g. `versions/google_pm.tex`) or the user’s specification (“review my Google PM version”).
   - Determine the corresponding role: if the file is `versions/google_pm.tex`, the role is `roles/google_pm.md`.

2. **Load context**
   - Read the resume file (parse the .tex or extract readable content).
   - Read the related role file from `roles/` for job context, keywords, and emphasis.
   - If user said “review as a hiring manager” (or recruiter, executive, interviewer), load the matching file from `personas/`.

3. **Produce the critique**
   - Apply the persona’s perspective if one was specified; otherwise use a balanced reviewer lens.
   - Structure the review with:
     - **Strengths** — What works well, what stands out positively.
     - **Weaknesses** — What’s missing or could be stronger.
     - **Missing signals** — Keywords, metrics, or scope the role expects but aren’t present.
     - **Risky or vague claims** — Bullets that are unclear, inflated, or could invite tough interview questions.
     - **Concrete rewrite suggestions** — Specific edits or bullet replacements (1–2 per weak area).

4. **Write the review**
   - Output path: `reviews/{company}_{role}_review.md` (e.g. `reviews/google_pm_review.md`).
   - Use the same naming as the source version for traceability.
   - **Do not** write to `learnings/` or `proposed_learnings/` in this workflow.

5. **Confirm**
   - Tell the user where the review was written and, if used, which persona was applied.

## Output

- A markdown file in `reviews/` with the full critique, ready for human reading and optional use in **extract_learnings**.

## Personas

- If the user says “review as a senior recruiter” (or hiring manager, executive, interviewer), load the matching persona and apply that perspective when judging strengths, weaknesses, and suggestions. The persona’s “tone for feedback” should shape how you phrase the critique.
