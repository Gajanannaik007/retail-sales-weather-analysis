# 📈 Retail Sales & Weather Impact Analysis

Analyzing the impact of **weather conditions on retail sales** using **MySQL** and **Power BI** to uncover trends, drivers, and actionable insights.

---

## 🧾 Table of Contents

- 📘 [Project Overview](#project-overview)  
- 🎯 [Objectives](#objectives)  
- 📁 [Dataset](#dataset)  
- 🛠️ [Tools & Technologies](#tools--technologies)  
- 🗂️ [Folder Structure](#folder-structure)  
- 📊 [Data Analysis (SQL)](#data-analysis-sql)  
- 📊 [Power BI Dashboard Overview](#power-bi-dashboard)  
- 🧠 [Key Insights](#key-insights)  
- 📦 [How to Run](#how-to-run)  
- 📚 [References](#references)

---

## 📘 Project Overview

This project analyzes retail sales data along with weather information to determine how different weather conditions affect sales performance. Insights are generated using SQL queries and visualized through an interactive Power BI dashboard.

---

## 🎯 Objectives

- Understand patterns in sales over time  
- Analyze how weather (temperature, rainfall) affects purchasing  
- Discover trends for strategic business decisions  
- Build an interactive dashboard for visual storytelling

---

## 📁 Dataset

The dataset consists of:
- **Retail Sales Data** — transaction records with products, dates, sales
- **Weather Data** — temperature, precipitation, humidity recorded by date

📁 Location: `dataset/`

---

## 🛠️ Tools & Technologies

- 🐬 **MySQL** – Structured Query Language for data analysis  
- 📊 **Power BI** – Dashboard creation & visualization  
- 🧮 **MS Excel** – Data review and cleaning  
- 🐙 **GitHub** – Project hosting

---

## 🗂️ Folder Structure

# retail-sales-weather-analysis

```text
retail-sales-weather-analysis
├── dataset/
│   ├── retail_sales.csv
│   ├── weather_data.csv
│   └── README.md
│
├── sql_queries/
│   ├── data_cleaning.sql
│   ├── exploratory_analysis.sql
│   ├── weather_sales_join.sql
│   ├── exploratory_analysis.sql
│   └── README.md
│
├── powerbi/
│   ├── retail_sales_weather.pbix
│   └── README.md
│
├── screenshots/
│   ├── dashboard_overview.png
│   ├── sales_trends.png
│   └── README.md
│
├── docs/
│   └── project_report.md
│
└── README.md

```
```md
## 📊 Data Analysis (SQL)

```sql
 create or replace view retail.table_joined as
select
s.date,
dayname(date) as day_of_week,
case when weekday(date) in (5,6) then "weekend" else "weekday" end as is_weekend,
s.shop_id,
s.shop_name,
s.customers,
s.sales_usd,
s.sales_usd/s.customers as sales_per_customers,
su.pct_male,
su.pct_female,
su.pct_family,
su.pct_single,
w.avg_temp_f,
w.precip_in,
w.is_rain,
w.humidity_pct
From retail.sales s
left join retail.survey su
using(date)
left join retail.weather w
using (date)
```
## 📊 Power BI Dashboard Overview

- **Main KPIs:**  
  Total Sales ($5.7M) and Total Customers (333K) displayed using card visuals to highlight overall business performance.

- **Sales & Temperature Trend:**  
  Dual-axis line chart showing **Sales (USD)** and **Average Temperature (°F)** over time to analyze seasonal and weather impact on sales.

- **Location Performance:**  
  Bar chart displaying **Average Sales by Shop Location** (Miami Beach, Orlando, Tampa, Jacksonville) to identify top-performing stores.

- **Customer Demographics – Gender:**  
  Donut chart representing **Male vs Female customer distribution** for demographic insights.

- **Customer Demographics – Type:**  
  Donut chart comparing **Single vs Family customers**, highlighting customer composition.

- **Filters & Slicers:**  
  Interactive slicers for **Rain Condition** and **Date Range** to dynamically analyze sales under different weather and time scenarios.

- **Weather Impact Analysis:**  
  Visual correlation between rainfall, temperature, and sales trends to support weather-driven business decisions.

- **Interactive Design:**  
  Fully interactive visuals enabling drill-downs and dynamic filtering for deeper analysis.






