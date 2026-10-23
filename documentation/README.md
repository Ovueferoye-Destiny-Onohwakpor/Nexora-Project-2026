# Project Documentation

Supporting material for the Nexora Retail Nigeria Ltd. Power BI portfolio case study. The source `Segment` field (account type / primary-residency classification) is distinct from the DAX-derived `CustomerSegment` behavioral interaction tier.

## Documents

- [Data Quality and Limitations](data-quality-and-limitations.md) — data preparation decisions, known source-data issues, interpretation caveats, and validated KPI context.
- [Comprehensive Dashboard QA Report (Markdown)](qa-report-2026-10-22.md) — full QA checklist, model changes, regression expectations, final closure matrix, evidence boundary, and reconciliations. Last revised 22 October 2026; QA closure date remains 14 October 2026.

## Power BI source connection note

The packaged PBIX currently does not connect successfully to the raw Excel workbook in this repository; a successful reconnect and refresh have not been verified. The source is a static flat file rather than a live data source, so this is primarily a reproducibility/setup limitation. Updating the Power Query source path is necessary only if the report needs to be refreshed or reproduced in another environment; the documented analysis is based on the existing dataset snapshot.

## Evidence note

The [QA report](qa-report-2026-10-22.md) records 47/47 checks passed, including 30 checks verified against the model/data and 17 owner-confirmed manual checks. Owner-confirmed checks are reported as such; they should not be represented as independently reproduced.
