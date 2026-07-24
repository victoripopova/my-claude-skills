---
name: jira-to-notion-pipeline
description: "Use whenever the user has a Jira CSV export (support tickets, e.g. from the DOC project) and wants it triaged and pushed to Notion — not just cleaned up locally. Triggers: uploading a Jira export together with phrases like \"add these Jira tickets to Notion\", \"run this Jira CSV through to the Ideas database\", \"categorize these tickets and push feature requests to Notion\", \"same as before but from a Jira export\", or any request that combines a Jira CSV with populating the Ideas & UX Friction database. Reduces a full Jira export (270+ columns) down to the essentials, classifies each ticket/insight as Feature Request / UX Friction / Bug / Uncategorized (no Idea type — Jira tickets are reported issues, not interview inferences), and pushes the Feature Request AND UX Friction items into Notion. Bugs and Uncategorized (operational/admin requests) are triaged and reported in chat but never written to Notion."
---

# Jira → Notion Pipeline

Takes a raw Jira CSV export all the way from a full ticket dump to new rows in the
Ideas & UX Friction Notion database. **Feature Request and UX Friction** items get
pushed to Notion; Bug and Uncategorized do not. This matches the scope of the
sibling `interview-to-notion-pipeline` skill minus the Idea type (Jira tickets are
reported by someone, so there's no "agent's own inference" category the way there
is for interviews). Read that skill's SKILL.md for background on the destination
database if anything here is unclear.

---

## Fixed destinations

Stable for this workspace — don't search for them each time, but confirm with a
quick `fetch` if either seems to have moved:

- **Ideas & UX Friction database** data source: `collection://bdc0c024-49d8-41f0-a0fd-5bbd00ecada3`
- **Jira base URL** for ticket links: `https://datlinq.atlassian.net/browse/{Issue key}`
  (e.g. `DOC-11208` → `https://datlinq.atlassian.net/browse/DOC-11208`). If the
  CSV's tickets don't match this domain/project pattern, confirm the right base
  URL with the user before generating links.

---

## Step 1 — Read the CSV and reduce columns

Jira exports from this workspace commonly carry 270+ columns because multi-value
fields (Comment, Attachment, Sprint, Watchers, Labels) are exported as one column
per instance (`Comment`, `Comment.1`, `Comment.2`, ... `Comment.24`, etc.).

Reduce to just what's needed:

| Keep | Why |
|---|---|
| `Issue key` | Required — this is what builds the Jira link (e.g. `DOC-11208`), NOT `Issue id` (the numeric internal id) |
| `Summary` | Primary signal for what the ticket is about, often names the client |
| `Status` | Useful context, not written to Notion |
| `Created` | Becomes the Notion `Date` property |
| `Updated` | Optional context, not written to Notion |
| `Description` | Main body — where most classification signal and client identity lives |
| `Comment` (all instances merged) | Merge every `Comment`, `Comment.1`, `Comment.2`, ... column per row into one field, dropping blanks, joined with `\n\n---\n\n`. This is often where the actual ask gets clarified or resolved. |

Drop everything else (Attachment, Sprint, Watchers, Labels, all other Custom
fields) unless the user specifically asks for one.

If the user has already handed you a reduced CSV (e.g. from a prior step in the
same conversation), skip straight to Step 2.

---

## Step 2 — Classify each ticket

Each row may contain **one or more distinct insights** — a single ticket can bundle
a bug report and a separate feature ask, or two unrelated feature requests. Split
these into separate insight entries rather than forcing one classification per row.

**Classifying Type** (no "Idea" type here — that's reserved for the interview
pipeline, where it marks the agent's own inference; Jira tickets are reported by
someone, so everything here is either a concrete complaint or a concrete ask):

- **Bug** — something is broken, behaving unintentionally, or regressed from
  previously-working behavior (confirmed or strongly implied) — a UI rendering
  issue, a missing translation, a feature that "used to work and now doesn't,"
  a sync/data-pipeline failure, an integration error.
- **UX Friction** — the product works as designed, but the process is confusing,
  opaque, or requires a workaround. No concrete "build this new thing" ask —
  more like "I don't understand how X works" or "this is hard to find/do."
