# Resume System

An AI-powered system that generates tailored resumes, cover letters, and application materials from structured career data. Instead of manually rewriting a resume for every job, you describe a role — or paste a job description — and the system produces a version optimized for that specific application.

Built to work with AI coding agents (Cursor, Claude Code, GitHub Copilot). The system stores career data once and reuses it across every application, applying durable learnings from past reviews to improve each new version.

## How it works

**Your career data lives in structured files** — experiences, metrics, skills, and a pool of tagged resume bullets. When you target a new role, the system matches your strongest evidence to that role's requirements, reframes language for the domain, and produces a complete LaTeX resume and optional cover letter.

**Four personas** (senior recruiter, hiring manager, executive, interviewer) can critique any generated resume from different perspectives — flagging ATS risks, weak bullets, missing impact signals, or interview vulnerability.

**The system learns.** After each review cycle, insights are extracted, staged for approval, and merged into durable writing and tailoring rules. Each new resume benefits from every past iteration.

## What's inside

```
data/               Career facts: experiences, metrics, profile
content/            Master bullet pool with tags (#commerce, #AI, #leadership...)
roles/              One file per target role: JD analysis, keywords, tailoring emphasis, gap notes
personas/           Recruiter, hiring manager, executive, interviewer perspectives
skills/             Modular capabilities: resume writing, tailoring, cover letters, role fit evaluation, PDF ingest
workflows/          End-to-end flows: generate, tailor, review, write cover letter, evaluate role fit, extract/update learnings
versions/           Output: tailored .tex resumes and cover letters per application
reviews/            Multi-persona critiques of generated resumes
learnings/          Durable rules distilled from past sessions (writing, tailoring, company patterns)
proposed_learnings/ Staged learnings awaiting human approval
```

## Getting started

### Prerequisites

- An AI coding agent with file access. Any of these work:
  - [Cursor](https://cursor.sh) (open this folder as a workspace)
  - [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (run `claude` in this directory — it reads `CLAUDE.md` automatically)
  - [GitHub Copilot](https://github.com/features/copilot) in VS Code with chat enabled
  - Any LLM with file read/write access
- [LaTeX](https://www.tug.org/texlive/) installed locally to compile `.tex` output to PDF (`brew install --cask basictex` on macOS)

### Setup

1. Clone the repo:
   ```bash
   git clone https://github.com/mt109/resume-system.git
   cd resume-system
   ```

2. Open it in your AI agent of choice.

3. Start by asking any of the prompts below — the agent reads `AGENTS.md` for instructions on where to find skills, workflows, personas, and data.

### What you can ask

| Prompt | What happens |
|--------|-------------|
| "Generate a resume for [role]" | Produces a tailored `.tex` resume from the candidate's data |
| "Tailor for this job" + paste a JD | Analyzes the JD, matches evidence, reframes language, outputs a role-specific resume |
| "Is this role a good fit?" | Evaluates a JD against the candidate's profile, asks probing questions, gives a structured verdict |
| "Review this resume as a hiring manager" | Multi-persona critique with actionable feedback |
| "Write a cover letter for [company]" | Narrative that complements the resume without repeating it |
| "Improve this bullet" | Rewrites a single bullet for clarity, impact, and keyword alignment |

### Adding a new target role

1. Create `roles/{company}_{role}.md` with the job description, keywords, tailoring emphasis, and gap notes. See existing files in `roles/` for the format.
2. Ask the agent to generate a resume or cover letter for that role — it will use the role file automatically.

### Compiling a resume to PDF

```bash
pdflatex -output-directory versions versions/{company}_{role}.tex
```

## Design principles

- **Single source of truth.** Career data is stored once and never duplicated across versions.
- **Human-in-the-loop.** Learnings are proposed, not auto-applied. Nothing mutates durable memory without explicit approval.
- **Honest by default.** Scope verbs match actual ownership ("own" vs. "contributed to"). Gaps are named and bridged, not hidden.
- **Compounding quality.** Every review makes the next resume better through extracted and approved learnings.
