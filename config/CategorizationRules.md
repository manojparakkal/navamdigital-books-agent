# CategorizationRules.md — Navam Digital (Cash Basis)
Version: 1.0

## Priority Order (highest to lowest)
1. **VendorMap.csv** exact/contains matches (treat as authoritative)
2. Exact description match (if implemented)
3. Keyword rules (below)
4. Fallback category = `Suspense / Unclassified` (CPA-aligned) and send to Exceptions Agent

## Amount Sign Conventions
### Bank (Capital One Checking)
- **Money in:** positive
- **Money out:** negative

### Credit Card (Capital One Business Card)
Use this convention throughout:
- **Purchases/fees:** positive
- **Payments/credits/refunds:** negative

## Keyword Rules (only if VendorMap does not match)
- `domain`, `sqsp`, `squarespace` → Domain & Website
- `openai`, `chatgpt`, `claude`, `replicate` → SaaS Subscriptions
- `vercel`, `aws`, `azure`, `gcp` → Cloud/Hosting
- `uber`, `lyft`, `taxi` → Travel - Ground Transport
- `hotel`, `inn`, `marriott`, `hilton` → Travel - Lodging
- `air`, `airlines`, `emirates`, `delta`, `united` → Travel - Airfare
- `airport`, `lax` → Travel - Other
- `restaurant`, `cafe` → Meals & Entertainment
- `wire`, `fee` → Bank & Wire Fees

## Confidence Scoring (guidance)
- VendorMap match: **0.90–0.99**
- Strong keyword match: **0.75–0.89**
- Weak/fallback: **< 0.75** → send to Exceptions Agent

## Large Transaction Flag
- Any single transaction with absolute value **>= $1,000** → flag for owner review.

## Business vs Personal Review
Default: **flag** the following categories for business-purpose confirmation unless you explicitly mark them as always-business:
- Travel
- Meals & Entertainment
- Retail/Amazon/Convenience

## Audit Trail Requirement
Every classified transaction should store:
- source (BANK/CARD)
- original description
- category + confidence
- rule applied (VendorMap/keyword/fallback)


## CPA Reporting Rollup
- Maintain two levels of categorization:
  1. **Operational category** (default_category / account_name)
  2. **CPA reporting_category** (from ChartOfAccounts.csv)
- Reporting Agent should generate financial statements grouped by **reporting_category** and **reporting_group** for CPA-style output.
