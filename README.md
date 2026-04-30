# 🟡 Blinkit — Correlation Intelligence System

> A 4-page interactive analytics system built on Looker Studio, powered by a VLOOKUP-engineered Master Table derived from Blinkit's raw and cleaned grocery datasets. Designed to surface hidden correlations across operations, revenue, customer experience, and inventory risk.



---

## 📌 Table of Contents

- [Project Overview](#project-overview)
- [Repository Structure](#repository-structure)
- [Data Pipeline](#data-pipeline)
  - [Raw Dataset](#raw-dataset)
  - [Cleaned Dataset](#cleaned-dataset)
  - [Master Table](#master-table)
- [Dashboard System — 4 Pages](#dashboard-system--4-pages)
  - [Page 1 — Executive Correlation Overview](#page-1--executive-correlation-overview)
  - [Page 2 — Operations & Delivery Correlation](#page-2--operations--delivery-correlation)
  - [Page 3 — Customer Experience & Revenue Correlation](#page-3--customer-experience--revenue-correlation)
  - [Page 4 — Product Profit & Inventory Risk Correlation](#page-4--product-profit--inventory-risk-correlation)
- [Tech Stack](#tech-stack)
- [Key Insights](#key-insights)
- [Author](#author)

---

## 📖 Project Overview

The **Blinkit Correlation Intelligence System** is a multi-page analytical dashboard system that goes beyond basic reporting. Instead of just showing *what* the numbers are, this system focuses on *why* variables move together — identifying statistical correlations that drive real business decisions at Blinkit.

The project follows a complete end-to-end data analytics pipeline:

```
Raw Dataset
    ↓  (cleaning & standardization)
Cleaned Dataset
    ↓  (VLOOKUP-based merging in Excel)
Master Table
    ↓  (connected to Looker Studio)
4-Page Correlation Intelligence System
```

Built as part of the **DVA (Data Visualization & Analysis)** course at **Newton School of Technology**.

---

## 📁 Repository Structure

```
blinkit-dva--correlation-system/
│
├── RawDataset/                   # Original unprocessed Blinkit data files
│
├── CleanedDataset/               # Preprocessed and standardized dataset files
│
├── Dashboard/                    # Master Table + Looker Studio export/assets
│
└── README.md
```

---

## 🔄 Data Pipeline

### Raw Dataset

The starting point — Blinkit's original grocery sales data, containing real-world messiness:

- Missing values in `Item_Weight` and `Outlet_Size`
- Inconsistent labels in `Item_Fat_Content` (e.g. `LF`, `low fat`, `Low Fat`, `reg`, `Regular` — all meaning the same thing)
- Mixed formatting and data type inconsistencies across columns

---

### Cleaned Dataset

The raw data was processed and standardized:

- **Missing Values** — `Item_Weight` filled using per-item mean; `Outlet_Size` filled using mode per outlet type
- **Label Standardization** — `Item_Fat_Content` normalized to exactly two values: `Low Fat` and `Regular`
- **Data Type Fixing** — numeric columns cast to correct float/int types
- **Outlier Handling** — IQR-based detection applied on `Item_MRP` and `Item_Outlet_Sales`

---

### Master Table

The **Master Table** is the single source of truth that powers all 4 Looker Studio dashboards.

It was built in **Microsoft Excel** by merging the cleaned datasets using **VLOOKUP** — combining item-level attributes with outlet-level metadata into one unified, analysis-ready flat table.

**Key columns in the Master Table:**

| Column | Description |
|---|---|
| `Item_Identifier` | Unique product ID |
| `Item_Type` | Product category (Dairy, Snacks, Beverages, etc.) |
| `Item_Fat_Content` | `Low Fat` or `Regular` |
| `Item_Weight` | Product weight in kg |
| `Item_Visibility` | Percentage of shelf display area allocated |
| `Item_MRP` | Maximum Retail Price |
| `Outlet_Identifier` | Unique store ID |
| `Outlet_Type` | Grocery Store / Supermarket Type I / II / III |
| `Outlet_Size` | Small / Medium / High |
| `Outlet_Location_Type` | Tier 1 / Tier 2 / Tier 3 city |
| `Outlet_Establishment_Year` | Year the outlet was set up |
| `Item_Outlet_Sales` | Total sales amount — primary target variable |

This Master Table was directly connected to **Google Looker Studio** as the data source for all 4 dashboard pages.

---

## 📊 Dashboard System — 4 Pages

The Looker Studio report is organized as a **Correlation Intelligence System** — 4 pages, each focused on a distinct analytical perspective.

---

### Page 1 — Executive Correlation Overview

**Audience:** Business leaders, project reviewers
**Purpose:** A high-level command view of the strongest correlations across the entire dataset — the "so what" page built for decision-makers.

**Covers:**
- Overall correlation summary across all key numerical variables
- Top strongest positive and negative correlations ranked
- Sales distribution by outlet type and location tier
- KPI scorecards — Total Sales, Avg MRP, Avg Item Visibility, Outlet Count
- Which variables most strongly predict `Item_Outlet_Sales`

---

### Page 2 — Operations & Delivery Correlation

**Audience:** Operations team, supply chain analysts
**Purpose:** Understand how outlet-level operational factors correlate with sales performance.

**Covers:**
- Outlet age vs. sales — do older outlets consistently sell more?
- Outlet size vs. total revenue — does bigger footprint = better performance?
- Location tier (Tier 1/2/3) vs. average sales per item
- Outlet type performance gap — Supermarket vs. Grocery Store breakdown
- Establishment year trend — growth curve of newer vs. established outlets

---

### Page 3 — Customer Experience & Revenue Correlation

**Audience:** Marketing team, category managers
**Purpose:** Analyze how customer-facing product attributes correlate with revenue — what the shopper sees and buys.

**Covers:**
- Item visibility vs. item sales — the counterintuitive visibility paradox
- Fat content preference by outlet type — Low Fat vs. Regular revenue split
- Product category vs. average sales — which categories drive the most money
- MRP vs. sales scatter — price sensitivity and elasticity signals
- Item type × outlet type sales matrix — category performance by store format

---

### Page 4 — Product Profit & Inventory Risk Correlation

**Audience:** Category managers, inventory planners
**Purpose:** Identify which products carry high margin potential vs. high inventory risk — and how these factors correlate with each other.

**Covers:**
- MRP vs. item weight — premium pricing patterns by weight class
- Low-visibility + high-MRP items — the inventory risk zone (expensive products that aren't getting shelf exposure)
- Item type vs. MRP distribution — overpriced categories relative to actual sales
- Profitability quadrant — High MRP × High Sales vs. Low MRP × Low Sales segments
- Fat content vs. MRP — does health labeling actually impact product pricing?

---

## 🛠️ Tech Stack

| Tool | Role |
|---|---|
| **Microsoft Excel** | Data cleaning, VLOOKUP-based Master Table engineering |
| **Google Looker Studio** | 4-page correlation dashboard design and visualization |
| **GitHub** | Version control and dataset storage |

---

## 💡 Key Insights

1. **Item MRP is the strongest predictor of sales** — higher-priced items consistently drive more revenue across all outlet types.
2. **Item Visibility has a weak-to-inverse correlation with sales** — high shelf visibility is often assigned to slow-moving items, not bestsellers.
3. **Supermarket Type I dominates total sales volume** by a significant margin over other outlet formats.
4. **Tier 3 city outlets punch above their weight** — smaller market outlets show stronger per-item average sales than expected.
5. **Outlet age positively correlates with sales** — stores established before 2005 outperform newer outlets in average revenue.
6. **Fat content label matters less than category** — Low Fat dominates the catalog count but doesn't always outsell Regular items.
7. **High MRP + Low Visibility = Inventory Risk** — premium products with poor shelf placement represent the highest potential lost revenue in the system.

---

## 👤 Author

**Akhilesh Kumar**
BTech Computer Science — AI Specialization
Newton School of Technology

- GitHub: [@UserAkku](https://github.com/UserAkku)

---

## 📝 License

This project is submitted for academic evaluation as part of the **DVA (Data Visualization & Analysis)** coursework at Newton School of Technology. Dataset used for educational purposes only.

---

> *"Correlation doesn't imply causation — but it tells you exactly where to look."*
