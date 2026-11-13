# 🛠️ ETL & Reporting Pipeline — E-Commerce SAMALARIS

**Project Status:** Completed  
**Tools:** Python (Pandas) | PostgreSQL | SQL | Power BI

---

## 📌 Executive Summary

This project builds an **end-to-end ETL pipeline** to transform SAMALARIS e-commerce transaction data from separate CSV files per table into a clean, structured database in PostgreSQL as a **Single Source of Truth** for reporting.

Each CSV file was cleaned separately according to its own table structure, then loaded into PostgreSQL. The clean data was then visualized in Power BI for sales performance monitoring.

As an example use case, the dashboard is used to monitor sales performance and return rate in Q3 2026.

---

## 🎯 Business Problem & Objectives

In Q3 2026, SAMALARIS transaction data was still stored as separate CSV files per table (`dim_customers`, `dim_products`, `order`, `shipping_details`) and was not yet centralized in a database, making it difficult to use for consistent reporting.

**Main Objectives:**
- **Extract:** Read each CSV file according to its respective table.
- **Transform:** Clean duplicates, standardize formats / naming, handle missing values, and validate data quality using Python (Pandas) per table, while preserving the original table structure.
- **Load:** Load each cleaned table into PostgreSQL (DBMS) as a centralized database.
- **Visualize:** Build an interactive dashboard in Power BI on top of PostgreSQL.

---

## 📊 Dataset Overview

- **Data Source:** SAMALARIS Internal Transaction Data (Q1 - Q3 2026)
- **Source Files:**
    - `dim_customers.csv` -> table `dim_customers`
    - `dim_products.csv` -> table `dim_products`
    - `order.csv` -> table `order`
    - `shipping_details.csv` -> table `shipping_details`
- **Q3 2026 Coverage:**
    - Total Orders (Q3): 1,487 Transactions
    - Total Returns (Q3): 829 Transactions (Return Rate: 55.75%)
    - Main Product Categories: Fashion, Home Appliances, Sports, Beauty, Electronics
    - Payment Methods: COD, Bank Transfer, E-Wallet, Credit Card

> Note: Files were already separated per table. No merging / joining was performed during ETL. Table structure was preserved.

---
## 🔄 ETL Pipeline Architecture

CSV Files (Already Separated Per Table)
    - dim_customers.csv -> table dim_customers
    - dim_products.csv -> table dim_products
    - order.csv -> table order
    - shipping_details.csv -> table shipping_details
        ↓ EXTRACT (Per File / Per Table)
Python (Pandas)
    - Cleaned duplicates
    - Standardized formats / naming
    - Handled missing values
    - Validated data quality
    - Table structure preserved, no joining
        ↓ LOAD (Per Table)
PostgreSQL (DBMS)
    - 4 clean & structured tables
    - Centralized database
    - Single Source of Truth
        ↓ VISUALIZE
Power BI Dashboard
    - Connected directly to PostgreSQL
    - Table relationships managed in Power BI
    
---

## ✅ Data Quality Checks

Before loading data into PostgreSQL, validation was performed:
- Duplicates removed
- Date formats & product naming standardized
- Missing values handled
- Data validated before loading into the database

---

## 📊 Power BI Dashboard

The dashboard was built on top of PostgreSQL to visualize key metrics and support data-driven decisions.

**Example metrics monitored:**
- Gross Revenue & Net Revenue per Quarter / Month
- Total Orders, Total Quantity, Return Rate %
- Return Reasons (Damaged in Transit, Wrong Size / Fit, etc.)
- Gross Revenue per City & Top Sales by Category

*This dashboard is the output of the pipeline above, not a separate analysis project.*

---

## 📊 Dashboard Insights — Example Use Case

The dashboard built on the clean PostgreSQL database is used to monitor Q3 2026 sales performance. Example insights obtained from the standardized data:

**1. Return by Category**
- Fashion is the largest contributor to returns with a return rate of 73.88%.
- Main root causes of returns (Pareto Distribution): Damaged in Transit (30.76%), Product Quality / Mismatch (28.83%), Wrong Size / Fit (23.88%), Delayed Delivery (16.53%).

**2. Courier & Region Performance**
- Issues were found in delivery duration and safety in regions outside Java (especially Medan & Makassar).
- Certain partner couriers showed a Damaged in Transit rate far above the operational average.

**3. COD Payment Risk**
- Transactions with Cash on Delivery (COD) payment method had the highest return vulnerability at 62.89%.
- Insight: The combination of Fashion category (size / fit issues) and COD payment method increases the tendency for buyers to reject / return goods upon courier arrival.

> Note: The insights above are an example output from the dashboard. The main focus of this project is on building the ETL pipeline and data quality that enables consistent and trustworthy reporting.

---

## ✅ What This Pipeline Enables

Because data is now clean, centralized in PostgreSQL, and serves as a Single Source of Truth, the business can:
- Monitor return rate per category, courier, and region without manual recapitulation from CSV files
- Identify root causes of returns based on validated data
- Use a Power BI dashboard directly connected to the database, so data remains consistent

---

## 🛠️ Tools & Skills Used

- **ETL Method:** Extract → Transform → Load
- **Transform:** Python (Pandas) — Data Cleansing, Standardization, Handling Missing Values, Data Validation
- **Database:** PostgreSQL (DBMS) — Centralized Database, Single Source of Truth
- **Query:** SQL — Data Validation & Extraction
- **Visualization:** Power BI — Interactive Dashboard connected to PostgreSQL

---
