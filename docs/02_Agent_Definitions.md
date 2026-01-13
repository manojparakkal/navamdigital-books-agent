# Agent Definitions

Detailed responsibilities for Agents A–I.

### Suspense Handling (CPA-aligned)
- Any transaction with confidence < 0.75 MUST be posted to `Suspense / Unclassified`.
- No low-confidence transaction may be force-categorized.
- All Suspense items must appear in the Exceptions report and require owner resolution before final close.


### Dual Categorization Model
Each transaction maintains two category layers:
1. **Operational Category** (default_category / account_name)
2. **CPA Reporting Category** (reporting_category, reporting_group)

- Journal entries use the operational category.
- Financial statements are generated using CPA reporting categories.


### VendorMap Authority
- VendorMap.csv is the highest-precedence classification source.
- Vendor rules represent explicit owner intent and must override keyword or heuristic logic.
