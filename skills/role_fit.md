# Skill: Role fit evaluation

## When to use

- User asks whether a role is a **good fit**, whether they should **apply**, or wants a **fit assessment** before investing time in tailoring.
- User pastes a job description or points to an existing `roles/{company}_{role}.md` file.
- Before running `tailor_for_role` or `write_cover_letter`, to decide if the effort is worth it.

## Inputs

- **Target role:** `roles/{company}_{role}.md` (preferred) or raw JD from user.
- **Candidate data:** `data/profile.json`, `data/experiences.json`, `data/metrics.json`, `content/master_bullets.md`.
- **Learnings (optional):** `learnings/tailoring_rules.md`, `learnings/company_patterns/{company}.md` — prior knowledge about what works for this company.
- **User answers** to probing questions (gathered by the workflow before this skill runs in depth).

## Dimensions to evaluate

Score each dimension **Strong fit / Moderate fit / Weak fit / Dealbreaker** with a one-line rationale.

| # | Dimension | What to assess |
|---|-----------|----------------|
| 1 | **Hard skills match** | Do the candidate's technical skills, tools, and frameworks cover the minimum qualifications? Which preferred qualifications are met? |
| 2 | **Experience level** | Does years of experience and scope (team size, revenue, user scale) meet the bar? Is it a stretch, lateral, or step-back? |
| 3 | **Domain relevance** | Has the candidate worked in or adjacent to this industry/product area? How much reframing is needed to bridge? |
| 4 | **Soft skills & leadership** | Do the candidate's cross-functional, communication, and leadership experiences map to what the role demands? |
| 5 | **Culture & values** | Does the company's stated mission/culture align with what the candidate cares about? Are there genuine stories to tell? |
| 6 | **Growth & career arc** | Does this role advance the candidate's career goals? Does it open doors they want opened? |
| 7 | **Logistics** | Location, compensation range, travel, visa/sponsorship, hybrid/remote — are there blockers? |
| 8 | **Competitive positioning** | Against the likely applicant pool, where does the candidate fall? What would make them stand out or blend in? |

## Instructions

1. **Parse the JD** — Extract: title, level, team/product, minimum qualifications, preferred qualifications, responsibilities, stated values/culture, location, comp range, travel requirements.

2. **Map candidate strengths** — For each JD requirement, find the best matching evidence from `experiences.json`, `metrics.json`, `master_bullets.md`, and `profile.json`. Note where a match is direct, where it requires reframing, and where there is no credible bridge.

3. **Identify gaps honestly** — List qualifications or responsibilities with no clear candidate match. Classify each gap:
   - **Bridgeable:** Candidate has adjacent experience that can be reframed (state the reframe).
   - **Learnable:** Candidate lacks it but could credibly acquire it quickly (state why).
   - **Hard gap:** No realistic bridge — would rely on the employer overlooking it.

4. **Ask probing questions** — Before issuing a verdict, surface unknowns the data files can't answer. Ask the user directly (see "Probing questions" section below). Incorporate their answers into the final assessment.

5. **Score dimensions** — Fill in the dimension table with ratings and rationale.

6. **Produce verdict** — One of:
   - **Strong fit — apply.** Most dimensions are strong; gaps are bridgeable; competitive positioning is favorable.
   - **Worth a shot — apply with caveats.** Moderate fit overall; some hard gaps but the role is compelling enough to try. State what the candidate should emphasize and what risks to acknowledge.
   - **Stretch — apply only if highly motivated.** Multiple weak dimensions; candidate would need to outperform in interview to compensate. State what would need to go right.
   - **Poor fit — skip or revisit later.** Dealbreakers or too many hard gaps. Suggest what the candidate would need to change (experience, skills, timing) before this role class becomes viable.

7. **Suggest next steps** — Based on verdict:
   - Strong/Worth a shot → offer to run `tailor_for_role` and `write_cover_letter`.
   - Stretch → suggest specific prep (portfolio project, upskilling, networking) before applying.
   - Poor fit → suggest alternative role types or companies that better match current profile.

## Probing questions

Ask **only** what the data files can't answer. Pick the most relevant 3–5 from this bank; don't dump all of them. Adapt wording to the specific role.

### Career intent
- What draws you to this role — is it the company, the team/product, the job function, or something else?
- Where do you want to be in 2–3 years? Does this role move you toward that?
- Are you optimizing for learning, compensation, title, impact, or something else right now?

### Logistics & dealbreakers
- Are you open to the location (and hybrid/on-site expectations)?
- Does the comp range work for you?
- Any visa or sponsorship constraints?
- Would you need relocation assistance — and is that a blocker if they don't offer it?
- Is the travel requirement (if any) acceptable?

### Domain & motivation
- Do you have genuine interest in this product/domain, or is it mainly a career move?
- Is there a personal story or connection to the product that would be authentic in a cover letter?
- Have you used the product as a customer? What's your honest take on it?

### Gaps & honesty
- For the biggest gap I've identified: do you have any experience you haven't told me about that might bridge it?
- Are you comfortable being asked about [gap area] in an interview? Do you have a credible answer?
- Is there anything in the JD that makes you uncomfortable or that you'd want to push back on?

### Competitive context
- Do you know anyone at the company who could refer you?
- Have you applied here before? If so, what happened?
- Are you interviewing at similar companies — does this affect urgency or leverage?

## Output

- **Inline conversation:** Present the probing questions first, then deliver the fit assessment as a structured message (dimension table + gaps + verdict + next steps). Do **not** write a file unless the user asks for one.
- **Optional file:** If the user asks to save the assessment, write to `reviews/{company}_{role}_fit.md`.
