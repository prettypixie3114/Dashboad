# Pretty Pixie · Fashion Forever — Performance Command Center (v5.1)

Senior-management performance dashboard for the 9-Campaign Meta build.
Tracks live Meta API data against the locked targets from the `Mar+Apr Analysis v6` deliverables.

**v5.1 additions** · conversion funnel diagnostic · per-ad recommendation engine · auto-refresh · CVR/CTR everywhere

---

## What this dashboard shows

**Top-line (the management showcase view):**
- **Executive Header** — yesterday's MER as a big number with traffic-light status against Phase 1/2/3 goal band, plus a one-line summary ("6 of 10 gold KPIs on target · 2 at risk · 2 below target")
- **Margin Protection Rules** — all 10 rules from Section 14, with TRIPPED / HOLDING status and evidence. Surfaces at the top because these are the rules that prevent contribution-negative scaling.
- **Executive Summary table** — Goal · Where We Are · Status · What This Means · What To Do for all 23 KPIs (16 from Section J + 7 conversion funnel KPIs). Filter to Gold (the 6 CEO metrics) or Silver (tactical).
- **Conversion Funnel panel** *(v5.1)* — Impressions → Link Clicks → ATC → Init Checkout → Purchase. Each stage shows count, conversion rate from previous, drop-off %, and benchmark target. Highlights the biggest leak (e.g., "IC → Purchase losing 64.2% — Razorpay/GoKwik checkout health · was 48.8% baseline, 36% today").
- **Funnel Stage Allocation** — Prospecting / Retargeting / Reactivation actual vs target % per phase
- **9-Campaign Matrix** — one card per campaign with phase-specific Goal / Actual / Gap / Kill rule status + CVR + CTR + AOV + Frequency at a glance. Click any card for ad-level detail.
- **Campaign Detail** (modal) — full TAPG table for 10 campaign KPIs · kill-rule alert banner · interactive chart with values labeled · ad-set table with recommendation · **ad-level table with per-ad action** *(v5.1)* applying Sheet 16 Section 3 thresholds: each ad gets KILL / PAUSE / REFRESH / AUDIT / SCALE / HOLD / BUILDING verdict with reasoning. Direct links to Meta Ads Manager for any ad.
- **Interactive Trends** — chart with metric filter (ROAS, Spend, Revenue, CPA, AOV, Orders) and scope filter (Account total, by stage, or any of 9 campaigns). Target and kill lines drawn.
- **Audience Segments** — F35-44, F25-34, etc. with Goal ROAS vs actual. Surfaces "Exclusion Broken" alert if any spend leaks to Male 18-34 (which should be excluded permanently).
- **Pre-Flight Checklist** — 22-item launch readiness tracker with localStorage persistence.
- **Auto-refresh** *(v5.1)* — toggle Off / 5min / 15min / 30min in the header. Live "synced X seconds ago" counter.

**Conversion metrics added in v5.1:**
- **CVR · Click → Purchase** — the conversion engine (≥1.5% P1 · ≥2.0% P2 · ≥2.5% P3)
- **Link CTR** — link clicks / impressions (≥1.0-1.5% by phase)
- **ATC Rate** — Add-to-Cart per link click (≥4-6% by phase)
- **IC → Purchase %** — Razorpay/GoKwik checkout health (≥40-50% by phase · baseline 36%, target 48.8%+)
- **Hook Rate (3-sec)** — creative quality signal (≥25-30% by phase)
- **CPC** — Cost per link click (≤₹30-40 by phase)
- **CTR** — total CTR including image clicks (≥1.0-1.5% by phase)

**Per-ad action engine (v5.1):**
Every ad in a campaign gets a verdict following Sheet 16 Section 3 thresholds:
- **Cold prospecting:** ROAS <1.0x at ₹15K → KILL within 24hr · 1.0-1.4x → REFRESH hook · ≥1.5x → PROMOTE +20%
- **Warm RT (C8):** <1.5x at ₹8K → KILL within 48hr · ≥2.5x → PROMOTE
- **Hot DPA (C7):** <2.0x at ₹5K → CATALOG AUDIT (not creative)
- **Reactivation (C9):** <2.5x at ₹5K → REFRESH hook + window · ≥5.0x → SCALE +30%
- **Universal:** Frequency >3.5x → PAUSE · >3.0x → REFRESH · 0 orders at ₹5K → KILL

**Status language used throughout:**
- ON TARGET · AT RISK · BELOW TARGET · NOT YET TRACKED
- Plain English: "Meeting the goal" · "Close to goal · watch" · "Below goal · action needed" · "Not enough data yet"
- Every KPI has: *What This Means* (the metric in plain English) + *What To Do* (the action if breached)

---

## File structure

```
fashionforever-dashboard/
├── index.html      ← Main app · React + Tailwind via CDN · 1,200+ lines
├── config.js       ← Every editable target lives here · 390 lines
└── README.md       ← This file
```

**`config.js` is the only file you'll edit regularly.** It contains every number from your three source PDFs:
- 9 campaigns with per-phase daily budgets, predicted ROAS bands, CPA caps, frequency caps
- 16 Section J KPIs with exact phase bands (P1/P2/P3)
- 10 Margin Protection Rules with trigger logic
- 8 audience segments with target ROAS bands
- 22-item pre-flight checklist
- Funnel stage allocation (75/20/5 → 65/25/10 → 60/28/12)
- Asset count targets per phase (20→23→25 ad sets; 44→55→62 ads)

When targets change, edit `config.js`, push to GitHub, refresh the browser. **No need to touch `index.html`.**

---

## Source data references (locked targets)

Every number in `config.js` is traceable to one of these source PDFs:

