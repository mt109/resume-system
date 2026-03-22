# Workflow: Update learnings

## When to run

- User has approved (or edited) items in `proposed_learnings/` and wants them merged into durable memory.
- User says “merge these learnings” or “update learnings with what I approved.”
- After **extract_learnings**, the user has reviewed the proposal and is ready to make it permanent.

## Steps

1. **Identify approved source(s)**
   - Input: one or more files in `proposed_learnings/` (e.g. `proposed_learnings/google_pm_review_learnings_proposed.md`).
   - If the user doesn’t specify, ask or use the most recent proposal.
   - The user may have edited the file to remove items they don’t want; treat the current file contents as the approved set.

2. **Load current learnings**
   - Read `learnings/writing_rules.md`, `learnings/tailoring_rules.md`, and files in `learnings/company_patterns/` (e.g. `learnings/company_patterns/google_pm.md`).

3. **Deduplicate**
   - For each approved item, check if an equivalent rule already exists in the target file.
   - Skip exact duplicates and near-duplicates; merge or refine if the new version is clearer.

4. **Merge by category**
   - **Writing learnings** → Append or integrate into `learnings/writing_rules.md`. Keep entries concise; group by theme if helpful.
   - **Tailoring learnings** → Append or integrate into `learnings/tailoring_rules.md`. Avoid redundancy with writing rules.
   - **Role/company-specific learnings** → Append or integrate into `learnings/company_patterns/{company}_{role}.md`. Create the file if it doesn’t exist (e.g. `learnings/company_patterns/startup_pm.md`).

5. **Keep non-redundant**
   - Prefer one clear statement per rule. If two approved items say the same thing, combine them.
   - Maintain a consistent format (e.g. bullet list with one rule per line).

6. **Write updates**
   - Update only the learnings files that received new content.
   - Optionally: move or archive the source file in `proposed_learnings/` (e.g. rename to `_merged` or move to a `processed/` subfolder) so it’s clear what’s been applied. Ask the user if they want this.

7. **Confirm**
   - Tell the user which files were updated and how many items were merged.
   - Remind them that future **resume_writer**, **bullet_generator**, and **tailoring** runs can now use these learnings if the skills are updated to read from `learnings/`.

## Output

- Updated `learnings/writing_rules.md`, `learnings/tailoring_rules.md`, and/or `learnings/company_patterns/*.md`.

## Trust rule

- Only merge items that appear in the user-approved proposal file(s). Do not infer or add learnings that weren’t in the proposal.
