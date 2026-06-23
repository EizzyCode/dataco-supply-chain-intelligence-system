# Dataset Source

## DataCo Smart Supply Chain Dataset

This project uses the publicly available **DataCo Smart Supply Chain for Big Data Analysis** dataset.

**Source:** Kaggle
**Link:** https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis

---

## Dataset Overview

| Detail | Value |
|---|---|
| Format | Single flat CSV file |
| Raw rows | 180,519 |
| Raw columns | 53 |
| Unique orders (after cleaning) | 65,750 |
| Time period covered | January 2015 to December 2018 |
| Markets covered | Africa, Europe, LATAM, Pacific Asia, USCA |

---

## Why the Raw File Is Not Included in This Repository

The raw dataset file is not uploaded to this repository because:

1. It is publicly available directly from the original source above
2. Redistributing third-party datasets without explicit permission is discouraged practice
3. The file exceeds typical repository size conventions for a portfolio project

To reproduce this project, download the dataset directly from the Kaggle link above and follow the data preparation steps documented in Section 3 of the accompanying technical report (`DataCo_Technical_Report.pdf`).

---

## Known Data Quality Notes

A few data quality characteristics were identified and addressed during preparation, all documented in full in the technical report:

- Missing zip codes on a small percentage of records
- Suspected fraud orders flagged in the `Order Status` column
- Shipping date occasionally preceding order date in a small number of edge cases
- Inconsistent formatting in some product description fields

These were handled during the Power Query cleaning stage and are explained step by step in Section 3 of the technical report.
