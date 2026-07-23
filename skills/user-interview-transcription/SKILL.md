---
name: user-interview-transcription
description: "Use whenever a user uploads or pastes a transcript from a user research/UX interview and wants it cleaned up, reformatted, or summarized. Triggers: \"interview transcript\", \"summarize this interview\", uploaded .txt/.srt/.vtt/.docx interview recordings, or requests for insights from a user interview — also \"user research\", \"UX interview\", \"participant\", \"respondent\" alongside raw text/files. Always produce both outputs even if only one is requested. Covers one interview at a time. Summary includes: sentiment, a classified Insights section (Type: Bug/UX Friction/Feature Request/Idea/Praise/Uncategorized; Evidence: Observed/Stated; plus Frequency and Context), and a User Context section for background facts. Quotes go inline as evidence, never in a separate list."
---

# User Interview Transcription & Summary Skill

This skill takes a raw or auto-generated transcript from a UX / user research interview
and produces two outputs:
1. **A clean, readable transcript** with speakers labelled as Interviewer / Participant
2. **A structured research summary** covering sentiment, classified & evidence-tagged insights, and user context

---

## Step 1 — Read the Input

Accept any of these input formats:
- Uploaded `.txt`, `.srt`, `.vtt`, `.docx` file → read it (use the file-reading skill if needed)
- Pasted raw text directly in chat
- A mix (e.g. user pastes messy auto-generated captions)

If the file format is unclear, check `/mnt/user-data/uploads/` and use the file-reading skill
to extract the text content before proceeding.

---

## Step 2 — Identify Speakers

Auto-generated transcripts often have no speaker labels, wrong labels, or timestamps mixed in.

Your job:
- **Detect the interviewer** — typically the one asking questions, rarely sharing personal
  experiences, using phrases like "Can you tell me...", "What do you think...", "How did that make you feel..."
- **Detect the participant** — the one being interviewed, sharing experiences, opinions, stories
- If there are multiple participants (e.g. a group session), label them Participant 1, Participant 2, etc.
- If speaker identity is truly ambiguous, label as Speaker A / Speaker B and note this to the user

---

## Step 3 — Produce the Clean Transcript

Format rules:
- Remove timestamps entirely (unless the user asks to keep them)
- Remove filler words sparingly — keep "um", "uh", "like" only if they meaningfully affect tone;
  remove excessive repetition (e.g. "I mean, I mean, I mean")
- Fix obvious transcription errors (e.g. "I use the app to by groceries" → "buy groceries")
  but do NOT paraphrase or change meaning — preserve the participant's voice
- Label every speaker turn clearly:

```
Interviewer: Can you walk me through the last time you used the app?

Participant: Yeah, so it was last Tuesday. I was trying to, uh, find the settings menu
and I just couldn't figure out where it was. It felt really buried.
```

- Use a blank line between speaker turns
- If the transcript is very long (>30 minutes of speech), split into logical sections with
  a simple heading like `--- Section 1 ---` roughly every 10–15 minutes of content

