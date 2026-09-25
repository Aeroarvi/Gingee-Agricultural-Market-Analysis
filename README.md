# Agricultural Market Trade Analysis – Gingee APMc

## Overview
Portfolio-ready analysis of the supplied National Agriculture Market (NAM) Gingee Mandi Wise Agreement Type Summary Reports.

**Coverage in the supplied files:** FY 2022-23, FY 2023-24, FY 2024-25 and FY 2025-26.  
**Important:** four annual PDFs were supplied, not five. The project therefore covers **4 years**

## Business Problem
Turn annual mandi-level agricultural trade reports into a structured analytical dataset and dashboard that makes trade value, traded quantity, commodity mix and year-over-year changes easy to monitor.

## Dataset
- State: Tamil Nadu
- APMC: Gingee
- District: Villupuram
- Unit of measure: Qui (as printed in the reports)
- Records extracted: 108
- Core measures: Arrived Lots, Arrived Quantity, Traded Lots, Traded Quantity, Trade Value (Rs)
- Collection Fee: **not available as a usable field in the supplied PDFs**

## Data Cleaning
- Extracted commodity-year rows from the four PDFs.
- Standardized fiscal-year labels to `YYYY-YY`.
- Standardized text whitespace and commodity naming into a consistent `Commodity` field.
- Converted quantities, lot counts and trade value to numeric fields.
- Preserved zero-trade rows rather than deleting them.
- Checked duplicates and source totals.
- Flagged, but did not alter, cases where traded quantity/lots exceed arrived quantity/lots.
- Preserved the 0.01 Qui FY2022-23 source-total mismatch rather than silently correcting it.

## KPIs
- Total Trade Value: ₹6,977,530,895.63
- Total Trade Quantity: 2,781,257.22 Qui
- Total Traded Lots: 214,172
- Number of Commodities: 46
- Average Annual Trade Value: ₹1,744,382,723.91
- Latest FY YoY Trade Value Growth: 13.38%

## Key Analytical Findings
1. Paddy(75 KG) accounts for 85.06% of total trade value across the four supplied years.
2. FY2023-24 trade value increased 38.10% versus FY2022-23.
3. FY2024-25 trade value changed -9.90% versus FY2023-24.
4. FY2025-26 trade value changed 13.38% versus FY2024-25.
5. FY2025-26 has the highest traded quantity among the four supplied years: 811,165.91 Qui.
6. Collection fee analysis cannot be calculated from these PDFs because the supplied report does not provide a usable collection-fee measure.

## Power BI
Recommended model:
- `FactMarketTrade`: one row per Fiscal Year + Commodity.
- `DimYear`: Fiscal Year, Year Start, Year Index.
- `DimCommodity`: Commodity, Commodity Group.
- Optional `DimLocation`: State, District, APMC.

Use a one-to-many relationship from each dimension to the fact table.

## Suggested Dashboard
Title: **Agricultural Market Trade & Collection Fee Analysis – 5 Year Dashboard**

Top: Year slicer, Crop slicer, KPI cards  
Middle: Trade Value trend, Commodity Trade Value  
Bottom: Quantity trend, Commodity contribution, Trade Value vs Quantity

Because Collection Fee is absent, replace collection-fee visuals with Trade Value vs Quantity or Traded Lots until the missing fee data is supplied.

## Folder Structure
```text
agricultural-market-analysis/
├── data/
│   ├── raw/
│   │   ├── MARCH 2023.pdf
│   │   ├── MARCH 2024.pdf
│   │   ├── MARCH 2025.pdf
│   │   └── MARCH 2026.pdf
│   └── processed/
│       ├── gingee_market_clean.csv
│       └── gingee_market_analysis.xlsx
├── powerbi/
│   └── Agricultural_Market_Dashboard.pbix
├── docs/
│   └── data_quality_report.xlsx
└── README.md
```
