# Search Query Templates

Use these templates by substituting `[competitor]` with the actual company name.
Keep queries short (3–6 words). Do not use quotes, site: operators, or dashes
unless specifically noted — they reduce result breadth.

---

## 2a. Company Foundation

```
[competitor] funding crunchbase
[competitor] total raised investors
[competitor] employees headcount 2024
[competitor] CEO founder leadership team
[competitor] headquarters location founded
[competitor] PE acquisition OR [competitor] acquired by
```

Secondary sources to check directly if search yields thin results:
- crunchbase.com/organization/[competitor-slug]
- linkedin.com/company/[competitor-slug]

---

## 2b. Product Surface

```
[competitor] features pricing plans
[competitor] product overview
[competitor] pricing tiers
[competitor] enterprise security SOC2 SSO
[competitor] product updates 2024
[competitor] new features release
[competitor] integrations API
[competitor] changelog
```

Check directly:
- [competitor].com/pricing
- [competitor].com/features OR /product
- [competitor].com/changelog OR /releases

**Integration depth — always verify beyond the vendor's integrations page:**

The vendor's own integrations page will always make integrations sound more capable
than they are. For any named integration, run secondary verification:

```
[competitor] [integration-name] how it works
[competitor] [integration-name] API documentation
[competitor] [integration-name] marketplace listing
[integration-name] app marketplace [competitor]
```

Classify each integration found as one of:
- **Native two-way sync** — data flows both directions automatically
- **One-way export** — data pushes out from competitor into the other tool
- **API connection** — requires developer setup; not out-of-the-box
- **Middleware/Zapier** — connection exists only via third-party automation tool
- **Vendor-claimed only** — mentioned on their site but no independent confirmation found

Never write "integrates with X" in the output — always write the integration type.

**Mobile apps — verification required:**

Do not rely on vendor claims or secondary mentions for mobile app existence.
For any claimed mobile app, verify directly:
```
[competitor] app site:apps.apple.com
[competitor] app site:play.google.com
```
- iOS [H] = confirmed listing on apps.apple.com with active maintenance signals
- Android [H] = confirmed listing on play.google.com
- If only found via vendor claim or user mention = [M], note "not independently verified via store listing"

---

## 2c. ICP and Go-to-Market

```
[competitor] case studies customers
[competitor] customer logos
[competitor] target market OR ideal customer
[competitor] for [your category] companies
site:g2.com [competitor] reviews (use site: only here)
[competitor] partner program channel
[competitor] blog content marketing
```

Check directly:
- [competitor].com/customers OR /case-studies
- g2.com/products/[competitor-slug]/reviews (filter by role/company size)

---

## 2d. Market Perception

```
[competitor] reviews complaints
[competitor] vs [your product] reddit
[competitor] problems issues users
[competitor] support quality
```

For G2/Capterra: search for 2–3 star reviews specifically.
Filter by "most recent" not "most helpful" — recency matters more for board narrative.

---

## 2e. Recent Activity (date-scoped)

Use date filters in your search tool when available. Target last 6–12 months.

```
[competitor] funding 2024
[competitor] product launch 2024
[competitor] new feature announcement
[competitor] executive hire OR departure 2024
[competitor] partnership announcement 2024
[competitor] pricing change 2024
[competitor] layoffs OR restructuring 2024
[competitor] acquisition 2024
```

**Funding deep-dive** — run these if a funding event is found:

```
[competitor] funding use of proceeds
[competitor] Series [X] investor thesis
[competitor] CEO funding announcement quote
[competitor] valuation 2024
```

Fetch the full press release or TechCrunch/Bloomberg article, not just the snippet.
Look for: stated use of proceeds, investor rationale, CEO quote on strategy.

---

## 2f. Job Openings (hiring intent signals)

Job postings are one of the highest-signal sources for strategic intent.
Always run at time of profile generation — postings change weekly.

```
[competitor] jobs hiring 2024
[competitor] open roles careers
[competitor] site:linkedin.com/jobs [competitor]
[competitor] site:greenhouse.io OR lever.co OR ashbyhq.com
```

Check directly:
- [competitor].com/careers OR /jobs
- linkedin.com/company/[competitor-slug]/jobs

Interpret patterns, not just counts:
- Enterprise AE hiring → upmarket motion
- DevRel / developer advocate → PLG push
- Regional leads (EMEA, APAC) → geographic expansion
- Data / ML engineers → AI product investment
- No CS/support roles despite growth → potential churn risk signal

Record: total open roles, top 3–5 role clusters, and any notable gaps.

---

## 2g. LinkedIn Activity

Check the company page and 1–2 key exec profiles (CEO + CPO or CRO if findable).

```
[competitor] linkedin company page
[competitor] CEO linkedin posts
[competitor] CPO OR CRO linkedin
```

Fetch directly:
- linkedin.com/company/[competitor-slug] (posts tab)
- linkedin.com/in/[ceo-slug] (activity tab)

For each profile note:
- Posting frequency (posts/week approx)
- Dominant content themes (product, culture, customers, thought leadership, hiring)
- Any post in the last 30 days that signals strategy or momentum — capture URL + summary

> LinkedIn content is [M] at best — treat as narrative signal, not confirmed fact.

If standard queries return thin results (private company, small market):

```
[competitor] interview OR podcast CEO
[competitor] press release
[competitor] job postings (signals: growth areas, tech stack, target markets)
[competitor] conference presentation OR webinar
```

Job postings are underrated signal sources. A company hiring 10 enterprise AEs
while also posting 5 DevRel roles signals a PLG-to-enterprise motion shift.
