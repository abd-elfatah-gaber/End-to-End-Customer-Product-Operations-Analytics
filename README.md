# 📊 ProAnalytix — Sales & Operations Intelligence Dashboard

<div align="center">

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Measures-6366F1?style=for-the-badge)
![Data Model](https://img.shields.io/badge/Schema-Snowflake-0EA5E9?style=for-the-badge)
![Pages](https://img.shields.io/badge/Dashboard%20Pages-8-22C55E?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-16a34a?style=for-the-badge)

<br/>

> **A fully interactive, multi-page Power BI report delivering end-to-end business intelligence across Sales, Products, Customers, Production, Returns, and Territories.**

</div>

---

## 🗂️ Table of Contents

- [Project Overview](#-project-overview)
- [Dashboard Pages](#-dashboard-pages)
- [Data Model](#-data-model)
- [DAX Measures](#-dax-measures)
- [Key KPIs at a Glance](#-key-kpis-at-a-glance)
- [Tools & Technologies](#-tools--technologies)
- [Project Structure](#-project-structure)
- [How to Use](#-how-to-use)

---

## 🎯 Project Overview

**ProAnalytix** is a comprehensive business intelligence solution built entirely in **Power BI Desktop**. It transforms raw operational data into actionable insights across 8 interactive report pages, giving decision-makers a 360° view of the business.

| Feature | Details |
|---|---|
| 📁 File | `Final_Project.pbix` |
| 📄 Pages | 8 Report Pages |
| 🗃️ Schema | Snowflake Schema |
| 📐 Measures | 6 Organized Folders |
| 🎨 Theme | Green & Teal Corporate |
| 🧭 Navigation | Button-based sidebar + Drillthroughs |

---

## 📑 Dashboard Pages

### 1️⃣ Sales Report
> *Core revenue performance at a glance*

| KPI | Value |
|---|---|
| 💰 Total Sales | **$25M** |
| 🧾 Net Sales | **$24M** |
| 📦 Total Order Quantity | **84.17K** |
| 📈 Total Gross Profit | **$10M** |
| 💹 Net Profit Margin | **40.14%** |

**Visuals include:** Sales by Quarter (donut) · Sales by Country (donut) · Trend by Year (line chart) · Category & Subcategory decomposition tree · Gauge chart for Total Sales Amount.

---

### 2️⃣ Products Report
> *Product performance, ranking, and inventory health*

| KPI | Value |
|---|---|
| ✅ Sold Products | **130** |
| ❌ Unsold Products | **163** |
| 📦 Total Products | **293** |
| 🎨 Product Colors | **10** |
| 📏 Product Sizes | **19** |

**Visuals include:** Top 5 by Profit · Top 5 by Sales · Product detail table with Ranking by Sales & Profit.

---

### 3️⃣ Customers Report
> *Customer demographics and purchasing behaviour*

| KPI | Value |
|---|---|
| 👥 Total Customers | **18.15K** |
| 💍 Married | **9,817** |
| 💔 Single | **8,331** |
| 👨 Male | **9,126** |
| 👩 Female | **8,892** |

**Visuals include:** Sales by Marital Status · Education Level breakdown · Sales by Gender · Top 10 Customers by Sales bar chart.

---

### 4️⃣ Production Report
> *Factory performance, machine efficiency, and downtime analysis*

| KPI | Value |
|---|---|
| ⚙️ Total Actual Qty | **100M** |
| 🎯 Total Target Qty | **125M** |
| ⏱️ Total Operating Hours | **2,092** |
| 🔴 Total Downtime Hours | **395** |
| 🟢 Net Operating Hours | **1,697** |

**Visuals include:** Gauge (Actual vs Target) · Downtime by Machine · Qty by Machine Name · Downtime by Reason (Material Shortage, Feeding Station, Blow Head, etc.).

---

### 5️⃣ Returns Report
> *Return patterns, reasons, and financial impact*

| KPI | Value |
|---|---|
| 📦 Total Returned Qty | **1,828** |
| 💸 Total Returned Value | **$765K** |
| 📉 Return Rate | **2.17%** |
| 💰 AVG Returned Value | **$423** |

**Visuals include:** Returns by Gender · Returns by Marital Status · Top 10 Products by Returns · Return Rate by Quarter (line chart) · Return Reason breakdown.

---

### 6️⃣ Territories Report
> *Geographic distribution of sales and returns*

**Visuals include:** Treemap of Returns by Region · Order Qty by Country (bar) · Sales by Region · Returned Products by Location table with Continent / Country / Region drill-down.

---

### 7️⃣ Product Drillthrough
> *Deep-dive into any product from the Products page*

**Visuals include:** Category & Subcategory by Sales (treemap) · Product Style by Sales · Product Size by Sales · Product Color by Sales · Filtered detail table.

---

### 8️⃣ Sales Drillthrough
> *Time-intelligence deep-dive for sales metrics*

| KPI | Value |
|---|---|
| 🏭 Total COGS | **14.46M** |
| 📦 Net Quantity | **82.35K** |
| 💲 AVG Selling Price | **295.99** |
| 💵 AVG Sales Amount | **444.54** |

**Visuals include:** Gross Profit by Category · Gross Profit by Quarter · Gross Profit by Country · YTD / QTD / MTD table with Sales Last Year & Previous Month comparison.

---

## 🗃️ Data Model

The project uses a **Snowflake Schema** — an extension of the star schema with normalized dimension tables.

```
                    ┌─────────────┐
                    │  Calendar   │  ← Date dimension
                    └──────┬──────┘
                           │ 1
         ┌─────────────────▼─────────────────┐
         │              Sales                │  ← Fact Table
         │  (CustomerKey, ProductKey,        │
         │   TerritoryKey, OrderDate)        │
         └──┬──────────┬──────────┬──────────┘
            │ *        │ *        │ *
     1 ┌────┘    1 ┌───┘     1 ┌──┘
┌─────▼──────┐  ┌──▼────────┐  ┌▼───────────┐
│  Customers │  │ Products  │  │ Territories│
└────────────┘  └─────┬─────┘  └────────────┘
                      │ *
                 1 ┌──┘
          ┌────────▼──────────┐
          │ Product_Subcateg. │
          └────────┬──────────┘
                   │ *
              1 ┌──┘
       ┌────────▼──────────┐
       │ Product_Categories│
       └───────────────────┘

Additional tables:
• Complaints_Returns  → linked to Products & Territories
• Production_Lots     → linked to Products, Machines_List, Calendar
• Machines_List       → linked to Production_Lots
• Downtimes           → linked to Calendar
```

### Tables Summary

| Table | Type | Description |
|---|---|---|
| `Sales` | ⭐ Fact | Core transactional data |
| `Calendar` | 📅 Dimension | Date intelligence |
| `Customers` | 👥 Dimension | Customer demographics |
| `Products` | 📦 Dimension | Product catalogue |
| `Product_Subcategories` | 📂 Dimension | Normalized subcategory |
| `Product_Categories` | 📂 Dimension | Normalized category |
| `Territories` | 🌍 Dimension | Geographic hierarchy |
| `Complaints_Returns` | 📋 Fact | Returns & complaints |
| `Production_Lots` | 🏭 Fact | Production runs |
| `Machines_List` | ⚙️ Dimension | Machine metadata |
| `Downtimes` | 🔴 Fact | Machine downtime events |
| `_Measures 1` | 📐 Measures | All DAX measures (no rows) |
| `Top N Selector` | 🎛️ Parameter | Dynamic top-N slicer |
| `Bottom N Selector` | 🎛️ Parameter | Dynamic bottom-N slicer |

---

## 📐 DAX Measures

All measures are stored in the dedicated `_Measures 1` table, organized into **6 folders**:

```
📁 _Measures 1
├── 📂 Customers
│   ├── #Customers
│   ├── #Female Customers
│   ├── #Male Customers
│   ├── #Married Customers
│   ├── #Returned Products
│   └── #Single Customers
│
├── 📂 Production KPIs
│   ├── Lot Total Operating Hours
│   └── Net Operating Hours
│
├── 📂 Ranking
│   ├── Bottom N Products by Profit
│   └── Bottom N Products by Sales
│
├── 📂 Returns
│   ├── Avg Returned Quantity
│   └── Avg Returned Value
│
├── 📂 Sales KPIs
│   ├── Avg Sales Amount
│   ├── Avg Selling Price
│   ├── Cumulative Sales
│   ├── Net Profit Margin
│   ├── Net Quantity
│   ├── Net Sales
│   ├── Number of Customers
│   ├── Number of Products
│   └── #Sold products / #Unsold products
│
└── 📂 Time Intelligence Functions
    ├── Sales Last Year
    ├── Sales Previous Month
    ├── Total MTD
    ├── Total QTD
    └── Total YTD
```

---

## 📊 Key KPIs at a Glance

```
┌─────────────────────────────────────────────────────────┐
│                  BUSINESS SUMMARY                       │
├─────────────────┬───────────────────────────────────────┤
│  💰 Total Sales │  $25,000,000                          │
│  🧾 Net Sales   │  $24,000,000                          │
│  📦 Orders      │  84,170 units                         │
│  📈 Gross Profit│  $10,000,000  (40.14% margin)         │
│  👥 Customers   │  18,150                               │
│  📦 Products    │  293 (130 sold · 163 unsold)          │
│  🔄 Returns     │  1,828 units  ($765K value)           │
│  🏭 Actual Prod │  100M units  (vs 125M target)         │
└─────────────────┴───────────────────────────────────────┘
```

**Top Country by Sales:** 🇺🇸 United States (31.86%)  
**Top Product Category:** 🚲 Bikes ($23.6M)  
**Top Quarter by Sales:** Q2 (34.84%)  
**Peak Sales Year:** 2015 → 2016 → 2017 (trending analysis)

---

## 🛠️ Tools & Technologies

| Tool | Usage |
|---|---|
| ![Power BI](https://img.shields.io/badge/-Power%20BI-F2C811?logo=powerbi&logoColor=black&style=flat-square) | Report building, visualizations, publishing |
| ![DAX](https://img.shields.io/badge/-DAX-6366F1?style=flat-square) | KPIs, time intelligence, ranking measures |
| ![Power Query](https://img.shields.io/badge/-Power%20Query-0EA5E9?style=flat-square) | Data transformation and shaping |
| ![Snowflake Schema](https://img.shields.io/badge/-Snowflake%20Schema-64748b?style=flat-square) | Normalized relational data model |

---

## 📁 Project Structure

```
📦 Final-Project-PowerBI/
├── 📊 Final_Project.pbix          ← Main Power BI report file
├── 📸 screenshots/
│   ├── 01_Sales_Dashboard.png
│   ├── 02_Products_Report.png
│   ├── 03_Product_Drillthrough.png
│   ├── 04_Customers_Report.png
│   ├── 05_Production_Report.png
│   ├── 06_Returns_Report.png
│   ├── 07_Territories_Report.png
│   ├── 08_Sales_Drillthrough.png
│   └── 09_Data_Model_Snowflake.png
└── 📄 README.md
```

---

## 🚀 How to Use

1. **Clone** this repository or download the `.pbix` file
2. Open `Final_Project.pbix` in **Power BI Desktop** (version 2023 or later recommended)
3. Use the **left sidebar** to navigate between report pages
4. Use the **slicers** (Month Name · Quarter · Year) at the top to filter data
5. Right-click any product on the Products page and select **Drillthrough → Product Drillthrough** for a detailed product view
6. Click the **back arrow ←** on drillthrough pages to return

---

## 👤 About the Author

**Abd Elfatah Gaber**  
Data Analysis Student · ITI (Information Technology Institute) · Egypt 🇪🇬

[![GitHub](https://img.shields.io/badge/GitHub-abd--elfatah--gaber-181717?style=for-the-badge&logo=github)](https://github.com/abd-elfatah-gaber)
[![Mostaql](https://img.shields.io/badge/Mostaql-Abdelfatah26-1abc9c?style=for-the-badge)](https://mostaql.com/u/Abdelfatah26)
[![Khamsat](https://img.shields.io/badge/Khamsat-abd__elfatah__gaber26-e67e22?style=for-the-badge)](https://khamsat.com/user/abd_elfatah_gaber26)

---

<div align="center">

⭐ **If you found this project useful, please consider giving it a star!** ⭐

*Built with ❤️ using Power BI — ITI Diploma Final Project*

</div>
