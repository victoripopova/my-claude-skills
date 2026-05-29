---
name: prd-creator
description: Creates a structured Product Requirements Document (PRD) as a Markdown file from a user-provided feature description or notes. Use this skill whenever the user wants to write a PRD, product spec, or feature document — even if they say things like "draft a spec", "write up this feature", "turn my notes into a PRD", or "document this product idea". Always use this skill when the output should be a PRD-style document, regardless of how casually the request is phrased.
---

# PRD Creator

Creates a well-structured PRD Markdown file from a user's feature description, using a consistent template and a real example for reference.

## Inputs

The user provides one or more of:
- **Feature description** — freeform notes, bullet points, or a brief overview of what they want to build
- **Open questions / context** — hypotheses, unknowns, design constraints

Claude extracts any missing information from context before writing. If the user segment, severity of impact, or other critical details are not clear, ask before writing — do not invent plausible-sounding content.

## Steps

1. **Read the template and example** — load `references/prd-template.md` and `references/prd-example.md` before writing anything.
2. **Map the user's input to the template sections** — extract Problem, Customer Insights (Available Data + Open Questions), Solution (Now/Next and optionally Later), Design, Dev, Metrics (Main + Instrumental), Launch from the user's description.
3. **Write the PRD** — follow the template structure exactly. Use the example as a quality bar for tone, depth, and specificity.
4. **Save as a Markdown file** — output to `/mnt/user-data/outputs/<feature-name-kebab-case>_PRD.md`.
5. **Present the file** — use `present_files` to share it with the user.

## Template Rules

- **Problem**: State the current limitation concisely. Use a numbered list if there are multiple distinct problems. Be specific — name the exact friction, not a vague complaint. Include which user segment is impacted and how severely — if this is not clear from the user's input, ask. Do not invent it.

- **Customer Insights**: Two subsections:
  - `#### Available Data` — evidence already in hand: results of data analysis, surveys, qualitative feedback from interviews, direct user feedback, or observations about how the current solution works. Must never duplicate what is already described in Problem.
  - `#### Open Questions & Hypotheses` — genuine unknowns to validate. These should be things that are actually uncertain, not restatements of the problem or made-up content to fill space.

- **Solution**: Three subsections — `### Now` (MVP scope, mandatory), `### Next` (follow-on, mandatory), and `### Later` (optional — only include when there is genuinely relevant future scope worth capturing). Use bullet points. Be concrete about what ships in each phase.

- **Design**: Describe UI/UX behaviour, not visual style. Cover the key screens and states (empty state, main view, interactions).

- **Dev**: List the data model, API endpoints, and any integration notes. Use inline code formatting for entity fields and routes.

- **Metrics**: Two groups:
  - `#### Main Metric` — the primary success indicator (e.g. adoption rate, usage frequency, churn). One metric, clearly defined.
  - `#### Instrumental Metrics` — secondary signals that help diagnose what's driving (or not driving) the main metric (e.g. click-through rate, time-to-action). Keep to 2–4.

- **Launch**: Default structure is Beta → Production. Each phase should have a clear purpose. Only deviate from this structure if the user specifies a custom launch plan.

## Quality Bar

Read `references/prd-example.md` to calibrate:
- Problems are concrete and observable, not abstract
- Available Data in Customer Insights is evidence-based, not repeated from Problem
- Open Questions are genuinely uncertain — not invented to sound thorough
- Solution scope is realistic; Later is only present when warranted
- Main metric is singular and tied directly to the problem
- Instrumental metrics explain the main metric, not replace it
