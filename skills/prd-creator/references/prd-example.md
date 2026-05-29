# Notes Entity

## Problem

Reps can currently only add notes within an appointment. This creates three problems:

1. **No account-level notes** — if a rep wants to capture information about an account outside of a specific appointment, there is no way to do this. Account-level observations have nowhere to go.
2. **No overview of notes across appointments** — reviewing notes is painful. Reps must open each appointment individually to check its notes, making it impossible to get a quick overview of all notes for a company.
3. **Information gets lost** — because there is no easy way to add new information to an account, reps simply don't add it. The account ends up with incomplete context, which directly impacts the quality of AI-generated summaries and copilot insights.

## Customer Insights

- It remains an open question whether reps feel a need for standalone notes *not* tied to a specific appointment — this is a core hypothesis to validate.
- Starting with an empty "Notes" screen risks low adoption. Surfacing appointment-attached notes alongside standalone notes avoids the blank-state problem and seeds the feed immediately.

## Solution

Two types of notes exist within the Notes entity, both visible in a unified feed on the company card:

1. **Standalone notes** — created from scratch via the Notes tab → Add Note screen. Not tied to any appointment.
2. **Appointment-attached notes** — notes associated with a specific appointment. These are tagged with the appointment name, making their origin clear in the feed.

### Now
- Add a **Notes tab** to the company card
- Notes feed displays both note types in reverse-chronological order
- **Add Note screen** for creating standalone notes (free-form text input)
- Appointment-attached notes display a tag showing `[Appointment Name]`
- Notes are persistent per company

### Next
- **Voice-to-text input** on the Add Note screen to reduce friction for field reps entering notes on the go
- Notes feed into **AI chat** as additional context
- Notes surface in the **company pre-brief** to enrich AI-generated summaries

## Design

- **Notes tab** sits alongside existing tabs on the company card
- **Notes feed** renders both note types in a unified list:
  - Standalone notes: show timestamp and note body
  - Appointment-attached notes: show an appointment tag (`[Appointment Name]`) above the note body
- **Add Note screen**: minimal, full-screen text input with a voice-to-text button; no structured fields
- Empty state (before any notes exist): prompt the user to add the first note or highlights any appointment-attached notes if available

## Dev

- New `Note` entity with fields: `id`, `company_id`, `body`, `created_at`, `appointment_id` (nullable), `appointment_name` (denormalized for display), `appointment_date` (denormalized for display)
- API endpoints: `GET /companies/:id/notes`, `POST /companies/:id/notes`, `DELETE /notes/:id`
- Appointment-note association: when a note is created within an appointment context, `appointment_id` is populated automatically
- Voice-to-text: integrate device-native speech recognition (Web Speech API or equivalent mobile SDK)
- Notes feed into AI context pipeline: include company notes in the context payload sent to AI chat and pre-brief generation

## Metrics

- **Adoption rate**: % of active reps who create at least one note per week
- **Note type split**: ratio of standalone notes vs. appointment-attached notes (informs whether standalone notes address a real need)
- **AI output quality**: qualitative improvement in pre-brief relevance when notes are present vs. absent (user rating or A/B)
- **Voice-to-text usage**: % of notes created via voice input
- **Time-to-note**: average time from opening Add Note screen to saving (proxy for friction)

## Launch

- **Alpha**: internal testing with 2–3 field reps; focus on standalone vs. appointment-attached note distinction and blank-state UX
- **Beta**: rollout to a pilot team; validate whether reps feel the need for standalone notes or predominantly use appointment-attached notes
- **GA**: full rollout with voice-to-text enabled; announce in-app with a short onboarding tooltip on the Notes tab
- **Post-launch**: monitor adoption metrics for 4 weeks; decide whether to invest in standalone note discoverability or deprecate in favour of appointment-only notes based on usage data
