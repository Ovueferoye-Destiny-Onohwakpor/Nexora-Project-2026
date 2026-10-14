# Data Quality and Limitations

**Project:** Nexora Retail Nigeria Ltd. — Power BI portfolio case study  
**Reporting period:** 1 January 2025–30 June 2026  
**QA report date:** 14 October 2026

## Purpose and evidence boundary

This note documents preparation decisions, known source-data limitations, and the boundaries on interpretation. The dashboard QA report records **47 of 47 checks passed**: 30 checks were verified against the model/data and 17 were manual checks reported as owner-confirmed. The manual checks were not independently reproduced for this document.

A passed QA check means the tested calculation, model behavior, or report interaction met its defined expectation. It does **not** mean every source-data issue has been corrected or that the dataset is free of limitations.

## Data preparation and modeling

- Data types and categorical text were standardized in Power Query where required; extra spacing and case variations were addressed in prepared fields where applicable.
- Missing customer city and payment-method values are displayed as **Unspecified** rather than treated as known values.
- Three blank product-brand values were inferred from product-name patterns: PRD001 and PRD021 as Orion, and PRD031 as Apex. These are inferences, not source-confirmed brand assignments.
- The model uses product, customer, store, sales representative, and date dimensions with sales and target facts. The returns data was matched to sales lines using SalesLineID.
- Customer-level analysis should use CustomerID, not customer name, because names are not unique.
- The model includes a contiguous date table from 1 January 2025 to 30 June 2026 (546 calendar days), including one day with no sales.

## Known limitations and interpretation controls

### 1. Sales before product launch

There are **764 sales lines dated before the recorded product launch date**, representing approximately **₦351.6 million, or 10.6% of Net Revenue**. This may reflect source-date or lifecycle-record inconsistencies. The dashboard does not establish which date is wrong; treat product-lifecycle analysis with caution.

### 2. Sales before customer signup

There are **285 sales lines dated before the recorded customer signup date**, representing approximately **₦89.4 million, or 2.7% of Net Revenue**. These records need source-system validation before customer-acquisition or lifecycle conclusions are drawn.

### 3. Inferred product brands

The three blank brand values noted above were filled by inference from product names. Brand-level results involving these products depend on that assumption. Confirm the mappings against an authoritative product master before operational use.

### 4. Missing descriptive fields

- **12 customer records** have no City value and are represented as Unspecified.
- **12 sales lines** have no PaymentMethod value and are represented as Unspecified.

These records remain part of the data. Do not interpret Unspecified as a real city or payment channel.

### 5. Duplicate customer names

The source contains **314 duplicated customer-name values**. Different customer records may share a name, so name-based aggregation can merge distinct people. Use CustomerID for customer-level calculations and drill-through. Name-level displays should not be interpreted as a definitive count of unique customers.

### 6. Category casing variants

Source values such as **“Sme”** and **“Pos”** were noted during QA. Use the prepared/cleaned categorical fields where available. If raw and cleaned fields are mixed in a visual or measure, categories may split unexpectedly.

### 7. Limited historical coverage

The dataset covers January 2025 through June 2026 and contains no 2024 period. A 2025 year-over-year comparison is therefore unavailable. The reported H1 2026 vs H1 2025 comparison is a like-for-like six-month comparison, not a full-year comparison.

### 8. Date-filtered customer segments

Customer segment thresholds are responsive to the active date context. Across the full dataset, the noted 20th and 80th percentile thresholds are approximately ₦1.44 million and ₦4.80 million; for a 2026-only context, the 80th percentile is approximately ₦1.73 million. Segment membership can therefore change when date filters change. A “No Purchase History” result under a selected-period filter means no purchase in that period, not necessarily no all-time purchase.

### 9. Sales-target granularity and filter behavior

Targets are defined at **store/month** level, not at day, product, sales representative, channel, customer, or city level. On the Executive page, Target and Achievement are intentionally blank when Channel, customer Region, or City slicers are active because the target cannot be allocated reliably to those selections. A single-day selection may still show the month’s target; that value is not a daily target.

### 10. Return reasons do not establish root cause

“Defective” is the largest recorded return-reason category (194 units; approximately 34.3% of returned units, with about ₦46.3 million in refunds). This identifies a recorded reason, not the operational root cause. Confirm product quality, fulfillment, and return-processing records before assigning responsibility or proposing a specific corrective action.

### 11. Small counts in some comparisons

Sales-representative return counts are small (roughly 8–33 returned units per representative in the reviewed comparison). Rate rankings can move materially when counts are low. Interpret them as investigation signals rather than definitive performance rankings.

### 12. Discount bands and margin

Observed gross margin declines across the analyzed discount bands: 26.69% at 0% discount, 23.18% at 0.1–5%, 19.01% at 5.1–10%, and 11.75% above 10%. This is an association in the observed data. It does not prove discounts caused lower margin or establish whether discounts increased sales volume, customer retention, or incremental profit.

### 13. Channel performance is not proof of scalability

WhatsApp/Phone has the highest average order value (about ₦648,000), a 2.36% unit return rate, and approximately 12.4% of revenue in the reviewed analysis. These results suggest a channel worth investigating; they do not prove that increased investment will scale profitably. Check acquisition cost, capacity, repeat behavior, and incremental margin before recommending expansion.

### 14. Store-level gaps identify where to investigate, not why

Ikeja (102.80%), Abuja (102.64%), and Victoria Island (101.25%) exceeded target. Kano had the lowest target achievement (86.48%) and the highest store unit return rate (4.06%) in the reviewed comparison. These figures identify performance differences but do not establish the causes.

### 15. Customer and product concentration

Segment, product, and customer comparisons describe the records available in this dataset and time window. They should not automatically be generalized to future periods or the entire business without checking coverage, seasonality, and whether the dataset is representative.

### 16. Refresh and environment dependency

The source workbook was reported by the owner to use a Google Drive for Desktop mapped path (`H:\\My Drive\\_Portfolio\\Nexora_PowerBI_Assessment_Raw_Dataset (WELUP DIGITAL).xlsx`). Cross-machine refresh was reported as passed by the owner, but no independent environment logs were supplied here. Refresh may require updating the source path and credentials on another computer.

## Validated KPI context

The reviewed report records approximately:

- Gross Sales: **₦3.618 billion**
- Discount Value: **₦173.82 million**
- Net Sales: **₦3.4439 billion**
- Refund Value: **₦138.34 million**
- Net Revenue: **₦3.305513 billion**
- Net COGS: **₦2.551 billion**
- Gross Profit: **₦754.26 million**
- Gross Margin: **22.82%**
- Target Achievement: **96.90%**

The arithmetic identities tested were Gross Sales − Discount Value = Net Sales; Net Sales − Refund Value = Net Revenue; Net Revenue − Net COGS = Gross Profit; and Net Sales ÷ Sales Target = Target Achievement.

Use these labels precisely: **Net Sales is not Net Revenue, and neither is profit.**

## Recommended use

Treat the dashboard as a portfolio analysis and decision-support prototype. Validate lifecycle dates, brand assignments, missing fields, customer identity, and refresh configuration before using the results for operational decisions. Where the dashboard shows an association or a performance gap, investigate the mechanism before presenting it as a cause.
