---
name: competitor-profile
description: >
  Build a structured, comprehensive competitor profile from public web sources.
  Use this skill whenever the user asks to research a competitor, build a competitive
  profile, analyze a rival company, or gather intelligence on a competing product or
  vendor — even if they don't use the word "competitor". Trigger phrases include:
  "tell me about [company]", "what do we know about [company]", "research [company]",
  "competitive analysis of [company]", "who is [company] and what do they do",
  "I need a profile on [company]". Always use this skill for B2B competitor research tasks.
---

# Competitor Profile Skill

Builds a structured, board/investor-grade competitor baseline from public web sources.
Output is designed to feed into slide decks, memos, or strategy documents — dense,
timestamped, and extractable. Not a narrative; a research dossier.

> ⚠️ **MANDATORY: This skill requires live web search.**
> Every data point in the output must come from a live web_search or web_fetch call
> made during this session. Training data is explicitly forbidden as a source for any
> output field. If web search returns no result for a field, the field must be marked
> as "Not found via live search" in Open Questions — never filled from memory.
> Begin Step 2 by running searches, not by recalling what you know.

---

## Step 0 — Intake

Before searching, confirm:

1. **Competitor name** — exact company name (and URL if known)
2. **Your product category** — used to frame relevance of features and ICP signals
3. **Output template** — which template to use:
   - `market-snapshot` — for board/investor use (feeds slide decks, memos)
   - `battlecard` — for sales use (objection handling, win/loss context)
   - `product-brief` — for PM/roadmap use (feature depth, technical signals)

If the output template is not specified, ask. Do not default silently.

> **For this skill, the primary template is `market-snapshot`.**
> Read `references/output-templates/market-snapshot.md` before beginning any search.

---

## Step 1 — Load Output Template

Read the relevant template from `references/output-templates/` before any searches.
The template defines required fields, optional fields, and confidence tagging rules.

---

## Step 2 — Search Sequence

**Use your native web_search and web_fetch tools for every search in this step.**
Do not rely on training data for any field in the output template — training data
has a knowledge cutoff and will produce stale profiles. If a search returns thin
results, run a follow-up search with a different query before accepting a gap.

For each section below:
1. Run the web_search queries listed in `references/search-queries.md`
2. Use web_fetch to retrieve full page content where snippets are insufficient
   (pricing pages, about pages, G2 review pages are always worth fetching in full)
3. **Tag every data point with its source URL and the date it was retrieved.**
4. Do not assert facts without a live source from this session.
5. If a fact cannot be verified by live search, mark it [L] and flag it in Open Questions.

**Claim evaluation rules — apply before marking anything [H] or [M]:**

- **Vendor marketing copy is not confirmation.** If the competitor's own website says
  "integrates with Salesforce," that is a claim, not a verified fact. Look for the
  actual integration documentation, API reference, or third-party marketplace listing.
  If only vendor copy is found, mark [M] and note: "vendor-claimed, not independently verified."

- **Binary facts require primary source confirmation.** For claims like "has iOS app,"
  "has Android app," "is SOC2 certified," or "offers SSO" — the only acceptable [H]
  sources are: the actual App Store/Play Store listing, the vendor's trust/security page
  with a dated certificate, or an official press release. A secondary mention (e.g. a
  review saying "I use the Android app") is [M] at most.

- **Integration depth must be specified, not assumed.** "Integration" is a spectrum.
  Always clarify: is it a native two-way sync, a one-way data export, an API connection
  requiring developer setup, or a Zapier/middleware connection? These are materially
  different capabilities. Never write "integrates with X" — always write what the
  integration actually does. See `references/search-queries.md` section 2b for
  integration depth query templates.

Run searches in this order:

### 2a. Company Foundation
Goal: establish stability, scale, and ownership context — critical for B2B/enterprise vendor evaluation.

- Funding stage, total raised, last round date, lead investors
- Headcount estimate and growth trend (last 12 months)
- Founded year, HQ location, geographic focus
- Ownership: VC-backed, bootstrapped, PE-owned, public?
- Key executives (CEO, CPO, CRO if findable)

### 2b. Product Surface
Goal: understand what they actually sell and at what price.

