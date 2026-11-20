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
    - `order.csv` -> `order`
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

Before loading cleaned tables into PostgreSQL, validation and standardization were applied across datasets:
- Removed duplicate records
- Standardized date formats, text casing/spacing, and product naming
- Handled missing values cleanly
- Verified data consistency prior to database ingestion
---

## F. Power BI Dashboard

The Power BI dashboard connects directly to PostgreSQL to visualize operational metrics and support data-driven tracking.


https://github.com/user-attachments/assets/dbf42ff2-302e-4b38-a580-dd45954e024a



**Key Metrics Monitored:**
- Gross Revenue & Net Revenue per Quarter / Month
- Total Orders, Total Quantity, Return Rate (%)
- Return Reasons (Damaged in Transit, Wrong Size / Fit, Product Quality / Mismatch, Delayed Delivery, etc.)
- Gross Revenue per City & Top Sales by Category

*Note: The dashboard is a reporting layer built on top of the ETL pipeline output rather than a separate standalone project.*

---

## G. Dashboard Insights — Example Use Case

Using the cleaned data in PostgreSQL, the Q3 2026 dashboard highlights several operational patterns:

1. **Return Rate by Category & Root Causes**
   - Fashion recorded the highest return rate at 73.88%.
   - Main return drivers (Pareto breakdown): Damaged in Transit (30.76%), Product Quality / Mismatch (28.83%), Wrong Size / Fit (23.88%), and Delayed Delivery (16.53%).

2. **Regional & Courier Performance**
   - Delivery duration and item safety issues were more noticeable outside Java (particularly Medan and Makassar).
   - Specific courier partners showed Damaged in Transit rates above the operational average.

3. **COD Return Vulnerability**
   - Cash on Delivery (COD) transactions showed higher return vulnerability (62.89%), especially when combined with categories prone to sizing/fit issues like Fashion upon delivery.

> Note: These insights illustrate example monitoring outputs enabled by the pipeline; the core focus of this repository is the ETL workflow and data reliability.

---

## H. What This Pipeline Enables

With standardized tables centralized in PostgreSQL as a Single Source of Truth:
- Teams can track return rates by category, region, and courier without manual CSV compilation
- Return causes can be reviewed consistently using validated data
- Reporting stays aligned through a live connection to the structured database

---

## I. Tools & Skills Used

- **Pipeline Workflow:** Extract → Transform → Load (ETL)
- **Data Cleaning & Transformation:** Python (Pandas) — Deduplication, Standardization, Missing Value Handling, Data Quality Validation
- **Database:** PostgreSQL — Centralized Storage, Single Source of Truth
- **Querying & Validation:** SQL
- **BI & Visualization:** Power BI (Connected to PostgreSQL with data model relationships)
---