- **Feature Request** — the reporter (or someone relaying a client's ask, e.g. a
  CS lead forwarding a customer email) explicitly wants a specific capability
  that doesn't exist yet, with a clear, actionable ask.
- **Uncategorized** — internal/operational requests that aren't product feedback
  at all: API key creation, demo/test environment setup, one-off data fixes or
  restores, access requests, etc.

**Ambiguous cases:** if an insight sits between two types, pick the closer fit and
note the ambiguity briefly in the Idea Description — don't skip it or force a
false-confidence pick.

**Feature Request and UX Friction items move on to Step 3.** Bug and
Uncategorized items are still worth surfacing to the user (see Step 4), but no
Notion row gets created for them.

---

## Step 3 — Push Feature Requests and UX Friction to Notion

For each insight classified as **Feature Request** or **UX Friction**, create a
row in the Ideas & UX Friction data source with:

| Property | Value |
|---|---|
| Idea Name | Short, specific title for the request/friction point |
| Type | `Feature Request` or `UX Friction`, matching Step 2's classification (this pipeline never writes Bug/Idea rows) |
| Idea Description | The request/friction condensed to 1–3 sentences, in your own words |
| Client | The client/company name, inferred from ticket content — see below |
| Link | `https://datlinq.atlassian.net/browse/{Issue key}` |
| Date | The ticket's `Created` date, as a real Date property |

**Finding the Client:** Jira's own `Custom field (Customer)` column is almost
always empty in this export — don't rely on it. Instead infer the client from:
- The `Summary` line — often has the client name in parentheses at the end (e.g.
  `"DOC: Vraag ... (Van Geloven)"`) or as a prefix (`"Walraven - ..."`, `"Prod
  wish Lavazza - ..."`)
- Email signature blocks inside `Description` (company name, sender domain)
- CS agent phrasing inside `Comment` (e.g. "request from Thomas for VHC
  Actifood")

If the client genuinely can't be determined from the ticket text, leave the
Client property blank rather than guessing, and flag that ticket to the user in
Step 4.

**Date parsing:** `Created` is in `DD/MM/YY H:MM AM/PM` format (day-month-year,
not month-day-year) — confirm this before batch-converting many rows, since
misreading the order will silently shift every date.

**Never set Tags.** Same rule as the interview pipeline: leave that field
completely absent from the properties payload. Tagging requires comparing
against every existing row to spot cross-ticket patterns, which is a judgment
call that belongs to the person.

**Avoiding duplicates:** if this CSV might overlap with a previous run (e.g. the
user re-exports an updated Jira view), query the data source for existing `Link`
values before creating rows, and skip any ticket whose Jira link is already
present.

---

## Step 4 — Report back concisely

After Notion rows are created:
- State how many rows were added, broken down by Type (Feature Request / UX
  Friction)
- Give a one-line count breakdown of everything else found: e.g. "Also found 8
  Bugs and 2 Uncategorized items — not added to Notion since they're outside
  this pipeline's scope." Don't fully write these up unless the user asks — a
  count is enough visibility.
- Note any ambiguous Type calls from Step 2 in one line each.

---

## Edge cases

| Situation | How to handle |
|---|---|
| CSV is missing `Issue key` or has a different comment-column naming pattern | Adapt column detection (look for the actual column names present) and confirm with the user before proceeding if the structure is materially different |
| A ticket bundles a Feature Request/UX Friction point with a Bug | Split into separate insights (Step 2); only the Feature Request/UX Friction insight(s) get a Notion row |
| Ideas & UX Friction database ID has changed | Search for "Ideas & UX Friction" by name, confirm the new ID with the person before proceeding |
| Jira domain isn't `datlinq.atlassian.net` | Confirm the correct base URL with the user rather than assuming |
| User wants Bugs pushed too, for this run | That's a valid one-off ask — do it, but note it's outside this skill's default scope rather than silently expanding it every time |
| Very large CSV (100+ rows) | Process and classify in batches, confirm intermediate progress with the user if it's a large enough job to warrant it |