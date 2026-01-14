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
- 📊 [Power BI Dashboard](#power-bi-dashboard)  
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
## Data Analysis (SQL)

CREATE OR REPLACE VIEW retail.table_joined AS
SELECT
    s.date,
    DAYNAME(s.date) AS day_of_week,
    
    CASE 
        WHEN WEEKDAY(s.date) IN (5, 6) THEN 'Weekend'
        ELSE 'Weekday'
    END AS is_weekend,

    s.shop_id,
    s.shop_name,
    s.customers,
    s.sales_usd,

    -- Prevent division by zero
    CASE 
        WHEN s.customers > 0 THEN s.sales_usd / s.customers
        ELSE 0
    END AS sales_per_customer,

    su.pct_male,
    su.pct_female,
    su.pct_family,
    su.pct_single,

    w.avg_temp_f,
    w.precip_in,
    w.is_rain,
    w.humidity_pct

FROM retail.sales s
LEFT JOIN retail.survey su
    USING (date)
LEFT JOIN retail.weather w
    USING (date);