| Source | Used for |
|---|---|
| **`9-Campaign Build`** Section A | Daily spend caps per phase (₹54K → ₹62K → ₹75K) |
| **`9-Campaign Build`** Section B (C1–C9) | Per-campaign budgets, predicted ROAS, CPA caps, audience exclusions |
| **`9-Campaign Build`** Section J | All 16 KPI targets with phase bands |
| **`Sheet 16`** Section 0 | Active ad set / ad count targets (20 → 23 → 25 / 44 → 55 → 62) |
| **`Sheet 16`** Section 1 | Audience exclusion specs for each campaign |
| **`Sheet 16`** Section 3 | Kill & refresh thresholds (cold <1.0x@₹15K kill, etc.) |
| **`Sheet 16`** Section 4 | 22-item pre-flight checklist |
| **`Action Plan`** Section 9 | Audience segment targets (F35-44 goldmine, M18-34 kill) |
| **`Action Plan`** Section 13 | Daily morning KPI thresholds |
| **`Action Plan`** Section 14 | 10 Margin Protection Rules |

---

## Setup · GitHub Pages deployment

### 1) Push to GitHub

```bash
# In your local repo folder
git init
git add index.html config.js README.md
git commit -m "Pretty Pixie dashboard v5"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

### 2) Enable GitHub Pages

In the GitHub repo:
1. Settings → Pages
2. Source: **Deploy from a branch**
3. Branch: **main** · folder: **/ (root)**
4. Save. Wait 1–2 minutes.
5. Dashboard live at `https://<your-username>.github.io/<repo-name>/`

### 3) Get your Meta access token

In **Meta Business Manager**:
1. Settings → System Users → Create System User (or use existing)
2. Generate Token → select your ad account (`act_2295943007451315`)
3. Permissions: `ads_read`, `read_insights`, `business_management`
4. Copy the token
5. Paste it into the dashboard's token modal on first load (stored locally in your browser only — never sent to any server)

### 4) Daily workflow

- Open the dashboard URL
- Click **Sync Now** (top right) → fetches latest from Meta
- Use date presets (Today / Yesterday / 7d / 28d / Custom) to slice
- Click any campaign card for full detail
- Click **Print / PDF** for a clean screenshot to share with leadership

---

## How to update targets when phases change

When you move from Phase 1 to Phase 2 (Day 31), no edit needed — the app auto-detects the phase from `phaseStartIST` in `config.js` and shows Phase 2 targets automatically.

To change phase start date (e.g., delayed launch):

```js
// config.js
phaseStartIST: '2026-05-15T00:00:00+05:30',   // change this date
```

To change any campaign's predicted ROAS or budget:

```js
// config.js · find the C1 entry
{ slot: 'C1', ...,
  dailyBudget:  { p1: 14000, p2: 14000, p3: 15000 },   // ← edit these
  predictedRoas:{ p1: [1.4, 1.6], p2: [1.5, 1.7], p3: [1.6, 1.9] },   // ← or these
  ...
}
```

To change a Section J KPI band:

```js
// config.js · find kpis.mer (or whichever KPI)
mer: {
  ...
  bands: { p1: [1.6, 1.9], p2: [2.2, 2.7], p3: [2.8, 3.5] },   // ← edit these
  ...
}
```

Push to GitHub → refresh browser → new targets live.

---

## What's wired vs what's pending

✅ **Live from Meta** (working now):
- MER, ROAS by campaign, CPA, AOV, Spend, Orders, CTR, CPC, IC→Purchase, Frequency, Hook rate
- Audience segment breakdown (age × gender)
- Contribution margin (computed from revenue × 55% GM minus spend minus ₹120/order shipping)
- All ad-set and ad-level detail

⏳ **Renders as "—" with "Needs Shopify wire" tag** (until those integrations are added):
- Repeat Rate 60d (needs Shopify customer cohort)
- Prepaid Mix % (needs Shopify payment attribute)
- Cancel Rate % (needs Shopify order status)
- Discount % of Subtotal (needs Shopify discount applied)
- Bundle Attach Rate (needs Shopify line-item attribute)
- Refund Rate (needs Shopify refunds endpoint)
- Email Klaviyo Rev/wk (needs Klaviyo API)
- WhatsApp Rev/wk (needs BiteSpeed API)
- Click → Session % (needs GA4 connection)
- NC-ROAS (needs Shopify customer-cohort split)

These render with their **correct targets** so management sees what's being tracked vs what needs wiring. Once you add Shopify/Klaviyo/BiteSpeed connectors (v6 scope), they'll start populating live.

---

## Brutal-honest closing notes

This dashboard **reports correctly** against the locked plan. It does **not fix** the structural problems documented in the source PDFs:

1. **Click → Session 76% leak** — that's a Shopify theme problem (likely Mojito Lab JS). The dashboard will surface it; only a tech audit fixes it.
2. **₹1,000 flat off cannibalization** — the legacy code needs to sunset on Day 30 per the plan. Dashboard tracks discount %; manually killing the code is on the founder.
3. **Margin Rule R2 (ROAS floor)** will trip on Day 7-14 if exclusions aren't applied — verify Male 18-34 + 18 wasted cities + 5 high-cancel states are excluded at the **account level** before launch (checklist items #11, #15).
4. **NC-ROAS masking (R9)** — without Shopify cohort wiring, this rule is "Pending data". Until then, blended MER alone can hide a degrading new-customer acquisition. The plan documents this; the dashboard can't compute it without the connector.

Phase 1 success = MER 1.6-1.9x by Day 30 with contribution margin between -₹2L and +₹3L. The plan is sequenced as STABILIZE → BUILD → SCALE for a reason: do not scale spend until Phase 1 targets are met.
