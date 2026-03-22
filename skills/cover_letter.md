# Skill: Cover letter

## When to use

- User asks for a **cover letter**, **letter of interest**, or **application email** for a specific role or company.
- User wants a narrative that **complements** a tailored resume (same role) without repeating it bullet-for-bullet.
- After **`tailor_for_role`** or alongside **`versions/{company}_{role}.tex`**, to produce matching prose for an application portal.

## Inputs

- **Target role:** `roles/{company}_{role}.md` (preferred) or full job description + URL from the user.
- **Candidate facts:** `data/profile.json`, `data/experiences.json`, `data/metrics.json`; optional `content/master_bullets.md` for phrasing.
- **Tailored resume (optional):** `versions/{company}_{role}.tex` or the version the user is submitting—keep **claims consistent**; do not introduce new metrics or titles not supported by data or the resume.
- **Optional from user:** Hiring manager or recruiter name; tone (formal / direct / warm); max length (words or one page); things to **avoid** (salary, relocation); **must-include** themes (e.g. XR, ML partnership).

## Instructions

1. **Extract job signals:** From the role file or JD: official job title, team/product (if stated), top 3–5 responsibilities, required skills, mission or values language worth echoing **once** (no buzzword stacking).
2. **Pick 2–3 proof points:** Choose the strongest **true** stories from `experiences.json` / metrics that map to those responsibilities (e.g. discovery → Offer Wallet / merchandising / experimentation; XR → Unity + gaming surfaces). Prefer **outcome + your role** in one sentence each.
3. **Structure (default):**
   - **Opening (short):** State role, company, and why this intersection fits you (one concrete hook—not “I am writing to apply”).
   - **Body:** One paragraph on **relevant impact** (numbers only if already in data/resume and approved for external use); one paragraph on **skills or domain** (e.g. ML coursework + how you’d collaborate with ML/DS if you don’t own recsys); optional short paragraph on **mission/culture** only if grounded (no generic flattery).
   - **Close:** Confident, brief thank-you and forward look (interview, conversation)—no desperation.
4. **Do not:** Copy the entire resume; repeat the same bullet text verbatim; invent credentials, dates, or unreleased product details; claim sole ownership of team/ org outcomes—use **accurate** verbs (owned, led, contributed to, shipped, supported).
5. **Length:** Aim **250–400 words** unless the user specifies otherwise; stay within **one page** if they will paste into a PDF.
6. **Formatting:** Plain paragraphs for `.md`; optional greeting (`Dear Hiring Manager,` or named if provided). Sign-off with the candidate’s name from `profile.json`.

## Output

- Write to **`versions/{company}_{role}_cover_letter.md`** using the same `{company}_{role}` slug as the tailored resume (e.g. `versions/google_youtube_xr_gaming_discovery_cover_letter.md`).
- If the user only has a free-text company name, derive a sensible slug or ask once.
- After writing, tell the user the **file path** and offer to **tighten for a word limit** or **paste-ready plain text** if they need it for a web form.

## Optional: persona

- If the user asks to “sound like a hiring manager would want” or similar, load `personas/hiring_manager.md` and bias toward **impact, tradeoffs, and clarity** over adjectives.
- For **startup** or **highly technical** roles, slightly shorter sentences and more **specific nouns** (systems, surfaces, metrics).
