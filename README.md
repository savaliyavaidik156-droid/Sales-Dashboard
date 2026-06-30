# Global Superstore — Sales & Profitability Analysis

**Power BI case study analyzing 4 years of global retail data across 5 markets and 23 regions.**

![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-F2C811?logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Measures-yellow)
![Excel](https://img.shields.io/badge/Excel-Data%20Source-217346?logo=microsoftexcel&logoColor=white)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange)

---

## Overview

This project analyzes the Global Superstore dataset (2012–2015) to identify what's driving — and draining — profitability across products, regions, customer segments, and discounting strategy. The goal was to move past "what sold" and answer "where is the business actually making, or losing, money, and why."

The analysis is built as an interactive Power BI dashboard (`sales_dashboard.pbix`) on top of the raw transactional dataset (`global_superstore_2016.xlsx`).

## Dataset

| Attribute | Detail |
|---|---|
| Source file | `global_superstore_2016.xlsx` |
| Sheets | Orders, Returns, People |
| Order records | 51,290 line items across 25,728 orders |
| Date range | Jan 2012 – Dec 2015 (4 years) |
| Customers | 17,415 unique |
| Products | 3,788 unique |
| Markets | 5 — USCA, Europe, Asia Pacific, LATAM, Africa |
| Regions | 23 |
| Segments | Consumer, Corporate, Home Office |
| Categories | Technology, Furniture, Office Supplies (17 sub-categories) |

## Tools Used

- **Power BI Desktop** — data modeling, DAX measures, interactive visuals
- **Excel** — source data
- **DAX** — custom measures for sales, profit, margin, and discount KPIs

## Business Questions

1. How profitable is the business overall, and is growth improving margin or just hiding problems?
2. Which categories and sub-categories drive profit, and is any of them quietly losing money?
3. Does discounting help close sales, or does it destroy profit past a certain point?
4. Which markets and regions are profitable, and which are operating at a loss?
5. Do customer segment or shipping speed meaningfully affect profitability?
6. How much revenue and profit is exposed to product returns?

## Dashboard

### Page 1 — Executive Overview (built)

| Visual | Shows |
|---|---|
| KPI strip | Total Sales, Total Profit, Profit Margin %, Number of Orders, Avg Discount % |
| Monthly trend (combo chart) | Total Sales & Total Profit (left axis) vs. Profit Margin % (right axis), by month |
| Profit by Category | Clustered bar chart |
| Profit by Segment | Donut chart |
| Sales & Profit by Country | Filled map |
| Profit Margin % by Market | Column chart |
| Filters | Year, Category, Market, Segment (slicers) |

### Pages 2–3 (planned)

Not yet built. Based on the gaps in Page 1, the logical next pages are:

- **Page 2 — Product & Discount Deep-Dive**: sub-category profitability table, discount-band vs. margin chart, top/bottom 10 products by profit — built around the Tables/discount finding below.
- **Page 3 — Customer, Returns & Regional Drill-Through**: top customers, return rate by region, ship mode cost vs. margin, order priority view, with drillthrough from the country map.

## Key Insights

### 1. Headline numbers

| Metric | Value |
|---|---|
| Total Sales | $12,642,502 |
| Total Profit | $1,467,457 |
| Profit Margin | 11.61% |
| Avg Order Value | $491.39 |
| Avg Discount | 14.29% |
| Total Shipping Cost | $1,358,086 |

### 2. One sub-category is bleeding money — and discounting is why

Of 17 sub-categories, **Tables is the only one losing money overall**: -$64,083 profit on $757,042 in sales (-8.46% margin). Every other sub-category is profitable, ranging from Fasteners (+15.5% margin) to Paper (+24.0% margin).

The cause is visible in the data: Tables carries the **highest average discount of any sub-category, at 29.1%**, against a dataset-wide average of 14.29%. Split by discount band, Tables is profitable at 0% discount (23% margin, $60,447 profit), turns negative past 20% discount, and at 50%+ discount loses $65,026 on just $55,921 of sales — a -116% margin. The sub-category isn't structurally unprofitable; it's being discounted past the point of profitability.

### 3. The discount-to-margin relationship is strong, and dataset-wide

| Discount band | Margin |
|---|---|
| 0% | 25.32% |
| 0–10% | 17.23% |
| 10–20% | 9.86% |
| 20–30% | -5.53% |
| 30–50% | -32.39% |
| 50%+ | -111.02% |

Row-level correlation between discount and profit margin is **-0.85** — one of the strongest relationships in the dataset. Discounts above roughly 20% reliably produce losses across the business, not just in Furniture.

### 4. Category profitability: Technology and Office Supplies are carrying Furniture

| Category | Sales | Profit | Margin |
|---|---|---|---|
| Technology | $4,744,558 | $663,779 | 13.99% |
| Office Supplies | $3,787,493 | $518,596 | 13.69% |
| Furniture | $4,110,452 | $285,083 | 6.94% |

Furniture has sales comparable to Technology but less than half the margin, almost entirely explained by Tables dragging the category average down — Chairs, Bookcases, and Furnishings are each individually profitable at 9–11% margin.

### 5. Growth is strong, but margin isn't improving with scale

| Year | Sales | YoY Growth | Profit Margin |
|---|---|---|---|
| 2012 | $2,259,451 | — | 11.02% |
| 2013 | $2,677,439 | +18.5% | 11.48% |
| 2014 | $3,405,746 | +27.2% | 11.95% |
| 2015 | $4,299,866 | +26.3% | 11.73% |

Sales nearly **doubled from 2012 to 2015 (+90%)**, but margin moved less than one percentage point over the same period. The business is scaling revenue, not unit economics — worth flagging against any pure growth narrative.

### 6. Market and region performance is uneven

| Market | Sales | Profit | Margin |
|---|---|---|---|
| Europe | $3,287,336 | $449,552 | **13.68%** |
| USCA | $2,364,129 | $304,214 | 12.87% |
| LATAM | $2,164,605 | $221,643 | 10.24% |
| Asia Pacific | $4,042,658 | $403,176 | 9.97% |
| Africa | $783,773 | $88,872 | 11.34% |

Asia Pacific generates the most sales but has the weakest margin among the major markets; Europe is smaller but more profitable per dollar sold.

At the region level, three regions are running at an outright loss: **Central Asia (-37.71%), Western Africa (-28.99%), and Western Asia (-17.00%)**. Southeastern Asia is barely above breakeven at 2.02% despite $884,423 in sales — a strong candidate for a dedicated regional drill-down on Page 3.

### 7. Segment and shipping mode are not major profitability levers

| Segment | Margin | Orders |
|---|---|---|
| Consumer | 11.51% | 13,291 |
| Corporate | 11.54% | 7,724 |
| Home Office | 11.99% | 4,713 |

| Ship Mode | Sales Share | Margin | Avg Ship Cost |
|---|---|---|---|
| Standard Class | 60% | 11.75% | $20.09 |
| Second Class | 20% | 11.40% | $30.56 |
| First Class | 14% | 11.37% | $41.12 |
| Same Day | 5% | 11.42% | $43.00 |

Margin is nearly flat across both segment and ship mode, within about half a point. Shipping cost roughly doubles for faster delivery, but pricing already absorbs it. Neither variable is where the profitability problem lives — discount and sub-category are.

### 8. Returns are contained, but concentrated in a few regions

4.19% of orders (1,079 of 25,728) were returned, tied to $525,932 in sales and $61,371 in recorded profit. Return rates aren't evenly spread: **Western US, Eastern Asia, Southern Europe, Southern Africa, and Southern US** all return at 5.1–5.5%, noticeably above the 4.19% average — good candidates for root-cause review on product quality or fulfillment accuracy.

## Key DAX Measures

| Measure | Purpose | Formula pattern |
|---|---|---|
| Total Sales | Sum of revenue | `SUM(Orders[Sales])` |
| Total Profit | Sum of profit | `SUM(Orders[Profit])` |
| Profit Margin % | Profit as % of sales | `DIVIDE([Total Profit], [Total Sales], 0)` |
| Avg Discount % | Average discount applied | `AVERAGE(Orders[Discount])` |
| NO. Of Order | Distinct order count | `DISTINCTCOUNT(Orders[Order ID])` |

## Recommendations

1. **Cap discounts on Tables at roughly 15–20%.** Above that threshold the sub-category consistently loses money; below it, it's solidly profitable.
2. **Set a discount ceiling policy around 20% business-wide**, not just for Tables — the -0.85 correlation holds across categories.
3. **Review Central Asia, Western Africa, and Western Asia** before further sales investment there; current unit economics are negative regardless of volume.
4. **Use Europe and Eastern/Southern Asia (13–19% margin) as the benchmark**, rather than chasing Asia Pacific's higher sales volume alone.
5. **Root-cause the above-average return regions** — Western US, Eastern Asia, Southern Europe, Southern Africa, Southern US — since even a 1-point reduction there reclaims meaningful sales and profit exposure.
6. **Treat segment and ship mode as operational variables, not profitability levers** — focus margin-improvement work on discount policy and sub-category mix instead.

## Repository Structure

```
├── global_superstore_2016.xlsx   # Raw source data (Orders, Returns, People)
├── sales_dashboard.pbix          # Power BI report (Page 1 live, 2-3 in progress)
└── README.md                     # This file
```
## About

Built as part of a Business Analyst portfolio project, alongside the Blinkit Sales Dashboard. Focused on demonstrating end-to-end BA workflow: data modeling, DAX, and translating dashboard output into business-ready insight and recommendations.
