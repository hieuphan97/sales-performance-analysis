# 📊 Sales Performance Analysis | Business Performance Dashboard | Power BI

*Analyze & Discover the Global Sales Performance Insights of a Multi-Market Retail Business | Power BI*

**+ Business question:** How is the business performing across markets, products, and time — and where should leadership focus resources to maximize growth and profitability?

**+ Domain:** Multi-market Retail / Global Sales

> 📌 *This project delivers a strategic decision-support dashboard built for Senior Management, enabling data-driven decisions on market expansion, product portfolio optimization, and revenue growth.*

**Author:** Phan Trung Hiếu

**Date:** 2024

**Tools Used:** Power BI Desktop

---

## 📑 Table of Contents

1. [📌 Background & Overview](#-background--overview)
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)
3. [🧠 Design Thinking Process](#-design-thinking-process)
4. [📊 Key Insights & Visualizations](#-key-insights--visualizations)
5. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)

---

## 📌 Background & Overview

### Objective:

### 📖 What is this project about?

This project analyzes global sales performance data across markets, product categories, and time periods using Power BI. The objective is to provide Senior Management with a comprehensive, multi-dimensional view of business health to support fast and accurate strategic decisions.

✔️ Identify overall business performance trends (Revenue, Profit, Profit Margin, Quantity, Orders).

✔️ Analyze market performance to determine which regions to invest in or scale back.

✔️ Evaluate product portfolio to identify star products and underperformers.

✔️ Provide granular transaction-level reporting for drill-down analysis.

✔️ Enable comparisons against prior year (PY) performance across all dimensions.

> 📌 *The core business questions this dashboard answers:*
> 1. *What does the overall business look like right now? (Are we strong or weak?)*
> 2. *How are individual markets performing? (Where should we attack and where should we defend?)*
> 3. *Which product groups are driving growth? (What are our stars and what are our laggards?)*

### 👤 Who is this project for?

✔️ **Senior Management & C-Suite** — for strategic resource allocation decisions

✔️ **Regional Sales Managers** — for market-level performance monitoring

✔️ **Product Managers** — for portfolio optimization decisions

✔️ **Data Analysts & Business Analysts** — for reporting and further analysis

---

## 📂 Dataset Description & Data Structure

### 📌 Data Source

- **Source:** Internal sales transaction dataset (provided as compressed archive)
- **Format:** `.rar` compressed file containing structured tables
- **Time Range:** 2011 – 2014

### 📊 Data Structure & Relationships

#### 1️⃣ Tables Used:

The dataset follows a **Star Schema** with **3 core tables**: `Orders` (Fact), `People`, and `Returns`.

In Power BI, these were expanded into a dimensional model with the following tables:

| Table | Type | Description |
|---|---|---|
| `Fact_Sales` | Fact | Core transaction records (Sales, Profit, Quantity) |
| `Dim_Customer` | Dimension | Customer details and segmentation |
| `Dim_Product` | Dimension | Product hierarchy (Category, Sub-Category, Product Name) |
| `Dim_Order` | Dimension | Order information (Order ID, Ship Mode) |
| `Dim_OrderDate` | Dimension | Order date calendar table |
| `Dim_ShipDate` | Dimension | Ship date calendar table |
| `Returns` | Reference | Return status per Order ID |
| `People` | Reference | Sales person linked to Region |

#### 2️⃣ Table Schema & Data Snapshot

**Fact_Sales (Orders)**

| Column Name | Data Type | Description |
|---|---|---|
| Order ID | TEXT | Unique identifier per order |
| Customer ID | TEXT | Foreign key to Dim_Customer |
| Product ID | TEXT | Foreign key to Dim_Product |
| Sales | FLOAT | Revenue from the transaction |
| Profit | FLOAT | Profit from the transaction |
| Quantity | INT | Number of units sold |
| Discount | FLOAT | Discount applied |
| Order Date | DATE | Date the order was placed |
| Ship Date | DATE | Date the order was shipped |
| Ship Mode | TEXT | Shipping method |
| Region | TEXT | Sales region |
| Country | TEXT | Country of the order |
| Market | TEXT | Market segment (US, EU, APAC, LATAM, etc.) |
| Segment | TEXT | Customer segment (Consumer, Corporate, Home Office) |

<details>
<summary>Click to expand: Dim_Product Schema</summary>

| Column Name | Data Type | Description |
|---|---|---|
| Product ID | TEXT | Unique product identifier |
| Product Name | TEXT | Full product name |
| Category | TEXT | High-level category (Furniture, Technology, Office Supplies) |
| Sub-Category | TEXT | Sub-level category (Chairs, Phones, Binders, etc.) |

</details>

<details>
<summary>Click to expand: Dim_Customer Schema</summary>

| Column Name | Data Type | Description |
|---|---|---|
| Customer ID | TEXT | Unique customer identifier |
| Customer Name | TEXT | Full customer name |
| Segment | TEXT | Consumer / Corporate / Home Office |
| Postal Code | TEXT | Customer postal code |
| City | TEXT | City |
| State | TEXT | State / Province |
| Country | TEXT | Country |

</details>

#### 3️⃣ Data Relationships:

The model uses **one-to-many** relationships from dimension tables to the Fact_Sales table. `Dim_OrderDate` and `Dim_ShipDate` both connect to Fact_Sales via their respective date fields, enabling time intelligence calculations. `People` connects via `Region` and `Returns` connects via `Order ID`.

<img width="1043" height="686" alt="image" src="https://github.com/user-attachments/assets/36be9ca1-5d5f-4b3e-95c4-de30bdcba5fc" />

---

## 🧠 Design Thinking Process

The dashboard was built following the **Design Thinking methodology**, ensuring the output is centered on the actual needs of the end user (Senior Management).

### 1️⃣ Empathize — Understand the Stakeholder

**Key Stakeholder:** Senior Management (Strategic Decision-Makers)

They need a clear, high-level map of business performance — without having time to analyze raw data themselves. Their core pains include:

- Making million-dollar decisions with fragmented, delayed data
- Wasting time waiting for reports from multiple sources
- Missing market opportunities due to lack of timely information
- Being data-rich but insight-poor

**Their key questions:**
- "Am I missing opportunities in any market?"
- "Why did revenue drop last quarter?"
- "Which products are actually profitable?"
- "Where are our top 3 growth markets?"

### 2️⃣ Define Point of View — Identify What Matters

**Northstar Metric 1:** Total Revenue (Tổng Doanh Thu)
> Measures market penetration and scale of growth. It is the most fundamental indicator of business size and market presence.

**Northstar Metric 2:** Total Profit (Tổng Lợi Nhuận)
> Revenue alone can be misleading. Profit is the ultimate health indicator — it proves that the company's strategy, pricing, and operations are creating sustainable value.

**Key Points of View (Dashboard Pages):**
| Page | Angle | Business Question |
|---|---|---|
| Overview | Time & Aggregated | How is the overall business performing YoY? |
| Market | Geography & Segment | Which markets are gold mines and which are drains? |
| Product | Product Hierarchy | Which products/categories are stars vs. laggards? |
| Report | Granular Transactions | What are the details behind the KPIs? |

### 3️⃣ Ideate — Brainstorm Visualizations

Chart selection was organized by **information layer**:

- **Layer 0 (Scorecards):** KPI cards for Revenue, Profit, Profit Margin, Quantity, Total Orders with sparklines and vs. PY comparison
- **Layer 1 (1D Breakdown):** Revenue by Year/Month, Profit by Category, Revenue by Region
- **Layer 2 (2D Breakdown):** Revenue Trend by Category + Region, Revenue YoY% by Sub-Category, Top 15 Locations table with sparklines

### 4️⃣ Prototype & Review

Multiple drafts (5 iterations) were created and evaluated across these criteria:
- Information quality
- Chart type effectiveness
- Layout and visual hierarchy
- Color consistency
- Axis labels and annotations

The final version uses a dark theme with gold/teal highlights for high contrast and executive-level readability.

---

## 📊 Key Insights & Visualizations

### 🔍 Dashboard Preview

#### 1️⃣ Overview Page

![Overview Dashboard](screenshots/overview.png)

📌 **Analysis:**

- **Observation:** Total Revenue reached **$19,690M** with **+52.13% growth vs. Prior Year**. Profit grew to **$2,645M (+54.55% vs. PY)** with a stable Profit Margin of **13%**. Revenue showed consistent upward trajectory from 2011 to 2014, with **Q4 (months 10–11)** showing the highest monthly revenue peaks (+90.83%, +51.00% vs. PY).
  
- **Observation:** The Central region leads all markets at **$5,350M** in revenue, followed by South at **$2,988M**. The weakest markets (EMEA, Africa, Canada) combined represent less than 4% of total revenue.

- **Recommendation:** Capitalize on Q4 momentum with targeted promotions. Investigate seasonal demand drivers in peak months. Consider reallocating marketing spend from underperforming markets (EMEA/Africa) toward high-growth regions.

---

#### 2️⃣ Market Page

![Market Dashboard](screenshots/market.png)

📌 **Analysis:**

- **Observation:** The **Central region dominates** with $6,692M revenue and a 13–14% profit margin, consistent across all regions. The **Consumer segment** represents the largest share of the Revenue Decomposition ($10,060M), followed by Corporate ($6,197M) and Home Office ($3,433M).

- **Observation:** Among the **Top 15 Locations**, California leads with **$526,723K** in revenue. The EU and APAC markets show competitive clustering in the Revenue vs. Profit Margin scatter chart, indicating healthy profitability at scale.

- **Observation:** Return rate and revenue trend data (Central and South regions shown) indicate that the highest-revenue markets also maintain stable growth trajectories — suggesting the growth is sustainable, not spiky.

- **Recommendation:** Double down on the Central and South regions for near-term growth. Investigate the Corporate segment in underperforming regions as a potential untapped opportunity.

---

#### 3️⃣ Product Page

![Product Dashboard](screenshots/product.png)

📌 **Analysis:**

- **Observation:** **Chairs** is the top sub-category by revenue ($488,294K) with a 51.73% YoY growth. **Phones** ($380,181K) and **Storage** ($407,333K) also show strong YoY growth at 51.85% and 56.50% respectively. By contrast, **Tables** show negative profit (-$6,268K), making it the only loss-making sub-category.

- **Observation:** In the **bubble chart** (Total Orders vs. Total Profit), the largest bubbles cluster around the 2K–4K order range with $200M–$350M profit — indicating that the sweet spot for profitability is mid-volume, high-margin products, not necessarily the highest-order-count categories.

- **Observation:** **Novimex Executive Leather Armchair** leads product-level revenue with an extraordinary **+180.54% YoY growth**. Samsung and Nokia Smart Phones also perform strongly at top-line revenue.

- **Recommendation:** Discontinue or reprice the **Tables** sub-category to eliminate the loss. Increase investment in the top-performing product lines (Chairs, Phones, Storage). Monitor high-return-rate products for quality issues.

---

#### 4️⃣ Report Page

![Report Dashboard](screenshots/report.png)

📌 **Analysis:**

- **Observation:** The report page provides **granular transaction-level data** with full details: Date, Product, Category, Region, Country, Person, Quantity, Revenue, Profit, and Profit Margin. Color-coded profit cells (green = positive, red = negative) enable instant identification of loss-making transactions.

- **Observation:** High-volume transactions (30,000+ units) for Furniture items in the Central and East regions are visible, with varying profit margins from negative (-1%) to highly positive (48%). This highlights the importance of discount management.

- **Recommendation:** Use this report page for operational audits. Flag transactions with negative profit margins for pricing or discount policy review. Cross-reference with the Market and Product pages to pinpoint systemic issues.

---

## 🔎 Final Conclusion & Recommendations

Based on the insights and findings above, we recommend the **Senior Management team** to consider the following:

✅ **Market Strategy:** Continue investing heavily in the **Central and South regions**, which together account for the majority of revenue and maintain healthy margins. Evaluate the viability of EMEA, Africa, and Canada — consider restructuring or exiting low-ROI markets.

✅ **Product Portfolio:** Prioritize **Chairs, Phones, and Storage** as core growth drivers. Urgently address the **Tables sub-category** which is the only category generating a net loss. Introduce stricter discount controls, as excessive discounting is a key driver of negative margins.

✅ **Seasonality:** Build Q4 (October–November) into the annual sales strategy as a proven peak period. Develop pre-season inventory and marketing plans to maximize this window.

✅ **Customer Segments:** The **Consumer segment** generates the largest revenue, but the **Corporate segment** may offer better margin efficiency. A deeper customer-level profitability analysis is recommended as a next step.

✅ **Operational:** Implement a regular review cadence using the Report page to identify and correct high-discount or low-margin transactions before they compound. A return rate analysis by product would also add significant value.
