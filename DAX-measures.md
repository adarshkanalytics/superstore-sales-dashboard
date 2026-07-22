# DAX Measures Documentation

This document lists all custom DAX measures and calculated columns used in the Superstore Sales Dashboard, with explanations of their business logic.

---

## Core KPI Measures

```dax
Total Sales = SUM('Sample - Superstore 2'[Sales])
```
Sum of all sales transactions. The foundational revenue metric used across every page.

```dax
Total Profit = SUM('Sample - Superstore 2'[Profit])
```
Sum of all profit values. Used alongside Total Sales to evaluate business health beyond top-line revenue.

```dax
Profit Margin % = DIVIDE([Total Profit], [Total Sales])
```
Profit as a percentage of sales. `DIVIDE()` is used instead of `/` to safely handle divide-by-zero cases.

```dax
Total Orders = DISTINCTCOUNT('Sample - Superstore 2'[Order ID])
```
Counts unique orders. A plain `COUNT` would over-count since each order can span multiple line items (rows).

```dax
Total Customers = DISTINCTCOUNT('Sample - Superstore 2'[Customer ID])
```
Counts unique customers, avoiding duplicate counting when a customer has multiple orders.

```dax
Avg Order Value = DIVIDE([Total Sales], [Total Orders])
```
Average revenue per order — a key indicator of customer spending behavior.

```dax
Total Quantity = SUM('Sample - Superstore 2'[Quantity])
```
Total units sold across all transactions.

```dax
Avg Discount = AVERAGE('Sample - Superstore 2'[Discount])
```
Average discount rate applied across transactions.

---

## Time Intelligence Measures

```dax
Sales PY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))
```
Total Sales for the same period, one year prior. Requires a dedicated Date table marked as a date table for accurate results.

```dax
YoY Growth % = DIVIDE([Total Sales] - [Sales PY], [Sales PY])
```
Year-over-year growth rate, comparing current period sales to the prior year.

---

## Ranking & Top-N Logic

```dax
Sub-Category Rank = 
RANKX(
    ALLSELECTED('Sample - Superstore 2'[Sub-Category]),
    [Total Profit],
    ,
    DESC,
    DENSE
)
```
Ranks each sub-category by profitability (highest = rank 1). `ALLSELECTED` respects active filters (e.g., region, date range) while still ranking across all sub-categories rather than just the visible rows. `DENSE` avoids gaps in ranking when values tie.

```dax
Top Region = 
CALCULATE(
    SELECTEDVALUE('Sample - Superstore 2'[Region]),
    TOPN(1, VALUES('Sample - Superstore 2'[Region]), [Total Sales], DESC)
)
```
Dynamically returns the name of the top-performing region by sales. Used as a headline KPI card on the Regional Analysis page.

---

## Product Health Measures

```dax
Total Products = DISTINCTCOUNT('Sample - Superstore 2'[Product ID])
```
Count of unique products in the catalog.

```dax
Profitable Products = 
CALCULATE(
    DISTINCTCOUNT('Sample - Superstore 2'[Product ID]),
    FILTER(
        VALUES('Sample - Superstore 2'[Product ID]),
        CALCULATE([Total Profit]) > 0
    )
)
```
Counts products whose cumulative profit is positive — identifies healthy inventory.

```dax
Loss Making Products = [Total Products] - [Profitable Products]
```
Products operating at a net loss — flagged for review.

---

## Calculated Columns

```dax
Discount Range = 
SWITCH(
    TRUE(),
    'Sample - Superstore 2'[Discount] = 0, "0-10%",
    'Sample - Superstore 2'[Discount] <= 0.2, "10-20%",
    'Sample - Superstore 2'[Discount] <= 0.3, "20-30%",
    'Sample - Superstore 2'[Discount] <= 0.4, "30-40%",
    "40%+"
)
```
Buckets individual discount rates into readable ranges for the Profit by Discount Range visual.

```dax
DayName = FORMAT('Date'[Date], "dddd")
```
Extracts the day-of-week name from the Date table.

```dax
DayNumber = WEEKDAY('Date'[Date], 2)
```
Numeric day-of-week (Monday = 1 ... Sunday = 7), used purely to sort `DayName` chronologically instead of alphabetically via "Sort by column."

---

## Data Modeling Notes

- The model follows a **star schema**: a single fact table (`Sample - Superstore 2`) joined to a dedicated `Date` dimension table on Order Date.
- The Date table is explicitly marked as a **Date Table** in Power BI, which is required for `SAMEPERIODLASTYEAR` and other time-intelligence functions to work correctly.
- `ALLSELECTED` is used (rather than `ALL`) in ranking measures so that rankings respond correctly to report-level filters (region, category, date range) without being restricted only to what's currently visible in a Top-N filtered visual.
