---
name: user-interview-transcription
description: >
  Use this skill whenever a user uploads or pastes a transcript from a user research
  or UX interview and wants it cleaned up, reformatted, or summarized. Triggers include:
  any mention of "interview transcript", "clean up this transcript", "fix this transcription",
  "summarize this interview", uploading .txt / .srt / .vtt / .docx files described as
  interview recordings or transcripts, or asking for insights from a user interview.
  Also trigger when the user mentions "user research", "UX interview", "participant",
  or "respondent" alongside any kind of raw text or file. Use this skill even if the
  user only asks for one of the two outputs (clean transcript OR summary) — always
  offer both.
  The summary covers: overall sentiment, key themes & insights, and pain points.
  Quotes are embedded directly inside the bullet they support (pain point or insight)
  as evidence — never collected in a standalone "Notable Quotes" section.
---

# User Interview Transcription & Summary Skill

This skill takes a raw or auto-generated transcript from a UX / user research interview
and produces two outputs:
1. **A clean, readable transcript** with speakers labelled as Interviewer / Participant
2. **A structured research summary** covering themes, pain points, notable quotes, and sentiment

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

Output as a `.txt` or `.docx` file (offer the user their preferred format; default to `.docx`
as it's easier to share and annotate). Use the docx skill if creating a Word document.

---

## Step 4 — Produce the Research Summary

Structure the summary as follows. Keep it concise but substantive — this is a research
artefact that a product team will actually use.

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

## Key Themes & Insights
[3–6 bullet points. Each should be a meaningful insight, not just a topic label.
Good: "Participant relies heavily on workarounds because the core feature feels unreliable"
Bad: "Feature reliability"
Where a quote sharpens an insight, embed it directly in the bullet as evidence:
- Insight description. > "Quote illustrating it." — Speaker]

---

## Pain Points
[Bulleted list of specific frustrations, blockers, or confusing moments.
Where a quote captures the pain point particularly well, embed it directly in the bullet:
- Pain point description. > "Quote illustrating it." — Speaker]

---

```

Output the summary as a separate `.docx` file, or inline in chat if the user prefers.

---

## Step 5 — Deliver the Outputs

Always produce both outputs unless the user explicitly asked for only one.

**File naming format:** `DD-MM-YY_FirstnameLastname_transcript.docx` and `DD-MM-YY_FirstnameLastname_summary.docx`
- Use the date of the interview if known, otherwise today's date
- Use the interviewee's name (the participant, not the interviewer)
- Example: `16-04-25_AliFireouzbakhsh_transcript.docx` and `16-04-25_AliFireouzbakhsh_summary.docx`

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
