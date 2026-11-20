# Self-Project ETL & Reporting Pipeline E-Commerce SAMALARIS

![Project Status](https://img.shields.io/badge/Project%20Status-Completed-brightgreen)  ![Tools](https://img.shields.io/badge/Tools-Python%20%7C%20PostgreSQL%20%7C%20Power%20BI%20-blue)

---

## A. Executive Summary

This project builds an **end-to-end ETL pipeline** to transform SAMALARIS e-commerce transaction data from separate per-table CSV files into a clean, centralized database in PostgreSQL as a **Single Source of Truth** for reporting.

Each CSV file was cleaned separately according to its table structure and loaded into PostgreSQL as individual tables (with relationships modeled in Power BI rather than pre-joining tables during ingestion). The structured data was then connected to Power BI for sales and return performance monitoring.

As an example use case, the dashboard is used to monitor sales performance and return rates in Q3 2026.

---

## B. Business Problem & Objectives

SAMALARIS transaction data (covering Q1–Q3 2026) was previously stored as separate CSV files per table (`dim_customers`, `dim_products`, `order`, `shipping_details`) rather than a centralized database, making consistent reporting and monitoring harder to maintain.

**Main Objectives:**
- **Extract:** Read each CSV file per table (`dim_customers`, `dim_products`, `order`, `shipping_details`).
- **Transform:** Clean duplicates, standardize formats and naming, handle missing values, and run data quality checks using Python (Pandas) per table while preserving the table structure.
- **Load:** Load each cleaned table into PostgreSQL as a centralized database acting as a Single Source of Truth.
- **Visualize:** Build an interactive dashboard in Power BI connected to PostgreSQL, with table relationships configured in the semantic/data model.
---

## C. Dataset Overview

- **Data Source:** SAMALARIS Internal Transaction Data (Q1 – Q3 2026)
- **Source Files & Target Tables:**
    - `dim_customers.csv` -> `dim_customers`
    - `dim_products.csv` -> `dim_products`
    - `order.csv` -> `order` *(note: `order` is a reserved keyword in SQL, so quote as `"order"` when querying in PostgreSQL)*
    - `shipping_details.csv` -> `shipping_details`
- **Q3 2026 Highlight Metrics:**
    - Total Orders (Q3): 1,487 Transactions
    - Total Returns (Q3): 829 Transactions (Return Rate: 55.75%)
    - Main Product Categories: Fashion, Home Appliances, Sports, Beauty, Electronics
    - Payment Methods: COD, Bank Transfer, E-Wallet, Credit Card

> Note: Source files were processed per table without merging or joining into a single flat table during ETL; table relationships were defined in Power BI for reporting.

---
## D. ETL Pipeline Architecture

```text
CSV Files (Per Table)
  ├── dim_customers.csv
  ├── dim_products.csv
  ├── order.csv
  └── shipping_details.csv
        │
        ▼  EXTRACT & TRANSFORM (Python / Pandas per table)
           - Remove duplicates
           - Standardize formats & naming
           - Handle missing values
           - Run data quality checks
           - Keep table structure intact (no pre-joining)
        │
        ▼  LOAD (PostgreSQL)
           - Centralized tables as Single Source of Truth
        │
        ▼  MODEL & VISUALIZE (Power BI)
           - Direct connection to PostgreSQL
           - Table relationships configured in Power BI
```    
---

## E. Data Quality Checks

Before loading data into PostgreSQL, validation was performed:
- Duplicates removed
- Date formats & product naming standardized
- Missing values handled
- Data validated before loading into the database

---

## F. Power BI Dashboard

The dashboard was built on top of PostgreSQL to visualize key metrics and support data-driven decisions.

**Example metrics monitored:**
- Gross Revenue & Net Revenue per Quarter / Month
- Total Orders, Total Quantity, Return Rate %
- Return Reasons (Damaged in Transit, Wrong Size / Fit, etc.)
- Gross Revenue per City & Top Sales by Category

*This dashboard is the output of the pipeline above, not a separate analysis project.*

---

## G. Dashboard Insights — Example Use Case

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

## H. What This Pipeline Enables

Because data is now clean, centralized in PostgreSQL, and serves as a Single Source of Truth, the business can:
- Monitor return rate per category, courier, and region without manual recapitulation from CSV files
- Identify root causes of returns based on validated data
- Use a Power BI dashboard directly connected to the database, so data remains consistent

---

## I. Tools & Skills Used

- **ETL Method:** Extract → Transform → Load
- **Transform:** Python (Pandas) — Data Cleansing, Standardization, Handling Missing Values, Data Validation
- **Database:** PostgreSQL (DBMS) — Centralized Database, Single Source of Truth
- **Query:** SQL — Data Validation & Extraction
- **Visualization:** Power BI — Interactive Dashboard connected to PostgreSQL

---
