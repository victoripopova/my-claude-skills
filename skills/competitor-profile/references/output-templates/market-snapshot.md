# Market Snapshot Template

**Purpose:** Feed into board decks, investor updates, and strategy memos.
**Consumer:** PM or founder who will author the final narrative.
**Format:** Dense, structured, extractable. No prose paragraphs. Data + source + date.
**Target length:** 600–900 words of content. Every field gets a confidence tag.

Confidence tags:
- **[H]** = High — confirmed from primary source (company site, official filing, press release)
- **[M]** = Medium — inferred from secondary source (analyst, review site, news article)
- **[L]** = Low — single unverified source, or data older than 12 months

---

## [COMPETITOR NAME] — Market Snapshot

*Profile generated: [DATE]*
*Covers activity: [DATE RANGE — e.g. "Jan 2024 – Jan 2025"]*

---

### 1. Company Basics

| Field | Value | Confidence | Source | Date |
|-------|-------|------------|--------|------|
| Founded | | | | |
| HQ | | | | |
| Funding stage | | | | |
| Total raised | | | | |
| Last round | | | | |
| Lead investors | | | | |
| Headcount (est.) | | | | |
| Headcount trend | Growing / Stable / Shrinking | | | |
| Ownership type | VC-backed / Bootstrapped / PE / Public | | | |
| CEO | | | | |

---

### 2. Product

**Value proposition** [H/M/L]:
> [Their homepage headline or closest equivalent — verbatim, in quotes, with URL]

**Pricing model** [H/M/L]:
> [Per seat / Usage-based / Enterprise contract / Freemium — and what the entry tier costs if known]

**Key features** [H/M/L]:
- [Feature 1]
- [Feature 2]
- [Feature 3]
- [Feature 4]

**Enterprise readiness signals** [H/M/L]:
- [ ] SOC2 certified
- [ ] SSO / SAML
- [ ] Admin controls
- [ ] Audit logs
- [ ] SLA / uptime guarantees

**Key integrations** [H/M/L]:

For each integration, specify the type — never just list a name.
Format: `Tool name — integration type (source)`

Types: Native two-way sync / One-way export / API connection / Middleware only / Vendor-claimed only

Example:
- Salesforce — one-way data export via API (vendor docs, Jan 2025)
- HubSpot — one-way data export via API (vendor docs, Jan 2025)
- Zapier — middleware connector, 12 zaps available (zapier.com, Jan 2025)

**Mobile apps** [H/M/L]:

- iOS: [Confirmed via App Store listing / Not found / Vendor-claimed only] — link + last update date
- Android: [Confirmed via Play Store listing / Not found / Vendor-claimed only] — link + last update date

**Recent product moves (last 6 months)** [H/M/L]:
- [Announcement 1 — date]
- [Announcement 2 — date]

---

### 3. Go-to-Market

**Target buyer** [H/M/L]:
> [Job title(s), seniority, department — sourced from case studies or G2 reviewer profiles]

**Target company profile** [H/M/L]:
> [Size range + verticals — e.g. "100–2000 employee SaaS companies, strong in fintech and HR tech"]

**Sales motion** [H/M/L]:
> [PLG / Outbound / Channel / Hybrid — and evidence for the inference]

**Named customers** [H/M/L]:
> [List up to 10 logos they display publicly — with source URL]

**Marketing channels** [M/L]:
> [e.g. "Heavy SEO, active LinkedIn, quarterly webinars, no paid search visible"]

---

### 4. Market Perception

**What they're known for** [M]:
> [2–3 sentence synthesis of consistent praise themes across reviews]

**Consistent complaints** [M]:
> [2–3 sentence synthesis of recurring issues — focus on 3-star reviews]

**Review volume and score** [H]:
> G2: [X reviews, Y.Y/5.0 as of DATE]
> Capterra: [X reviews, Y.Y/5.0 as of DATE]

---

### 5. Momentum (last 6–12 months)

Summarize only material changes. Skip rows where no credible signal was found.
Every row must include a live source URL — no row is complete without one.

| Signal type | Detail | Date | Confidence | Source |
|-------------|--------|------|------------|--------|
| Funding | | | | [Link]() |
| Product launch | | | | [Link]() |
| Geographic expansion | | | | [Link]() |
| Executive change | | | | [Link]() |
| Partnership | | | | [Link]() |
| Pricing change | | | | [Link]() |
| M&A activity | | | | [Link]() |
| Negative news | | | | [Link]() |

**Funding deep-dive** *(populate only if a funding event was found)*

- **Round size & structure:** [e.g. $6M Series A1, co-led by X and Y]
- **Stated use of proceeds:** [e.g. US market expansion, product hiring — from press release or CEO quote]
- **Investor thesis / why now:** [Any stated rationale from investor or company — quote if available, with URL]
- **Total raised to date:** [Cumulative figure]
- **Implied valuation signal:** [Only if disclosed or leaked — mark [L] if inferred]

**Job openings signal** *(run a fresh search at time of profile generation)*

Hiring pattern reveals strategic intent. Check their careers page and LinkedIn Jobs.

| Role | Department | Signal interpretation |
|------|------------|----------------------|
| [e.g. Enterprise AE x3] | Sales | Upmarket motion, targeting larger deals |
| [e.g. DevRel Engineer] | Marketing | PLG push, developer ICP |
| [e.g. Head of EMEA] | GTM | Geographic expansion |

- **Overall hiring posture:** [Growing / Flat / Contracting — based on open role count vs. 3 months ago if detectable]
- **Notable gaps:** [Roles you'd expect but don't see — e.g. no data/ML roles despite AI claims]
- Source: [careers URL] — retrieved [DATE]

**LinkedIn activity snapshot** *(check company page + 1–2 key exec pages)*

*Company page:*
- Posting cadence: [e.g. 3–4x/week / sporadic / inactive]
- Dominant themes: [e.g. product launches, customer stories, hiring, thought leadership]
- Recent post that stands out: [Title or summary + URL + date]

*Key exec(s):*
- [Name, Title]: [Posting themes + frequency + any notable recent post with URL]
- [Name, Title]: [Posting themes + frequency + any notable recent post with URL]

> ⚠️ LinkedIn data is inherently [M] confidence — content is curated by the company/individual.
> Note what they're *choosing* to amplify, not what it proves.

---

### 6. Open Questions

Fields that could not be populated with sufficient confidence.
These are the gaps — useful for knowing what further research to commission.

- [ ] [Field 1] — could not find credible source
- [ ] [Field 2] — only found data older than 12 months
- [ ] [Field 3] — conflicting sources, needs verification

---

### 7. Analyst Notes

*Optional — only include if the PM/author adds these manually after review.*

> [Key implication for your positioning or roadmap — written by the human, not generated]
