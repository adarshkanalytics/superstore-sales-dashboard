<div align="center">

# 📊 Superstore Sales Dashboard
### Executive Business Intelligence Report | Power BI

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-15%2B%20Measures-2E5FA3?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-0E8C7F?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-6B7686?style=for-the-badge)

A 7-page executive dashboard transforming 9,994 raw retail transactions into actionable, decision-ready insights — built end-to-end in Power BI.

[View Dashboard Pages](#-dashboard-pages) • [Key Insights](#-key-business-insights) • [DAX Measures](docs/DAX-measures.md) • [Data Model](#%EF%B8%8F-data-model)

</div>

---

## 📌 Overview

Superstore's leadership had no real-time visibility into which regions, product categories, and customer segments were driving profit versus which were causing losses — decisions were being made on instinct rather than data.

This project delivers a single, interactive source of truth: a 7-page Power BI report covering sales performance, profitability, customer behavior, product health, and regional trends, backed by a proper star-schema data model and 15+ custom DAX measures.

## 🎯 Business Objectives

- Track sales and profit trends over time
- Identify top and underperforming regions, states, and categories
- Flag loss-making products and sub-categories before they become a bigger problem
- Understand customer value and behavior patterns
- Give leadership a single, fast, executive-level view for decision-making

---

## 🗂️ Dashboard Pages

This report consists of **7 interconnected dashboard pages**, each built to answer a key business question through interactive visualizations and KPIs.

| # | Dashboard | Primary Business Objective |
|---|-----------|----------------------------|
| 1 | 📊 Executive Overview | Monitor overall business performance through executive-level KPIs. |
| 2 | 💰 Sales Analysis | Analyze sales trends across products, categories, and customer segments. |
| 3 | 📈 Profit Analysis | Evaluate profitability and identify high- and low-performing areas. |
| 4 | 👥 Customer Analysis | Understand customer behavior, value, and purchasing trends. |
| 5 | 📦 Product Analysis | Measure product performance and identify growth opportunities. |
| 6 | 🌍 Regional Analysis | Compare sales and profit performance across regions and states. |
| 7 | 💡 Business Insights | Summarize key findings and provide actionable business recommendations. |

> 📷 **Dashboard Screenshots:** Browse all report pages in the [`screenshots/`](screenshots) directory.

---

## 📈 Key Business Insights

- 🏆 **California** is the top-performing state, contributing **19.9%** of total revenue
- 💻 **Technology** is the highest-selling and highest-profit category ($836.15K sales / $145.45K profit)
- 📱 **Phones** is the best-selling sub-category ($330.01K)
- 🖨️ **Copiers** delivers the strongest profit margin (**37.13%**) among all sub-categories
- 🌎 **West** region leads in both sales ($725.46K) and profit ($108.42K)
- 📅 Sales show a consistent seasonal peak in **November and December**
- ⚠️ Overall profit margin declined **2.35% year-over-year** despite sales growth — flagged for leadership review

---

## 🧮 Sample DAX Measures

```dax
Profit Margin % = DIVIDE([Total Profit], [Total Sales])

Sub-Category Rank = 
RANKX(ALLSELECTED('Sample - Superstore 2'[Sub-Category]), [Total Profit], , DESC, DENSE)

Top Region = 
CALCULATE(
    SELECTEDVALUE('Sample - Superstore 2'[Region]),
    TOPN(1, VALUES('Sample - Superstore 2'[Region]), [Total Sales], DESC)
)
```

📄 **Full documentation of all 15+ measures, with explanations of the business logic behind each one, is available in [`docs/DAX-measures.md`](docs/DAX-measures.md).**

---

## 🗃️ Data Model

- **Star schema** design: a single fact table (`Sample - Superstore 2`) joined to a dedicated **Date dimension table** (Year, Quarter, Month, Day)
- The Date table is explicitly marked as a Date Table, enabling accurate time-intelligence calculations (`SAMEPERIODLASTYEAR`, YoY growth) that a raw date column cannot support
- Calculated columns (`Discount Range`, `DayName`, `DayNumber`) support clean, business-readable groupings and correct chronological sorting

---

## 🛠️ Tools & Skills Demonstrated

| Category | Details |
|---|---|
| **Data Modeling** | Star schema, relationships, dedicated Date table |
| **DAX** | Time intelligence, RANKX, TOPN, SWITCH, calculated columns |
| **Report Design** | Custom navigation, multi-page architecture, KPI-driven UX |
| **Data Cleaning** | Power Query transformations on the raw Superstore dataset |
| **Business Analysis** | Translating raw data into stakeholder-ready insights |

---

## 📁 Repository Structure

```
superstore-sales-dashboard/
├── README.md
├── LICENSE
├── Superstore_Sales_Dashboard.pbix
├── Sample_-_Superstore_2.xlsx
├── screenshots/
│   └── (one image per dashboard page)
└── docs/
    └── DAX-measures.md
```

---

## 🚀 How to Explore

1. Download `Superstore_Sales_Dashboard.pbix`
2. Open in [Power BI Desktop](https://www.microsoft.com/en-us/power-platform/products/power-bi/downloads) (free)
3. Use the navigation bar at the bottom of each page to move between the 7 report views
4. Filters on the left (Region, Category, Segment, Ship Mode, Order Date) apply across all visuals on a page

---

<div align="center">

## 📫 Let's Connect

**Adarsh Kumar**  
📧 adarsh.kumar.job@gmail.com  
💼 [LinkedIn Profile](https://www.linkedin.com/in/adarshkumar2005/)

⭐ Feel free to connect with me for opportunities, collaborations, or feedback.

</div>