Output as a `.txt` or `.docx` file (offer the user their preferred format; default to `.txt`
as it's easier to share and annotate). Use the docx skill if creating a Word document.

---

## Step 4 — Produce the Research Summary

Structure the summary as follows. Keep it concise but substantive — this is a research
artefact that a product team will actually use. This summary covers a single interview only;
cross-interview aggregation happens in a separate downstream skill, not here.

```
# Interview Summary
**Date**: [if known]
**Participant**: [anonymised label or first name if provided]
**Duration**: [approx, if known]

---

## Overall Sentiment
[1–2 sentences: was the participant broadly positive, frustrated, neutral, mixed?
What was the dominant emotional tone of the session?]

---

## Insights

[One entry per distinct insight — a bug, a friction point, a feature request, or praise.
Each entry always leads with Type, then Evidence, in that order, followed by Frequency
and Context. Keep entries tight — this is a scanning document, not prose.]

### [Short, specific insight title]
- **Type:** Bug / UX Friction / Feature Request / Idea / Praise / Uncategorized (see rules below)
- **Evidence:** Observed (demonstrated live in the session, e.g. on a screen share) /
  Stated (self-reported by the participant, not directly witnessed)
- **Frequency:** [how often this happens if the participant gave any indication — "every
  Friday," "once, no example given," "daily," "unknown/not stated" — never invent a frequency]
- **Context:** [any situational detail that helps explain when/where/how this happens —
  e.g. "done at home in the evening," "only for well-known repeat clients," "during a
  weekly batch session." Omit if the participant gave none.]
- **Details:** [the insight itself in 1–3 sentences, in your own words. Embed a quote
  inline only if it sharpens or evidences the point: "...description. > 'Quote.' — Speaker"]

Repeat the block above for each insight. Order entries by how much weight they'd carry in a
prioritization conversation, not by when they came up in the interview.

**Classifying Type:**
- **Bug** — something in the product is broken or behaving unintentionally (confirmed or
  strongly implied, e.g. a search that used to work and now doesn't, a missing/incorrect field)
- **UX Friction** — the product works as designed, but it costs the participant real effort,
  confusion, or a workaround
- **Feature Request** — the participant wants something that doesn't exist yet, and asked
  for it directly or clearly implied a specific ask
- **Idea** — a *hidden* opportunity you're inferring on the participant's behalf: they never
  asked for a feature, but something they said reveals a gap or priority the product could
  address. Always name the exact statement it's inferred from, and be explicit this is your
  inference, not their request. Example: a participant says the first thing they need before
  a visit is the contact person's name — they never asked for it to be shown upfront, but that
  reveals a candidate feature (surface the contact person prominently). This differs from
  Feature Request in evidentiary weight: a Feature Request is something the participant asked
  you to build; an Idea is something you noticed on their behalf.
- **Praise** — something is explicitly working well or better than before
- **Uncategorized** — use this rather than forcing a fit; briefly note why it doesn't
  cleanly fit the other five

---

## User Context
[Bulleted list of factual, situational information about how this participant works, that
isn't itself a request or a complaint — it's background that helps interpret everything
above. Examples: account/client volume ("~605 accounts"), a habitual workflow pattern
("batches appointment closing every Friday afternoon"), tool habits ("does all client email
through Outlook, not the in-app client"), role or environment details. If the participant
didn't share much of this, keep the section short rather than padding it.]

---

```

Output the summary as a separate markdown file, or inline in chat if the user prefers.

---

## Step 5 — Deliver the Outputs

Always produce both outputs unless the user explicitly asked for only one.

**File naming format:** `DD-MM-YY_FirstnameLastname_transcript.txt` and `DD-MM-YY_FirstnameLastname_summary.md`
(default formats — swap to `.docx` only if the user asks for Word specifically)
- Use the date of the interview if known, otherwise today's date
- Use the interviewee's name (the participant, not the interviewer)
- Example: `16-04-25_AliFireouzbakhsh_transcript.txt` and `16-04-25_AliFireouzbakhsh_summary.md`

Present them clearly:
- "Here's your **clean transcript** → [file]"
- "Here's your **research summary** → [file or inline]"

Then briefly highlight (in 2–3 sentences in chat) the single most interesting or surprising
thing from the interview — this helps the user quickly orient before they read the full summary.

---

## Edge Cases

| Situation | How to handle |
|---|---|
| Only one speaker detected | Ask the user to confirm before proceeding |
| Transcript is in another language | Clean and summarise in that language; note this to the user |
| Multiple interviews in one file | Split into separate summaries, one per interview |
| Very short transcript (<5 min) | Still produce both outputs; summary will naturally be shorter |
| Heavily redacted or anonymised | Respect existing anonymisation; don't try to re-identify |
| Poor audio quality / many [inaudible] markers | Flag these in the clean transcript with `[inaudible]`; don't guess |