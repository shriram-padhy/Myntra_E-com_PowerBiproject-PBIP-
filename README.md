# Myntra_E-com_PowerBiproject-PBIP-

# Myntra Analytics Dashboard (Power BI Project / PBIP)

A Myntra-style e-commerce analytics dashboard built in Power BI and stored as a **Power BI Project (PBIP)** so every change to the report and data model is readable, diffable, and version-controlled.

![Dashboard preview](images/dashboard.png)

## What this project shows

- A dark-themed, multi-panel KPI dashboard designed to match a reference UI
- A star-schema data model (orders fact table + customers and brands dimensions + a date table)
- DAX measures for the KPI cards
- A custom report theme (JSON) for the dark pink/orange palette
- The report and model saved as plain-text files using the PBIP format

## Dashboard contents

| Section | Visual |
|---|---|
| KPI cards | Total sales, total orders, total customers, active brands, average rating (with sparklines) |
| Sales by category | Horizontal bar chart |
| Orders by time of day | Donut chart |
| Order channel | Donut chart (App vs Web) |
| Monthly sales trend | Line chart with area fill |
| Insights | Text callouts summarising the top category, peak ordering window, and channel split |
| Navigation | Page navigator for Overview, Sales, Order, Brand, Category, Location, and Ratings pages |
| Filters | City and category slicers |

## Data

The dataset is **synthetic**, generated with Python to mirror the shape of a fashion e-commerce business. It is not real Myntra data.

| Table | Rows | Key columns |
|---|---|---|
| `orders` | 15,200 | order_id, order_date, time_of_day, customer_id, city, category, brand_id, channel, sale_amount, rating |
| `customers` | 86,000 | customer_id, signup_date, city |
| `brands` | 3,100 | brand_id, brand_name, primary_category, is_active |

Relationships: `orders[customer_id]` → `customers[customer_id]` and `orders[brand_id]` → `brands[brand_id]` (many-to-one).

## Key measures

```DAX
Total Sales = SUM(orders[sale_amount])
Total Orders = COUNTROWS(orders)
Total Customers = DISTINCTCOUNT(customers[customer_id])
Active Brands = CALCULATE(COUNTROWS(brands), brands[is_active] = TRUE)
Avg Rating = AVERAGE(orders[rating])
```

## Repository structure

```
Myntra_dashboard.pbip          Project entry point (open this in Power BI Desktop)
Myntra_dashboard.Report/       Report pages and visuals (JSON)
Myntra_dashboard.SemanticModel/ Data model: tables, measures, relationships
images/                        Dashboard screenshot
```

## How to open it

1. Install the latest Power BI Desktop.
2. Download or clone this repository.
3. Double-click `Myntra_dashboard.pbip`.
4. If the data sources show an error, go to **Transform data → Data source settings → Change source** and point each table to your local copy of the CSV files.

## What I learned

- How the PBIP format separates the report from the semantic model
- Why text-based project files make BI work easier to review and track
- Designing a dashboard around a reference layout, from theme to composite KPI cards

## Tools

Power BI Desktop, DAX, Python (data generation), GitHub

## Author

Shriram - [LinkedIn](https://www.linkedin.com/in/sriram-padhy-7299421b5) | [GitHub](https://github.com/shriram-padhy)
