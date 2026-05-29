# Example: Market Snapshot — Acme Analytics

*This is a fictional annotated example showing how a completed profile should look.*
*Annotations in [brackets] explain decisions made at each field.*

---

## Acme Analytics — Market Snapshot

*Profile generated: 15 Jan 2025*
*Covers activity: Jan 2024 – Jan 2025*

---

### 1. Company Basics

| Field | Value | Confidence | Source | Date |
|-------|-------|------------|--------|------|
| Founded | 2018 | H | crunchbase.com/acme | Nov 2024 |
| HQ | San Francisco, CA | H | acmeanalytics.com/about | Jan 2025 |
| Funding stage | Series B | H | techcrunch.com/acme-series-b | Mar 2024 |
| Total raised | $47M | H | techcrunch.com/acme-series-b | Mar 2024 |
| Last round | $28M Series B | H | techcrunch.com/acme-series-b | Mar 2024 |
| Lead investors | Sequoia, Bessemer | H | techcrunch.com/acme-series-b | Mar 2024 |
| Headcount (est.) | ~180 | M | linkedin.com/company/acme | Jan 2025 |
| Headcount trend | Growing (+40% YoY) | M | linkedin.com/company/acme | Jan 2025 |
| Ownership type | VC-backed | H | crunchbase.com/acme | Nov 2024 |
| CEO | Jane Smith (co-founder) | H | acmeanalytics.com/team | Jan 2025 |

[ANNOTATION: Headcount from LinkedIn is always Medium confidence — it's self-reported
and lags reality. Note the trend is more useful than the absolute number for board narrative.]

---

### 2. Product

**Value proposition** [H]:
> "The analytics platform built for operations teams who can't wait for data." — acmeanalytics.com, Jan 2025

[ANNOTATION: Always quote their own words verbatim here. The board will recognize
marketing language and can calibrate accordingly.]

**Pricing model** [M]:
> Per seat, $49/user/month (Starter), $99/user/month (Pro). Enterprise pricing: contact sales.
> Minimum 5 seats on all plans. Annual billing required for >20% discount.

[ANNOTATION: Pricing is Medium because it's from their website but can change anytime.
Always include the observation date.]

**Key features** [H]:
- Real-time dashboard builder (drag-and-drop, no SQL required)
- Pre-built connectors: Salesforce, HubSpot, Snowflake, BigQuery (47 total)
- Alerting engine with Slack/email/webhook delivery
- Role-based access controls
- Embedded analytics (white-label for B2B SaaS customers)

**Enterprise readiness signals** [H]:
- [x] SOC2 Type II certified (badge on pricing page)
- [x] SSO / SAML (listed as Pro+ feature)
- [x] Admin controls
- [ ] Audit logs — not mentioned anywhere
- [x] SLA / uptime guarantees (99.9% on Enterprise plan only)

**Key integrations** [H]:
> Salesforce, HubSpot, Snowflake, BigQuery, Redshift, Postgres, Stripe, Zendesk, Jira, Slack

**Recent product moves (last 6 months)** [H/M]:
- AI-generated dashboard summaries (beta) — blog.acmeanalytics.com, Oct 2024
- Embedded analytics GA launch — blog.acmeanalytics.com, Aug 2024
- Snowflake Native App — snowflake.com/partners announcement, Sep 2024

---

### 3. Go-to-Market

**Target buyer** [M]:
> VP Operations, Head of Revenue Operations, Director of Finance. Company size 50–500.
> Evidence: 80% of G2 reviewers identify as "Operations" or "RevOps" roles. Case studies
> feature ops leads, not data engineers.

[ANNOTATION: G2 reviewer profiles are underused. Filtering by reviewer job title gives you
ICP data the company might not publish directly.]

**Target company profile** [M]:
> 50–500 employee B2B SaaS companies. Strong vertical presence in fintech and HR tech
> (8 of 12 named case studies). No enterprise (>1000 employee) logos visible.

**Sales motion** [M]:
> Hybrid PLG + outbound. Free trial available (14 days, no credit card). Active outbound
> SDR team visible on LinkedIn (7 SDR job posts in Q4 2024). Suggests PLG for top of funnel,
> outbound for mid-market conversion.

**Named customers** [H]:
> Rippling, Brex, Lattice, Ironclad, Chargebee, Drata, Merge, Workiva (logos page, Jan 2025)

