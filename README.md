# DataCo Supply Chain Intelligence System

Power BI supply chain analytics project analysing 65,750 orders across 5 global markets to diagnose a 57.42% late delivery rate. Built on the SCOR framework with a star schema, 27 DAX measures, row-level security, and a full technical report.

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Tool](https://img.shields.io/badge/tool-Power%20BI-yellow)
![Framework](https://img.shields.io/badge/framework-SCOR-black)

---

## Live Demo

**Dashboard:** [Insert Power BI embed / public link here]

**Technical Report (PDF):** [DataCo_Technical_Report.pdf](./DataCo_Technical_Report.pdf)

**Portfolio:** [datascienceportfol.io/ashibcosmas](https://datascienceportfol.io/ashibcosmas)

> Row-level security has been disabled in the publicly embedded version above, since Power BI does not support public sharing for reports with RLS enabled. The full RLS implementation (12 roles across Executive, Regional Manager, and Country Manager tiers) is documented in the technical report and demonstrated in the local `.pbix` file. Available on request.

---

## The Problem

DataCo Global is a mid-to-large scale e-commerce and retail distribution company operating across five international markets: Africa, Europe, LATAM, Pacific Asia, and USCA. More than half of all fulfilled orders, **57.42%**, arrive late. This project investigates why, what it is costing the business, and what should be done about it.

Key findings at a glance:

| Metric | Value |
|---|---|
| Total orders analysed | 65,750 |
| Late delivery rate | 57.42% |
| Profit margin | 10.78% |
| Revenue at risk (late orders) | $9.2M |
| Total loss amount | ($3.88M) |
| Shipping Efficiency Index | 83.82% |

The most striking finding: late delivery rate variance across product categories is almost flat (61.59% to 62.58%), and all five markets cluster between 56% and 59%. This is not a seasonal, regional, or product-specific problem. It is a systemic failure in scheduling and logistics infrastructure.

First Class shipping, the company's premium tier, recorded a **100% late delivery rate** across the entire dataset.

---

## Dataset

**Source:** [DataCo Smart Supply Chain Dataset (Kaggle)](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis)

Raw file: 180,519 rows, 53 columns, single flat CSV covering orders from 2015 to 2018.
After cleaning and deduplication: 65,750 unique order records.

The dataset does not include warehouse inventory data, supplier lead times, or actual logistics cost per shipment. These limitations are documented in full in the technical report. See [`dataset/dataset_source.md`](./dataset/dataset_source.md) for full dataset notes.

---

## Project Structure

This project is organised around the **SCOR (Supply Chain Operations Reference) model**:

| Dashboard Section | SCOR Domain |
|---|---|
| Delivery Performance Analysis | Deliver |
| Demand & Order Behaviour Analysis | Plan |
| Supply Pressure & Risk Analysis | Source / Plan |
| Profitability & Cost Impact Analysis | Enable |

### Dashboard Pages

1. **Cover Page** — project overview, key stats, world map visual
2. **Executive Summary** — high level KPIs and trends for C-level stakeholders
3. **Delivery Overview** — delivery performance trends and shipping metrics
4. **Root Cause Analysis** — diagnostic breakdown of late delivery drivers
5. **Demand & Product Analysis** — order volume patterns and product velocity
6. **Profitability & Cost Impact** — margin analysis and cost of inefficiency
7. **Drillthrough** (hidden) — order level investigation page

---

## Tech Stack

- **Microsoft Power BI Desktop** — data modelling, DAX, dashboard build
- **Microsoft Excel (Power Query)** — data preparation pipeline
- **DAX** — 27 measures across delivery, financial, demand and supporting categories
- **Star schema** — 1 fact table (`FactOrders`) and 7 dimension tables

### Data Model

```
FactOrders (centre)
├── DimCustomer
├── DimProduct
├── DimCategory
├── DimRegion ── DimGeography
├── DimShippingMode
└── DimDate
```

Full data model architecture is documented in Appendix D of the technical report.

---

## Key Features

- **Star schema data model** built from a single flat CSV file
- **27 DAX measures** across delivery performance, financial, demand and product categories
- **Row-level security** with 12 roles (1 Executive, 5 Regional Managers, 6 Country Managers)
- **Dynamic drillthrough** with a context-aware page title using `COALESCE` and `SELECTEDVALUE`
- **Collapsible slicer panel** using bookmarks and the Selection Pane
- **Dark mode enterprise design** in a single black and gold colour palette
- **Dynamic report date** measure using `TODAY()`

---

## Challenges & Lessons Learned

Data preparation was the hardest part of this project, not the dashboard build. A few highlights:

- Power BI Desktop repeatedly failed to load the dataset due to merge operations multiplying `FactOrders` from 65,750 rows to over 3 million rows, caused by duplicate values in dimension tables before deduplication was applied.
- After multiple failed attempts (buffering, disabling background refresh, moving the file off OneDrive), the root cause was found to be the merge operations themselves. The fix was to remove all merges from Power Query entirely and build relationships directly in Power BI's model view, the correct approach for a star schema.
- The data preparation pipeline was eventually rebuilt in **Excel Power Query** and the resulting M code imported into Power BI, which resolved the loading issue completely.
- Delivery rate measures initially mixed row-level and order-level counting (`COUNTROWS` vs `DISTINCTCOUNT`), which inflated several KPIs. All measures were corrected to use consistent order-level counting.

The full list of challenges and corrections is documented in Sections 3 and 9 of the technical report.

---

## Repository Contents

```
├── DataCo_Supply_Chain_Intelligence_System.pbix    # Full Power BI file (RLS intact)
├── DataCo_Technical_Report.pdf                     # Full technical report
├── README.md
├── screenshots/                                    # Dashboard page exports
│   ├── 01_cover_page.png
│   ├── 02_executive_summary.png
│   ├── 03_delivery_overview.png
│   ├── 04_root_cause_analysis.png
│   ├── 05_demand_product_analysis.png
│   ├── 06_profitability_cost_impact.png
│   ├── 07_drillthrough.png
│   ├── 08_rls_regional_manager.png
│   └── 09_rls_country_manager.png
└── dataset/
    └── dataset_source.md                           # Dataset reference and notes
```

---

## About This Project

This is a personal portfolio project built to demonstrate supply chain analytics, Power BI development, and enterprise BI governance practices. It was structured using a formal project brief, a Requirements Traceability Matrix, a context diagram, and a data flow diagram before any development began.

**Analyst:** Ashibeshi Cosmas
**Certifications:** Microsoft PL-300 (Power BI Data Analyst Associate), CSCMP Supply Chain Foundations
**Portfolio:** [datascienceportfol.io/ashibcosmas](https://datascienceportfol.io/ashibcosmas)
**GitHub:** [EizzyCode](https://github.com/EizzyCode)

---

## License

This project uses a publicly available dataset for educational and portfolio purposes. Feel free to fork and explore, but please credit the original dataset source if you reuse it.
