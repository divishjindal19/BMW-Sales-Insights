# 🚗 BMW Sales Insights Dashboard (Power BI)

An interactive **Power BI dashboard** designed to analyze **BMW global sales performance, revenue trends, product popularity, and regional demand**.  
This project demonstrates how **Business Intelligence tools can transform raw sales data into actionable insights** using interactive visuals, data modeling, and DAX calculations.

The dashboard allows users to explore sales data by **model, country, sales channel, and time period**.

---

# 📊 Dashboard Overview

The dashboard provides insights into:

- Global sales performance
- Top selling BMW models
- Revenue growth trends
- Country-wise performance
- Sales channel contribution
- Detailed model insights

Users can dynamically filter data using **Year, Month, and Weekday slicers**.

---

# 🖼 Dashboard Screenshots

## Main Sales Dashboard
![Dashboard](./assets/dashboard_overview.png)

Shows:

- Global sales trend
- Top selling models
- Country performance
- Revenue comparison with previous year
- Channel-wise sales

---

## Model Insights Page
![Model Insights](./assets/model_insights.png)

Displays:

- Selected BMW model image
- Units sold per country
- Average price by region
- Model level performance

---

# 🎯 Project Objective

The purpose of this project is to build a **real-world Business Intelligence dashboard** similar to what automotive companies use for:

- Sales monitoring
- Market performance analysis
- Product demand analysis
- Revenue trend tracking
- Strategic decision making

---

# 🗂 Dataset Description

The dataset simulates **BMW vehicle sales across multiple countries and channels**.

### Data Includes

- Car models
- Country sales
- Sales channels
- Sales quantities
- Unit prices
- Time dimension

---

# 🧩 Data Model

The project follows a **Star Schema** data model for better performance and scalability.

## Fact Table

### `factTable`

| Column | Description |
|------|-------------|
| Date | Transaction date |
| dimChannelChannelID | Sales channel reference |
| dimCountryCountryID | Country reference |
| dimModelModelID | Car model reference |
| Quantity Sold | Number of vehicles sold |
| Unit Price | Price per unit |
| Total | Total revenue |

---

## Dimension Tables

### `dimModel`

| Column | Description |
|------|-------------|
| ModelID | Unique model ID |
| Model | BMW model name |
| Car Images Column2 | Model image reference |

---

### `dimCountry`

| Column | Description |
|------|-------------|
| CountryID | Country ID |
| Country | Country name |
| Flag | Country flag |
| Region | Sales region |

---

### `dimChannel`

| Column | Description |
|------|-------------|
| ChannelID | Channel ID |
| Channel | Sales channel |

Example channels:

- Dealership
- Wholesale
- Online

---

### `Calendar`

| Column | Description |
|------|-------------|
| Date | Full date |
| Month | Month name |
| Monthnum | Month number |
| Qtr | Quarter |
| Weekday | Day of week |

---

# 📊 Key Dashboard Visualizations

### 📈 Global Sales Trend
Shows yearly revenue comparison with **previous year performance**.

---

### 🚘 Top Selling Models
Displays BMW models ranked by **total units sold**.

Example models:

- BMW Z4
- BMW X7
- BMW X6
- BMW X5
- BMW X4

---

### 🌍 Country Sales Table
Shows:

- Country flag
- Units sold
- Revenue
- Percentage change
- Revenue sparkline trend

---

### 🧭 Sales by Channel
Donut chart showing sales distribution between:

- Online
- Dealership
- Wholesale

---

### 📊 Quantity Sold by Year
Bar chart comparing yearly sales.

---

# 🧮 DAX Measures

The project uses multiple **DAX calculations** to derive insights.

---

## ALL MEASURES

```DAX
Revenue =
SUMX(
    factTable,
    factTable[Quantity Sold] * factTable[Unit Price]
)


Units =
SUM(factTable[Quantity Sold])

Revenue PY =
CALCULATE(
    [Revenue],
    SAMEPERIODLASTYEAR(Calendar[Date])
)

Revenue Variance =
[Revenue] - [Revenue PY]

Revenue Growth =
DIVIDE([Revenue Variance], [Revenue PY])

Qty Sold PY =
CALCULATE(
    [Units],
    SAMEPERIODLASTYEAR(Calendar[Date])
)

Qty Sold Variance =
[Units] - [Qty Sold PY]
