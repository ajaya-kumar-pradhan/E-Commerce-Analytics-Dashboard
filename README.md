# 🛒 FinCart360 — E-Commerce Analytics Dashboard

<div align="center">

**$12.64M in sales. 21,629 orders. One dashboard that shows exactly where the money is — and where it isn't.**
*A production-grade Power BI platform covering sales performance, customer intelligence, product profitability, and operational efficiency.*

<br>

[![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://app.powerbi.com/view?r=eyJrIjoiZDA0M2E1YWUtMGU2NC00NDk2LTg1MjUtOTRhNmM5MDk5OTEzIiwidCI6IjdlMzEwODQ1LTg0ZTEtNGRiOC1hZjk4LTcwNDA0MTkwZDhkZSJ9)
[![DAX](https://img.shields.io/badge/DAX-20%2B%20Measures-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)](https://github.com/ajaya-kumar-pradhan)
[![Star Schema](https://img.shields.io/badge/Star%20Schema-7%20Tables-6C3483?style=for-the-badge)](https://github.com/ajaya-kumar-pradhan)
[![RLS](https://img.shields.io/badge/RLS-2%20Dynamic%20Roles-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)](https://github.com/ajaya-kumar-pradhan)
[![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen?style=for-the-badge)](https://github.com/ajaya-kumar-pradhan)

<br>

### 🚀 [View Live Power BI Dashboard →](https://app.powerbi.com/view?r=eyJrIjoiZDA0M2E1YWUtMGU2NC00NDk2LTg1MjUtOTRhNmM5MDk5OTEzIiwidCI6IjdlMzEwODQ1LTg0ZTEtNGRiOC1hZjk4LTcwNDA0MTkwZDhkZSJ9)

</div>

---

## 📌 Overview

**FinCart360** is a full-scale e-commerce decision-support platform — built not as a collection of charts, but as a structured analytics system where every visual maps to a specific business question for a specific audience.

The platform covers four critical lenses: executive performance, product profitability, customer retention, and operational efficiency. From the CEO's morning KPI brief to a seller checking their own numbers via Row-Level Security — it handles all of it from a single `.pbix` file.

> **The Business Problem:** E-commerce teams drown in data but starve for insight. Revenue looks healthy until you check margins. Customers look loyal until you check retention. Top-selling products often carry the worst profitability.
>
> **The Solution:** A 4-page interactive dashboard that surfaces the right signal to the right stakeholder — with drillthrough, dynamic segmentation, and RLS baked in from day one.

---

## 📊 Key Features

- 📈 **Executive KPI command center** — Revenue, orders, profit, AOV, and margin tracked with MoM and YoY overlays in a single view
- 🔍 **Product profitability exposure** — Dual-axis Revenue vs. Margin % chart that immediately exposes high-revenue, low-margin traps (looking at you, Electronics)
- 👥 **Customer segmentation engine** — Scatter-based value matrix classifies 686 customers into Champions, Big Spenders, Loyal Low-Value, and At-Risk quadrants
- 📦 **Operations monitoring** — Cancellation heatmap, delivery delay analysis by shipping provider, and return rate tracking across all fulfillment channels
- 🔁 **Drillthrough on every dimension** — Right-click any product or customer to navigate to a dedicated detail page with full 24-month history
- 🔒 **Row-Level Security** — Dynamic roles for 50+ sellers (`USERPRINCIPALNAME()`) and regional managers (mapping table) — each user sees only their data
- 🎛️ **Dynamic KPI selector** — Field parameter + `SWITCH` measure toggles treemap metric between Revenue, Orders, Customers, Profit, Margin %, or Return Rate in one click

---

## 🛠️ Tech Stack

| Layer | Tool / Technology | Usage in This Project |
|---|---|---|
| **BI & Visualization** | Power BI Desktop + Service | 4-page dashboard, drillthrough, tooltip pages, KPI alerts |
| **Data Modeling** | Star Schema (1 Fact + 6 Dims) | Relationship design, filter direction, Date Table setup |
| **Calculations** | DAX — 20+ measures, 3 calc columns | SUMX, INTERSECT, SWITCH, SAMEPERIODLASTYEAR, SELECTEDVALUE |
| **Data Transformation** | Power Query (M Language) | CSV ingestion, order + items merge, pre-compute offloading |
| **Data Source & Prep** | SQL, Python (Pandas), Excel | Schema design, synthetic data generation, cleaning pipeline |
| **Deployment** | Power BI Service | Daily 6AM refresh, RLS roles, dashboard pinning, email alerts |

---

## 📈 Key Metrics & Scale

| Metric | Value |
|---|---|
| 💰 Total Revenue | **$12.64M** |
| 📦 Total Orders | **21,629** |
| 👥 Total Customers | **686** |
| 📊 Dashboard Pages | **4 main + 4 supporting** |
| 🧮 DAX Measures | **20+** |
| 🗂️ Schema Tables | **7 (1 Fact + 6 Dimensions)** |
| 🔒 RLS Roles | **2 Dynamic Roles** |
| 💵 Avg Order Value | **$584.50** |
| 🔁 Customer Retention Rate | **49.12%** |
| ✅ Order Completion Rate | **82.31%** |
| 📉 Cancellation Rate | **2%** |
| 🔄 Return Rate | **13%** |

---

## 🧠 Insights & Business Value

| Insight | Dashboard Signal | Recommended Action |
|---|---|---|
| 💸 **Electronics Margin Trap** | $8.58M revenue — lowest margin on dual-axis chart | Bundle high-margin accessories to lift category profitability |
| 👑 **Revenue Concentration Risk** | Champions quadrant drives outsized share in customer scatter | Launch VIP retention program before these customers churn |
| 📉 **Retention Freefall** | Monthly retention dropped from 70% (Jan) → 49% (Dec) | Activate win-back campaigns targeting churned High Value segment |
| 🚚 **FedEx Delay Spike** | Highest delayed order count across all providers | Renegotiate SLA terms or redistribute volume to Bluedart |
| 🗓️ **Q4 Revenue Concentration** | Revenue trend peaks Oct–Dec in monthly line chart | Build inventory in Q3; deploy promotional campaigns in Q1–Q2 to flatten seasonality |

**Business value delivered:**
> Sellers see only their own data. Regional managers see only their states. Executives see everything — revenue, risk, and retention — from a single morning view. The dashboard doesn't just report what happened; it flags what needs to happen next.

---

## 🖼️ Dashboard Preview

### 1️⃣ Executive Overview
*KPI Cards (Revenue, Orders, Profit, AOV, Margin) · Monthly Revenue Trend · YoY Comparison · Order Status Donut · YTD Running Total*

![Executive Overview](screenshots/page1_executive_overview.png)

---

### 2️⃣ Sales & Product Analysis
*Revenue by Category · Revenue vs Margin % Dual-Axis · Product Performance Matrix · Dynamic KPI Treemap · Product Drillthrough*

![Sales & Product Analysis](screenshots/page2_sales_product.png)

---

### 3️⃣ Customer Insights
*Customer Value Scatter Matrix · Segment Revenue Bars · Retention Trend Line · US Geographic Map · Customer Leaderboard · Customer Drillthrough*

![Customer Insights](screenshots/page3_customer_insights.png)

---

### 4️⃣ Operations
*Cancellation Heatmap (State × Category) · Delivery Delay Analysis · Shipping Provider Rankings · Order Status by Month*

![Operations](screenshots/page4_operations.png)

---

## 🏗️ Data Architecture

**Star Schema Design:**

```
                    dim_Date
                       │
dim_Category ──── fact_sales ──── dim_Products
                       │
dim_Customers ─────────┤──────── dim_Sellers
                       │
                   dim_Shipping
```

```sql
-- Core Fact Table
fact_sales      → order_id, customer_id, product_id, seller_id, date_id,
                  quantity, price_per_unit, status

-- Shipping Bridge
dim_Shipping    → order_id, provider, shipping_date, delivery_status, return_date

-- Dimension Tables
dim_Date        → date_id, date, month, quarter, year, month_name
dim_Products    → product_id, name, category_id, COGS, price
dim_Category    → category_id, category_name
dim_Customers   → customer_id, name, state, segment
dim_Sellers     → seller_id, seller_name
```

**Design Decisions:**
- All relationships: Many-to-One, single-direction filter flow (Dimension → Fact)
- `dim_Date` marked as official Date Table; Auto Date/Time disabled (reduces model size ~40%)
- `fact_sales` merges order header + order items into a unified table for both order-level and product-level analysis

---

## 💡 Key DAX Measures

```dax
-- Revenue (row-by-row SUMX for accuracy)
Total Revenue =
SUMX(fact_sales, fact_sales[quantity] * fact_sales[price_per_unit])

-- YoY Growth %
YoY Growth % =
VAR PY = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(dim_Date[Date]))
RETURN IF(ISBLANK(PY) || PY = 0, BLANK(), DIVIDE([Total Revenue] - PY, PY))

-- Customer Retention Rate (INTERSECT method)
Customer Retention Rate =
VAR CurrentYr = CALCULATETABLE(VALUES(fact_sales[customer_id]), DATESYTD(dim_Date[Date]))
VAR PriorYr   = CALCULATETABLE(VALUES(fact_sales[customer_id]),
                    SAMEPERIODLASTYEAR(DATESYTD(dim_Date[Date])))
RETURN DIVIDE(COUNTROWS(INTERSECT(CurrentYr, PriorYr)), COUNTROWS(PriorYr), 0)

-- Dynamic KPI Selector
Selected KPI =
SWITCH(SELECTEDVALUE('KPI Options'[KPI Name], "Revenue"),
    "Revenue",     [Total Revenue],
    "Orders",      [Total Orders],
    "Profit",      [Total Profit],
    "Margin %",    [Profit Margin %],
    "Return Rate", [Return Rate],
    [Total Revenue])
```

**Full measure library:**
`Total Revenue` · `Total Orders` · `Total Customers` · `Total Profit` · `Profit Margin %` · `MoM Growth %` · `YoY Growth %` · `YTD Revenue` · `Running Total Revenue` · `Revenue Last Year` · `Revenue Arrow` · `Revenue % of Total` · `Return Rate` · `Cancellation Rate` · `Lost Revenue (Cancellations)` · `Delivery Success Rate` · `Provider Delay Rate` · `Customer Retention Rate` · `Revenue per Customer` · `Customer LTV` · `Selected KPI` · `Dynamic Page Title`

---

## 🔢 Calculated Columns

```dax
-- Customer Segment (dim_Customers)
Customer Segment =
VAR Rev = CALCULATE([Total Revenue], ALLEXCEPT(dim_Customers, dim_Customers[customer_id]))
RETURN SWITCH(TRUE(),
    Rev >= 5000, "High Value",
    Rev >= 1500, "Medium Value",
    Rev >  0,    "Low Value",
                 "Inactive")

-- Delivery Delay Flag (dim_Shipping)
Delivery Delay Flag =
VAR Days = DATEDIFF(shipping[shipping_date],
               IF(ISBLANK(shipping[return_date]), TODAY(), shipping[return_date]), DAY)
RETURN SWITCH(TRUE(),
    ISBLANK(shipping[shipping_date]),        "Unknown",
    shipping[delivery_status] = "Delivered", "On Time",
    Days > 10,                               "Severely Delayed",
    Days > 7,                                "Delayed",
                                             "In Transit")
```

---

## 🔒 Row-Level Security

```dax
-- Seller View (applied to dim_Sellers)
-- Each seller sees only their own orders; filter propagates → fact_sales → dim_Products
[seller_name] = USERPRINCIPALNAME()

-- Regional Manager View (applied to dim_Customers)
-- Manager sees only states assigned to them in RegionAccess mapping table
[state] IN CALCULATETABLE(
    VALUES(RegionAccess[state]),
    RegionAccess[manager_email] = USERPRINCIPALNAME()
)
```

> One dynamic Seller role handles 50+ sellers automatically — no hardcoded filters, no role per user.

---

## ✨ Advanced Features

| Feature | Implementation |
|---|---|
| **Dynamic KPI Selector** | Disconnected `KPI Options` table + `SELECTEDVALUE` SWITCH measure |
| **Product Drillthrough** | Right-click → detail page with 12-month trend, order history, stock level |
| **Customer Drillthrough** | Right-click → 24-month history, category preferences, LTV |
| **Custom Tooltip Pages** | 320×240px hover pages with mini KPI cards on every data point |
| **Cross-Page Slicer Sync** | Year + Category synced across all 4 pages via Sync Slicers pane |
| **Conditional Formatting** | Icon sets (margin %), gradient scales (revenue), heatmap (cancellations), data bars (YoY) |
| **Dynamic Page Titles** | `SELECTEDVALUE`-driven titles reflect active filter context on every page |
| **Row-Level Security** | Seller + Regional Manager roles — 1 dynamic rule handles 50+ users |

---

## 📂 Project Structure

```
FinCart360-Ecommerce-Analytics/
│
├── 📊 E_Commerce_Analytics_Dashboard.pbix     # Main Power BI file
│
├── 📁 data/
│   ├── fact_sales.csv
│   ├── dim_date.csv
│   ├── dim_products.csv
│   ├── dim_category.csv
│   ├── dim_customers.csv
│   ├── dim_sellers.csv
│   └── shipping.csv
│
├── 📁 screenshots/
│   ├── page1_executive_overview.png
│   ├── page2_sales_product.png
│   ├── page3_customer_insights.png
│   └── page4_operations.png
│
├── 📁 docs/
│   ├── data_dictionary.md
│   ├── dax_measures.md
│   └── design_blueprint.md
│
└── 📄 README.md
```

---

## 🚀 How to Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/ajaya-kumar-pradhan/ecommerce-analytics-dashboard.git

# 2. Open the .pbix file in Power BI Desktop (v2.0+ recommended)

# 3. Place all CSV files from /data in the same directory, then refresh the dataset

# 4. Explore: use Year / Quarter / Category slicers to filter
#    Right-click any product or customer to drillthrough

# 5. Test RLS: Modeling > View As > Select Role
#    to simulate Seller or Regional Manager views
```

---

## 👤 About Me

**Ajaya Kumar Pradhan** — Data Analyst | Power BI Developer

I build analytics platforms that turn business data into clear, fast decisions. My work spans the full stack — data modeling, DAX, dashboard design, and deployment — with a focus on making insights accessible to every stakeholder, technical or not.

**Core Skills:** `Power BI` `DAX` `SQL` `Python` `Star Schema` `Power Query` `RLS` `ETL` `Customer Analytics`

<br>

📧 [ajayapradhan.connect@gmail.com](mailto:ajayapradhan.connect@gmail.com)
🔗 [linkedin.com/in/ajayakumarpradhan](https://www.linkedin.com/in/ajayakumarpradhan/)
💻 [github.com/ajaya-kumar-pradhan](https://github.com/ajaya-kumar-pradhan)

---

<div align="center">

*If this project helped or inspired you, consider giving it a ⭐ — it helps others find it too.*

</div>
