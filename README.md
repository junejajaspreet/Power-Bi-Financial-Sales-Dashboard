# Product Sales & Profitability Analysis (Power BI)

**Domain:** Financial Analytics / Sales Performance
**Tools:** Power BI Desktop, Power Query (M), DAX, Excel
**Timeline:** July 2026

## Business Problem

A multi-country sales business needed visibility into where its profit was actually coming from, and where it was quietly leaking. Aggregate numbers looked healthy on the surface, but leadership had no way to see which segments, products, or discount practices were dragging down profitability underneath that headline figure. This project builds an interactive Power BI dashboard to answer that question directly.

## Dataset

- **Source:** Microsoft Financial Sample Dataset (publicly available sample data)
- **Size:** 700 records, 16 fields
- **Fields:** Segment, Country, Product, Discount Band, Units Sold, Manufacturing Price, Sale Price, Gross Sales, Discounts, Sales, COGS, Profit, Date, Month Number, Month Name, Year
- **Coverage:** September 2013 – December 2014 (2013 is a partial year; noted throughout the analysis rather than glossed over)

## Approach

**1. Data Cleaning (Power Query)**
- Corrected the `Year` column from text to whole number
- Fixed a stray leading space in the `Sales` column header
- Validated the dataset for duplicates and null values (confirmed clean — 0 duplicates, 0 blanks across all 700 rows)
- Added a `Profit Category` calculated column (Loss / Low / Medium / High Profit) to enable quick profitability segmentation

**2. Data Modeling**
- Built a dedicated `Calendar` date table using `CALENDAR()`, marked it as an official Date Table, and related it to the fact table
- This was a deliberate fix: using the raw `Year` column directly with `SAMEPERIODLASTYEAR()` initially produced blank results due to a filter context conflict between the raw column and the date column. Routing time intelligence through a proper calendar table resolved it — a good example of diagnosing *why* a DAX formula returns blank rather than just re-writing it until something works.

**3. DAX Measures**
Nine core measures built to support the dashboard:
`Total Sales` · `Total Profit` · `Total Units Sold` · `Average Discount` · `Profit Margin` · `Year-to-Date Sales` · `Year-to-Date Profit` · `Previous Year Profit` · `Growth Percentage`

**4. Dashboard (6 pages)**
| Page | Contents |
|---|---|
| Profit Trend Analysis | Monthly and yearly profit trend line charts |
| Regional Profit Analysis | Profit by Country and Segment (bar charts) |
| Global Profit Distribution | World map, profit by country |
| Product Performance Analysis | Clustered column chart, top vs. bottom products |
| Category-Wise Performance | Treemap, product-level profit share |
| KPI Visualization | 5 summary KPI cards + Country / Year / Product / Segment slicers |

## Key Findings

- **Enterprise segment is running a net loss** (-0.6M) across *every single product*, despite a healthy 14.23% overall profit margin — the problem is segment-specific, not product-specific
- **Heavier discounting actively erodes margin**: Low discount band achieves 17.87% margin vs. just 9.07% for the High discount band — nearly halved, despite raw discount $ and raw profit $ showing a mild positive correlation
- **Government is the dominant segment in every single country** (all 5), contributing more than double the next-best segment
- **Paseo is the standout product**, and its most profitable pairing is specifically Paseo × Canada — the single highest product-country combination in the dataset
- Profit grew **235%** from 2013 to 2014 (caveat: 2013 only has 4 months of data, so this isn't a full like-for-like comparison — stated explicitly rather than presented as a clean headline number)
- A recurring **seasonal dip in November followed by a December surge** appears in both years, suggesting a real, plannable pattern rather than noise

## Repository Contents

```
├── README.md
├── Capstone_Sales_Profitability.pbix     # Full Power BI file (all pages, model, measures)
├── /screenshots                          # Dashboard page exports (PNG)
└── /documentation
    └── Project_Report.pdf                # Full write-up: methodology, screenshots, all analytical Q&A
```

## How to View

- **Full interactivity:** Open `Capstone_Sales_Profitability.pbix` in Power BI Desktop (free)
- **Quick look:** See `/screenshots` for static exports of each dashboard page, or the PDF report for the complete analysis with commentary

## Author

Jaspreet Singh Juneja
[LinkedIn] · [Portfolio link, if applicable]
