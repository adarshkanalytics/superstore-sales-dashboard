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

| # | Page | What It Answers |
|---|---|---|
| 1 | **Executive Overview** | "How is the business doing overall, right now?" |
| 2 | **Sales Analysis** | "Where is revenue coming from, and through which channels?" |
| 3 | **Profit Analysis** | "Where are we actually making money — and where are we bleeding it?" |
| 4 | **Customer Analysis** | "Who are our most valuable customers, and how is our base evolving?" |
| 5 | **Product Analysis** | "Which products should we double down on, and which should we cut?" |
| 6 | **Regional Analysis** | "Which regions and states deserve more investment?" |
| 7 | **Insights** | "What are the 5 things leadership needs to know today?" |

*(Screenshots of each page: [`/screenshots`](screenshots))*

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

### 📬 Let's Connect

*(Add your name, LinkedIn, and email here)*

⭐ If this project was useful or interesting, consider starring the repo!

</div>
