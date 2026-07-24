---
name: interview-to-notion-pipeline
description: "Use whenever the user wants a new user-research interview taken all the way to Notion in one go — not just cleaned up locally. Triggers: uploading/pasting an interview transcript together with phrases like \"add this to Interview Hub\", \"post this to Notion\", \"run this through to Notion\", \"same as before but put it in Notion\", or any request that combines interview transcription with Notion posting. This is a superset of the user-interview-transcription skill: it calls that skill for the clean transcript and structured summary, then additionally creates the Notion interview page (with transcript attached and summary as page content) and adds only the UX Friction / Feature Request / Idea entries to the Ideas & Friction database. Bugs and Praise stay in the interview page only — never in the database. Tags are never auto-assigned; that field is left blank for manual assignment."
---

# Interview → Notion Pipeline

This skill takes a raw interview transcript all the way from raw text to a fully
populated Notion Interview Hub entry. It is a wrapper around the
`user-interview-transcription` skill — always read that skill's SKILL.md too, since
it defines how the clean transcript and summary are actually built. This skill only
adds the Notion posting steps on top.

---

## Fixed destinations

These are stable for this workspace — don't search for them each time, but do
confirm with a quick `fetch` if either seems to have moved or been renamed:

- **Interview Hub page** (parent for new interview pages): `3a6fc493-c474-80b2-9963-d0423b5225fb`
- **Ideas & Friction database** data source: `collection://bdc0c024-49d8-41f0-a0fd-5bbd00ecada3`

If the person mentions a different hub/database by name, search for it instead of
assuming these IDs still apply.

---

## Step 1 — Run the transcription skill

Follow `user-interview-transcription` SKILL.md in full:
1. Read the input, identify speakers.
2. Produce the clean transcript (`.txt` content — don't create the local file yet
   if it's only going to Notion; just hold the cleaned text in memory).
3. Produce the structured summary (Overall Sentiment, Insights with Type/Evidence/
   Frequency/Context/Details, User Context).

Do not skip or shortcut this step — the Notion page content in Step 2 is exactly
this summary, and the database rows in Step 3 are pulled directly from the Insights
section this step produces.

---

## Step 2 — Create the Notion interview page FIRST

Order matters: the interview page must exist before Step 3, because each database
row needs a real link to it.

1. Upload the clean transcript as a Notion attachment (`notion-create-attachment`,
   plain text, filename pattern `DD-MM-YY_ParticipantName_transcript.txt`).
2. Create the page under the Interview Hub page ID above, titled
   `Participant Name — DD Month YYYY` (participant only, not the interviewer —
   Victoria is the constant interviewer across this workspace and isn't
   differentiating information).
3. Page content = the summary from Step 1: link to the attached transcript file at
   the top, then Overall Sentiment, Insights (all of them — Bug and Praise entries
   stay here even though they won't go to the database), then User Context.
4. Capture the resulting page URL — it's needed for every database row in Step 3.
5. Place the new page at the top of the interview list on the Interview Hub page,
   not the bottom — the list should always read most-recent-first. If the new page
   was appended at the end by default, move it above the existing interview pages
   before moving on to Step 3.

---

## Step 3 — Add ONLY UX Friction / Feature Request / Idea rows to the database

For each Insight from Step 1 whose Type is `UX Friction`, `Feature Request`, or
`Idea` — and only those — create a row in the Ideas & Friction data source with:

| Property | Value |
|---|---|
| Idea Name | The insight's short title |
| Type | UX Friction / Feature Request / Idea (never Bug or Praise here) |
| Idea Description | The insight's Details, condensed to 1–3 sentences if needed |
| Interview Link | The URL of the page created in Step 2 |
| Date | The interview date, as a real Date property |

**Never set Tags.** Leave that field completely absent from the properties payload
— don't guess a value, don't reuse an existing tag "because it looks close enough,"
and don't invent a new one. Tagging requires comparing this insight against every
other row already in the database to spot cross-interview patterns, which a
single-interview run can't reliably do. That judgment call belongs to the person,
always, with no exceptions — even if an existing tag seems like an obvious fit.

Bug and Praise insights are NOT added to this database. They exist only in the
Notion interview page body from Step 2. Don't create rows for them, and don't
mention them again once Step 2 is done — no separate "heads up, there was a bug"
note in chat, since that was the person's explicit preference.

---

## Step 4 — Report back concisely

After both the page and the database rows are created:
- Link the new interview page.
- State how many rows were added to Ideas & Friction, broken down by Type.
- Do NOT list bug/praise items again in chat — they're already visible in the page.
- One line highlighting the most interesting insight, same as the standalone
  transcription skill does.

---

## Edge cases

| Situation | How to handle |
|---|---|
| Interview Hub page ID or database ID has changed | Search for "Interview Hub" and "Ideas & Friction" by name, confirm with the person before proceeding on new IDs |
| An insight's Type is ambiguous between two of the three database-eligible types | Pick the closer fit and note the ambiguity briefly in the Idea Description rather than skipping the row |
| Multiple interviews submitted at once | Run the full pipeline once per interview — separate pages, separate row batches, never merged |
| The transcription skill flags something as Uncategorized | Do not add it to the database (it's not Bug/Praise but it's also not cleanly UX Friction/Feature Request/Idea) — leave it in the page only, and mention the ambiguity to the person in Step 4 so they can decide if it belongs in the database manually |