- Core value proposition — use web_fetch on their homepage directly; do not paraphrase from snippets
- Key features — use web_fetch on their /features or /product page; marketing copy on homepages misleads
- Pricing model: per seat, usage-based, enterprise contract, freemium?
- Pricing tiers — use web_fetch on their /pricing page; exact numbers or "contact us"
- Enterprise signals: SOC2, SSO, SAML, admin controls, audit logs — mentioned anywhere on site?
- Recent product announcements — date-filtered search, last 6 months only
- Integrations and tech stack signals — check /integrations page if it exists

### 2c. ICP and Go-to-Market
Goal: understand who they're selling to and how — highest-value section for positioning.

- Target buyer persona (job titles in case studies, testimonials, G2 reviews)
- Target company size and vertical (SMB? Mid-market? Enterprise?)
- Sales motion: PLG (self-serve trial), outbound-led, channel/partner?
- Key named customers (logos page, case studies, press releases)
- Marketing channels (SEO, paid, events, content — look at their blog cadence and LinkedIn)

### 2d. Market Perception
Goal: surface honest weaknesses — the 3-star reviews are more valuable than 5-star ones.

- G2, Capterra, or TrustRadius reviews — filter for 3-star ratings specifically
- Common praise themes (what they're known for being good at)
- Common complaint themes (what keeps coming up as missing or broken)
- How they respond to negative reviews publicly (signals support culture)
- Recent news coverage tone: positive momentum, controversy, layoffs?

### 2e. Recent Activity (last 6–12 months)
Goal: capture momentum signals for board-level narrative.

- Funding news — and if found, fetch the full press release for use of proceeds + investor rationale
- Product launches or major feature releases
- Executive hires or departures
- Partnerships or integrations announced
- Pricing changes
- Any M&A activity

### 2f. Job Openings (hiring intent)
Goal: infer strategic direction from hiring patterns.

- Fetch their live careers page at time of profile generation
- Cluster roles by department and interpret the pattern
- Note total open role count and any significant gaps

### 2g. LinkedIn Activity
Goal: understand the narrative they're actively pushing to the market.

- Company page: posting cadence and dominant themes
- CEO + 1 other exec (CPO or CRO): posting themes and any notable recent post
- Capture URLs for standout posts

> **Source link rule:** Every row in the Momentum table and every claim in sections 2e–2g
> must include a live hyperlink to the source. A source name alone (e.g. "PR Newswire") is not sufficient.

---

## Step 3 — Synthesis

After completing all searches:

1. Populate the output template fields from `references/output-templates/market-snapshot.md`
2. Tag each field with confidence: **High** / **Medium** / **Low**
   - High = confirmed from primary source fetched live this session (company site, official press release)
   - Medium = inferred from secondary source fetched live this session (analyst report, review site, news)
   - Low = single source, unverified, or could not be confirmed by live search
3. **Never populate a field from training data alone.** If live search failed to return data for a field,
   mark it [L] and move it to Open Questions. Label it explicitly: "Not found via live search."
4. Explicitly list **Open Questions** — fields that could not be populated with confidence
5. Include a **Staleness Warning** if any High-priority field returned results older than 6 months

---

## Step 4 — Output

**Output format: `.md` file only. Do NOT render the profile as an artifact or inline in chat.**

1. Write the completed profile to `/mnt/user-data/outputs/[competitor-slug]-profile.md`
   (e.g. `acme-analytics-profile.md`)
2. Use `present_files` to surface the file to the user as a downloadable link
3. After presenting the file, write a short inline summary (3–5 bullet points max)
   covering the most notable findings — funding stage, headcount, top strength,
   top weakness, and biggest momentum signal. This is the only prose that goes in chat.

Do not add narrative framing or editorial opinions to the file itself.
This is a research dossier, not a strategy memo. The user writes the story.

---

## Reference Files

- `references/search-queries.md` — templated search queries per section (load before Step 2)
- `references/output-templates/market-snapshot.md` — primary output template (load before Step 1)
- `references/output-templates/battlecard.md` — alternative template (load only if requested)
- `references/output-templates/product-brief.md` — alternative template (load only if requested)
- `assets/profile-example.md` — annotated example output (load if user asks for an example)
