# 🛒 E-Commerce Analytics Intelligence Dashboard
### Power BI | Multi-Page | Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-20%2B%20Measures-blue?style=for-the-badge)
![Star Schema](https://img.shields.io/badge/Star%20Schema-7%20Tables-green?style=for-the-badge)
![Pages](https://img.shields.io/badge/Dashboard%20Pages-4-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen?style=for-the-badge)

### 🔴 [View Live Dashboard →](https://app.powerbi.com/view?r=eyJrIjoiZDA0M2E1YWUtMGU2NC00NDk2LTg1MjUtOTRhNmM5MDk5OTEzIiwidCI6IjdlMzEwODQ1LTg0ZTEtNGRiOC1hZjk4LTcwNDA0MTkwZDhkZSJ9)

---

## 📌 Project Overview

A full-scale Power BI dashboard built on a **$12.64M e-commerce dataset** covering **21,629 orders**, **686 customers**, and **6 product categories**. Designed as a decision-support system — not just a collection of charts — with every visual mapped to a specific business question for a specific audience.

| Metric | Value |
|--------|-------|
| 💰 Total Revenue | $12.64M |
| 📦 Total Orders | 21,629 |
| 👥 Total Customers | 686 |
| 📊 Dashboard Pages | 4 (+ 4 supporting pages) |
| 🧮 DAX Measures | 20+ |
| 🗂️ Schema Tables | 7 (1 Fact + 6 Dimensions) |
| 🔒 RLS Roles | 2 Dynamic Roles |

---

## 🗂️ Dashboard Pages

### Page 1 — Executive Overview
> *CEO's morning briefing in a dashboard*

- **KPI Cards:** Total Revenue ($12.64M, +3.7% YoY), Orders (21,629, +5.6% YoY), Profit ($10M, +3.6% YoY), Avg Order Value ($584.50), Profit Margin % (0.75%)
- **Monthly Revenue Trends** — Line chart with MoM Growth % dual axis overlay
- **YoY Comparison** — Clustered bar comparing this year vs. prior year revenue by month
- **Order Status Distribution** — Donut chart: Completed (82.31%) / In Progress / Returned / Cancelled
- **YTD vs Running Total** — Area chart showing cumulative revenue growth Jan–Dec

---

### Page 2 — Sales & Product Analysis
> *Identify revenue drivers, margin leaders, and underperformers*

- **Revenue by Category** — Horizontal ranked bar (Electronics: $8.58M leads, but at low margin)
- **Revenue vs Profit Margin** — Signature dual-axis chart (column = revenue, line = margin %) — exposes the Electronics margin trap
- **Top Performing Product Matrix** — Sortable table: Revenue | Orders | Profit | Margin % | Return Rate | Arrow trend
- **Dynamic KPI Selector** — Field parameter toggles treemap between Revenue / Orders / Customers / Profit / Margin % / Return Rate
- **Drillthrough:** Right-click any product → Product Detail page with 12-month trend, full order history, stock level

---

### Page 3 — Customer Insights
> *Segment, retain, and grow the customer base*

- **KPI Cards:** 686 Customers | 259 High Value Customers | $18,429 Revenue per Customer | 49.12% Retention Rate
- **Revenue by Segment** — Bar chart: High Value ($46,060 avg) | Medium Value ($2,506) | Low Value ($497)
- **Customer Value Matrix** — Scatter plot: X = Orders, Y = Revenue, Bubble Size = Recency → Champions / Big Spenders / Loyal Low-Value / At-Risk quadrants
- **Retention Trend** — Line chart showing monthly retention rate (Jan: 70% → Dec: 49.12%) with 70% target reference line
- **Geographic Revenue Map** — Filled US map, revenue intensity by state
- **Customer Leaderboard** — Sortable: Name | Revenue | Orders | Segment | Last Purchase | LTV
- **Drillthrough:** Right-click any customer → Customer Detail page with 24-month trend, order history, category preferences

---

### Page 4 — Operations Dashboard
> *Monitor delivery performance, cancellations, and efficiency*

- **KPI Cards:** Cancellation Rate (2%) | Return Rate (13%) | Delivery Success (82%) | Avg Shipping Days (3.0)
- **Order Status by Month** — Stacked bar: Completed / Cancelled / In Progress / Returned — month by month
- **Cancellation Heatmap** — Matrix: Rows = State, Columns = Category, Color = Cancellation intensity (white → dark red)
- **Delivery Delay Analysis** — Dual-axis: On-Time vs Delayed counts by shipping provider (FedEx, DHL, Bluedart)
- **Shipping Provider Performance** — Horizontal bar ranked by delivery success rate vs SLA target reference line

---

## 🏗️ Data Model — Star Schema

```
                    dim_Date
                       │
dim_Category ──── fact_sales ──── dim_Products
                       │
dim_Customers ─────────┤──────── dim_Sellers
                       │
                   dim_Shipping (shipping table)
```

| Table | Type | Rows | Key Fields |
|-------|------|------|------------|
| `fact_sales` | Fact | ~21K | order_id, customer_id, product_id, seller_id, date_id, quantity, price, status |
| `dim_Date` | Dimension | 365+ | date, month, quarter, year, month_name |
| `dim_Products` | Dimension | — | product_id, name, category_id, COGS, price |
| `dim_Category` | Dimension | 6 | category_id, category_name |
| `dim_Customers` | Dimension | 686 | customer_id, name, state, segment |
| `dim_Sellers` | Dimension | — | seller_id, seller_name |
| `shipping` | Fact/Bridge | — | order_id, provider, shipping_date, delivery_status, return_date |

**Design Decisions:**
- All relationships: Many-to-One, **single-direction** filter flow (Dimension → Fact)
- `dim_Date` marked as official Date Table
- Auto Date/Time disabled (reduces model size ~40%)
- `fact_sales` merges order header + order items for unified order-level and product-level analysis

---

## 🧮 Key DAX Measures

```dax
-- Total Revenue (SUMX for row-by-row calculation)
Total Revenue =
SUMX(fact_sales, fact_sales[quantity] * fact_sales[price_per_unit])

-- YoY Growth %
YoY Growth % =
VAR PY = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(dim_Date[Date]))
RETURN IF(ISBLANK(PY) || PY = 0, BLANK(), DIVIDE([Total Revenue] - PY, PY))

-- Customer Retention Rate (INTERSECT method)
Customer Retention Rate =
VAR CurrentYr = CALCULATETABLE(VALUES(fact_sales[customer_id]), DATESYTD(dim_Date[Date]))
VAR PriorYr   = CALCULATETABLE(VALUES(fact_sales[customer_id]), SAMEPERIODLASTYEAR(DATESYTD(dim_Date[Date])))
RETURN DIVIDE(COUNTROWS(INTERSECT(CurrentYr, PriorYr)), COUNTROWS(PriorYr), 0)

-- Dynamic KPI Switch
Selected KPI =
SWITCH(SELECTEDVALUE('KPI Options'[KPI Name], "Revenue"),
    "Revenue",     [Total Revenue],
    "Orders",      [Total Orders],
    "Profit",      [Total Profit],
    "Margin %",    [Profit Margin %],
    "Return Rate", [Return Rate],
    [Total Revenue])
```

**Full Measure Library includes:**
`Total Revenue` · `Total Orders` · `Total Customers` · `Total Profit` · `Profit Margin %` · `MoM Growth %` · `YoY Growth %` · `YTD Revenue` · `Running Total Revenue` · `Revenue Last Year` · `Revenue Arrow` · `Revenue % of Total` · `Return Rate` · `Cancellation Rate` · `Cancellation Count` · `Lost Revenue (Cancellations)` · `Delivery Success Rate` · `Provider Delay Rate` · `Customer Retention Rate` · `Revenue per Customer` · `Customer LTV` · `Selected KPI` · `Dynamic Page Title`

---

## ✨ Advanced Features

| Feature | Implementation |
|---------|---------------|
| **Dynamic KPI Selector** | Disconnected `KPI Options` table + `SELECTEDVALUE` SWITCH measure |
| **Product Drillthrough** | Right-click product → detail page (trend, orders, stock) |
| **Customer Drillthrough** | Right-click customer → 24-month history, category mix |
| **Custom Tooltip Pages** | 320×240px pages with mini KPI cards — hover any data point |
| **Cross-Page Slicer Sync** | Year + Category synced across all 4 pages via Sync Slicers pane |
| **Conditional Formatting** | Icon sets (margin %), gradient scales (revenue), heatmap (cancellations), data bars (YoY) |
| **Dynamic Titles** | `SELECTEDVALUE`-driven titles showing active filter context on every page |
| **Row-Level Security** | Seller View (`USERPRINCIPALNAME()`) + Regional Manager View (mapping table) — 1 dynamic role handles 50+ sellers |

---

## 📐 Calculated Columns

```dax
-- Customer Segment (in dim_Customers)
Customer Segment =
VAR Rev = CALCULATE([Total Revenue], ALLEXCEPT(dim_Customers, dim_Customers[customer_id]))
RETURN SWITCH(TRUE(), Rev >= 5000, "High Value", Rev >= 1500, "Medium Value", Rev > 0, "Low Value", "Inactive")

-- Delivery Delay Flag (in shipping table)
Delivery Delay Flag =
VAR Days = DATEDIFF(shipping[shipping_date], IF(ISBLANK(shipping[return_date]), TODAY(), shipping[return_date]), DAY)
RETURN SWITCH(TRUE(),
    ISBLANK(shipping[shipping_date]),        "Unknown",
    shipping[delivery_status] = "Delivered", "On Time",
    Days > 10,                               "Severely Delayed",
    Days > 7,                                "Delayed",
    "In Transit")
```

---

## 💡 Business Insights Surfaced

| Insight | Dashboard Signal | Recommended Action |
|---------|-----------------|-------------------|
| **Electronics Margin Trap** | High revenue ($8.58M), low margin on dual-axis chart | Bundle high-margin accessories with electronics |
| **Revenue Concentration Risk** | Top customers drive disproportionate revenue (scatter quadrant) | Launch VIP retention program for Champions |
| **Retention Decline** | Retention fell from 70% (Jan) to 49% (Dec) | Activate win-back campaigns for churned High Value customers |
| **FedEx Delay Problem** | Highest delayed order count in Delivery Delay Analysis | Renegotiate SLA or redistribute volume to Bluedart |
| **Q4 Seasonal Spike** | Revenue trend peaks Oct–Dec | Pre-build inventory in Q3, run promotions in Q1–Q2 |

---

## 🔒 Row-Level Security

```dax
-- Seller View Role (applied to dim_Sellers)
[seller_name] = USERPRINCIPALNAME()
-- Filter propagates: dim_Sellers → fact_sales → dim_Products

-- Regional Manager View (applied to dim_Customers)
[state] IN CALCULATETABLE(VALUES(RegionAccess[state]),
              RegionAccess[manager_email] = USERPRINCIPALNAME())
```

---

## 🛠️ Tech Stack

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-20%2B%20Measures-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Power BI Service](https://img.shields.io/badge/Power%20BI%20Service-Deployed-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)

| Tool | Layer | Usage in This Project |
|------|-------|-----------------------|
| **Power BI Desktop** | Visualization | 4-page dashboard design, 20+ DAX measures, star schema modeling, RLS configuration, drillthrough & tooltip pages |
| **Power Query (M)** | Transformation | Data ingestion from CSV, column profiling, table merging (orders + order items into fact_sales), pre-computed transformations to offload DAX query time |
| **DAX** | Calculation | 20+ measures (SUMX, SAMEPERIODLASTYEAR, INTERSECT, SWITCH, SELECTEDVALUE) + 3 calculated columns (Customer Segment, Delivery Delay Flag, Days Since Last Order) |
| **SQL** | Data Modeling | Star schema design, data validation queries, relationship logic between fact and dimension tables |
| **Python** | Data Processing | Dataset generation, synthetic data scripting, Pandas-based data cleaning and pre-processing pipeline |
| **Power BI Service** | Deployment | Published to workspace, scheduled daily refresh at 6 AM, dashboard pinning, KPI email alerts, RLS role assignment to security groups — [🔴 Live Here](https://app.powerbi.com/view?r=eyJrIjoiZDA0M2E1YWUtMGU2NC00NDk2LTg1MjUtOTRhNmM5MDk5OTEzIiwidCI6IjdlMzEwODQ1LTg0ZTEtNGRiOC1hZjk4LTcwNDA0MTkwZDhkZSJ9) |

---

## 📁 Repository Structure

```
ecommerce-analytics-dashboard/
│
├── 📊 E_Commerce_Analytics_Dashboard.pbix     # Main Power BI file
│
├── 📂 data/
│   ├── fact_sales.csv
│   ├── dim_date.csv
│   ├── dim_products.csv
│   ├── dim_category.csv
│   ├── dim_customers.csv
│   ├── dim_sellers.csv
│   └── shipping.csv
│
├── 📂 screenshots/
│   ├── page1_executive_overview.png
│   ├── page2_sales_product.png
│   ├── page3_customer_insights.png
│   └── page4_operations.png
│
├── 📂 docs/
│   ├── data_dictionary.md
│   ├── dax_measures.md
│   └── design_blueprint.md
│
└── README.md
```

---

## 🚀 How to Use

1. **Clone this repository**
   ```bash
   git clone https://github.com/ajayakumar-pradhan/ecommerce-analytics-dashboard.git
   ```

2. **Open the PBIX file** in Power BI Desktop (version 2.0+ recommended)

3. **Load the data** — place all CSV files from `/data` folder in the same directory, then refresh the dataset

4. **Explore the dashboard** — use Year / Quarter / Category slicers to filter; right-click any product or customer to drillthrough

5. **Test RLS** — `Modeling > View As > Select Role` to simulate seller or manager views

---

## 👤 Author

**Ajaya Kumar Pradhan**
Data Analyst | Power BI | SQL | Python | Machine Learning

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://linkedin.com/in/ajayakumarpradhan)
[![GitHub](https://img.shields.io/badge/GitHub-Portfolio-black?style=flat&logo=github)](https://github.com/ajayakumar-pradhan)

---

## 📄 License

This project is open for portfolio and educational use. Please credit the author if reused.

---

*Built as part of a production-grade Power BI portfolio demonstrating enterprise dashboard design, advanced DAX, star schema modeling, and business intelligence storytelling.*