[ANNOTATION: Keep this to publicly displayed logos only. Don't infer from press mentions
unless the company explicitly claims the customer.]

**Marketing channels** [M]:
> Heavy SEO focus (estimated 45k organic visits/month via Semrush). Active LinkedIn
> (3–4 posts/week). Monthly webinar series. No paid search detected.

---

### 4. Market Perception

**What they're known for** [M]:
> Speed of implementation is the most cited praise — reviewers consistently mention going
> from signup to first dashboard in under an hour. Non-technical users highlight the no-SQL
> interface as a key differentiator.

**Consistent complaints** [M]:
> Limited customization beyond templates frustrates power users. Several 3-star reviews
> mention that "you hit the ceiling fast" when building complex multi-dataset views.
> Support response time flagged in 6+ reviews from the last 6 months.

**Review volume and score** [H]:
> G2: 312 reviews, 4.4/5.0 as of Jan 2025
> Capterra: 89 reviews, 4.3/5.0 as of Jan 2025

---

### 5. Momentum (last 6–12 months)

| Signal type | Detail | Date | Confidence | Source |
|-------------|--------|------|------------|--------|
| Funding | $28M Series B co-led by Sequoia and Bessemer | Mar 2024 | H | [TechCrunch](https://techcrunch.com/acme-series-b) |
| Product launch | Embedded analytics GA | Aug 2024 | H | [Blog](https://blog.acmeanalytics.com/embedded-ga) |
| Product launch | AI-generated dashboard summaries (beta) | Oct 2024 | H | [Blog](https://blog.acmeanalytics.com/ai-summaries) |
| Partnership | Snowflake Native App | Sep 2024 | H | [Snowflake](https://snowflake.com/partners/acme) |
| Executive change | New CRO hired (ex-Looker, Jane Doe) | Nov 2024 | M | [LinkedIn](https://linkedin.com/in/janedoe) |
| Pricing change | None detected | — | — | — |
| Negative news | None detected | — | — | — |

**Funding deep-dive**

- **Round size & structure:** $28M Series B, co-led by Sequoia and Bessemer Venture Partners
- **Stated use of proceeds:** "Accelerate enterprise go-to-market and expand EMEA presence" — CEO quote, TechCrunch Mar 2024
- **Investor thesis / why now:** Sequoia partner noted "the operations analytics category is being rebuilt around real-time data" — [TechCrunch](https://techcrunch.com/acme-series-b)
- **Total raised to date:** $47M
- **Implied valuation signal:** Not disclosed

**Job openings signal** *(as of Jan 2025)*

| Role | Department | Signal interpretation |
|------|------------|----------------------|
| Enterprise AE x4 | Sales | Active upmarket push, targeting 500+ employee cos |
| Head of EMEA | GTM | Geographic expansion consistent with Series B stated intent |
| Senior ML Engineer x2 | Product | Investing in AI features beyond current beta |
| DevRel Engineer | Marketing | Developer ICP expansion |

- **Overall hiring posture:** Growing — 23 open roles vs ~15 estimated 3 months ago
- **Notable gaps:** No customer success or implementation roles despite enterprise push — potential onboarding risk at scale
- Source: [acmeanalytics.com/careers](https://acmeanalytics.com/careers) — retrieved Jan 15 2025

**LinkedIn activity snapshot**

*Company page:*
- Posting cadence: 3–4x/week
- Dominant themes: customer stories, product launches, hiring
- Recent standout: ["How Rippling cut reporting time by 60%"](https://linkedin.com/posts/acme-rippling) — Jan 8 2025 (high engagement, 340 reactions)

*Key execs:*
- Jane Smith (CEO): 2–3x/week, themes: thought leadership on ops analytics, occasional product commentary. Recent: [post on "the death of the weekly report"](https://linkedin.com/in/janesmith/post/xyz) — Jan 10 2025
- Jane Doe (CRO, new): 1x/week so far, themes: enterprise sales hiring, early customer wins. New to role, narrative still forming.

---

### 6. Open Questions

- [ ] Audit log functionality — not mentioned on site or in reviews; unclear if exists
- [ ] Enterprise ARR or revenue — no public data, no analyst coverage found
- [ ] Churn signals — no data on renewal rates or customer retention
- [ ] EMEA go-to-market — all named customers are US-based; unclear if active in Europe

---

### 7. Analyst Notes

*[This section left blank — to be completed by the author after review]*
