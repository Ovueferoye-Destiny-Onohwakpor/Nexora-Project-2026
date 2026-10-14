# Nexora Retail Nigeria Ltd. — Power BI Portfolio Case Study

A commercial performance analysis built in Power BI for the January 2025–June 2026 reporting period. The project focuses on more than sales totals: it evaluates target attainment, revenue retained after refunds, margin, returns, store performance, customer behavior, and channel mix.

> **Portfolio note:** This repository provides dashboard screenshots, the Power BI project file, and supporting documentation. GitHub displays the screenshots and files; it does not host the report as an interactive Power BI web experience.

## Business question

How did Nexora perform against its sales target, where did performance differ across the business, and which patterns warrant further investigation?

## Dashboard preview

### Executive overview
![Executive dashboard](screenshots/executive-dashboard.png)

### Customer analysis
![Customer analysis](screenshots/customer-analysis.png)

### Sales representative performance
![Sales representative performance](screenshots/sales-rep-performance.png)

### Time analysis
![Time analysis](screenshots/time-analysis.png)

### Data model
![Power BI data model](screenshots/data-model.png)

## Selected results

| Metric | Result | Interpretation |
|---|---:|---|
| Gross Sales | ₦3.618B | Sales value before discounts |
| Net Sales | ₦3.4439B | Gross Sales less discount value |
| Net Revenue | ₦3.3055B | Net Sales less refunds |
| Gross Profit | ₦754.26M | Net Revenue less Net COGS |
| Gross Margin | 22.82% | Gross Profit as a share of Net Revenue |
| Target Achievement | 96.90% | Net Sales divided by sales target |

**Metric distinction:** Net Sales, Net Revenue, and Gross Profit are different measures and are not interchangeable.

### Findings to investigate

- **Target gap:** overall target achievement was 96.90%, equivalent to a 3.10% shortfall.
- **Period comparison:** H1 2026 Net Sales were 1.30% below H1 2025; Net Revenue was down 1.21%, while Gross Profit was approximately flat (+0.04%). Gross margin rose from 22.60% to 22.89%.
- **Store variation:** Ikeja (102.80%), Abuja (102.64%), and Victoria Island (101.25%) exceeded target. Kano recorded the lowest target achievement (86.48%) and the highest store unit return rate (4.06%). These gaps identify where to investigate; they do not establish causes.
- **Discount and margin:** observed gross margin declined across higher discount bands. This is an association in the available data, not proof that discounts caused the decline or increased sales volume.
- **Channel signal:** WhatsApp/Phone had the highest average order value (about ₦648,000), a 2.36% unit return rate, and approximately 12.4% of revenue in the reviewed analysis. This is a potential area for further testing, not proof of scalable or incremental profit.
- **Recorded return reasons:** “Defective” was the largest recorded reason category (194 units; about 34.3% of returned units). The reason label alone does not establish the operational root cause.

## Approach

1. **Prepare data** in Power Query: review data types, standardize categorical values, address missing descriptive fields, and record inferred brand mappings.
2. **Model data** using product, customer, store, sales representative, and date dimensions connected to sales and target facts.
3. **Build measures** in DAX for sales, discounts, refunds, revenue, cost, gross profit, margin, target achievement, returns, time comparisons, and customer segmentation.
4. **Design report pages** for executive overview, time analysis, customer analysis, and sales representative performance, supported by a data-model view.
5. **Validate** KPI arithmetic, model relationships, date behavior, slicers, drill-through, and report interactions.

## Data quality and limitations

The QA report dated 14 October 2026 records **47/47 checks passed**: 30 checks were verified against the model/data and 17 manual checks were owner-confirmed. The owner-confirmed checks are not represented here as independently reproduced.

Important limitations remain despite the passed QA checks:

- 764 sales lines pre-date product launch dates (about ₦351.6M / 10.6% of Net Revenue).
- 285 sales lines pre-date customer signup dates (about ₦89.4M / 2.7% of Net Revenue).
- Three blank product brands were inferred from product-name patterns; these mappings are not source-confirmed.
- 12 customer records have missing City values and 12 sales lines have missing PaymentMethod values; both are represented as Unspecified.
- 314 customer-name values are duplicated. Use CustomerID for customer-level analysis rather than treating names as unique identifiers.
- The dataset covers January 2025–June 2026 and has no 2024 data, so 2025 year-over-year analysis is unavailable.
- Targets are defined at store/month level, not for every day or every product, representative, channel, customer, or city. Some target measures are intentionally blank under incompatible slicer contexts.
- Customer segment thresholds vary with the selected date context.
- Return-reason labels, discount-band margin differences, channel metrics, and store gaps are descriptive signals; they do not prove root causes or causal effects.
- Refresh may depend on a local Google Drive for Desktop path and may require environment-specific changes on another computer.

See the full [Data Quality and Limitations note](documentation/data-quality-and-limitations.md) for details, and the [documentation index](documentation/README.md) for supporting files.

## Repository contents

- `report/Nexora_Retail_Nig_LTD_Tentative_Dashboard_10_11_2026_Finalized.pbix` — Power BI report file.
- `screenshots/` — dashboard and model screenshots, with consistent lowercase filenames.
- `documentation/qa-report-2026-10-14.pdf` — finalized QA report.
- `documentation/data-quality-and-limitations.docx` — formatted Word documentation.
- `documentation/` — Markdown documentation and index.

## Tools and skills demonstrated

- Power Query data preparation
- Dimensional modeling / star-schema design
- DAX measures and time comparisons
- KPI validation and data-quality documentation
- Interactive dashboard design and business interpretation

## Scope and responsible interpretation

This is a portfolio case study based on the dataset and reporting model in this repository. The results should be treated as decision-support signals for further investigation, not as proof of causality or as audited financial statements. Validate source lifecycle dates, inferred brands, customer identity, and refresh configuration before operational use.
