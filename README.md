# 🚀 End-to-End Food Supply Chain Data Engineering Project (Databricks)

## 📌 Project Overview

This project demonstrates a **complete end-to-end Data Engineering pipeline** built using **Databricks, Delta Lake, and the Medallion Architecture (Bronze → Silver → Gold)**.
The goal of the project is to simulate a **real-world food supply chain analytics platform** where raw shipment data is ingested, cleaned, transformed into dimensional models, and finally used for **business analytics dashboards and insights**.

The pipeline processes supply chain data including **products, suppliers, cities, warehouses, shipment dates, delivery dates, shipping modes, and costs** to generate actionable insights for operations and logistics teams.

This project was built to demonstrate **industry-level data engineering practices**, including:

* Data ingestion pipelines
* Data quality validation
* Dimensional data modeling
* Delta Lake storage
* Automated job scheduling
* Data warehouse style analytics
* Interactive dashboards

---

# 🏗 Architecture

The project follows the **Medallion Architecture**, a standard data engineering design pattern used in modern data platforms.

```
Raw CSV Data
      │
      ▼
Bronze Layer (Raw Ingestion)
      │
      ▼
Silver Layer (Cleaned & Validated Data)
      │
      ▼
Gold Layer (Analytics Views)
      │
      ▼
Databricks SQL Dashboard
```

---

# 📂 Project Structure

```
supply-chain-data-engineering-databricks/

│
├── notebooks
│   ├── 01_bronze_food_supply_ingestion
│   ├── 02_silver_food_supply_transformation
│   └── 03_gold_food_supply_analytics
│
├── data
│   └── raw_food_supply_chain.csv
│
├── dashboards
│   └── food_supply_chain_dashboard
│
└── README.md
```

---

# 🥉 Bronze Layer – Raw Data Ingestion

The Bronze layer stores **raw ingested data** exactly as received from the source system.

### Objectives

* Load raw CSV data
* Preserve original schema
* Store data in Delta tables
* Enable historical tracking

### Bronze Table

```
scf_bronze.raw_supply.bronze_food_supply_chain
```

### Ingestion Logic

Key steps performed:

1. Read raw CSV dataset
2. Infer schema
3. Store data as Delta table
4. Enable scalable storage for downstream transformations

Example logic:

```python
raw_df = spark.read \
.option("header", True) \
.option("inferSchema", True) \
.csv("/Volumes/workspace/default/raw_food_supply_chain.csv")

raw_df.write.format("delta") \
.mode("overwrite") \
.saveAsTable("scf_bronze.raw_supply.bronze_food_supply_chain")
```

---

# 🥈 Silver Layer – Data Cleaning & Transformation

The Silver layer contains **cleaned, validated, and structured data** ready for analytics.

This layer applies multiple **data quality rules**.

### Data Validation Rules

The pipeline ensures:

* No null values in critical fields
* Positive shipment quantities
* Positive costs
* Delivery date must be greater than shipment date
* Total cost recalculated

Example validation:

```python
validated_df = df.filter(
(col("quantity_shipped") > 0) &
(col("unit_cost") > 0) &
(col("delivery_date") >= col("shipment_date"))
)
```

---

# 📊 Dimensional Data Modeling

To support analytics workloads, the Silver layer creates a **star schema model**.

### Dimension Tables

```
scf_silver.dim.product
scf_silver.dim.supplier
scf_silver.dim.location
scf_silver.dim.date
```

### Fact Table

```
scf_silver.fact.shipments
```

This schema design enables **efficient analytical queries**.

---

# 🥇 Gold Layer – Business Analytics Layer

The Gold layer provides **aggregated views for BI dashboards**.

Instead of raw tables, the Gold layer exposes **business-friendly analytical views**.

### Views Created

```
scf_gold.analytics.vw_shipments
scf_gold.analytics.vw_revenue_by_city
scf_gold.analytics.vw_revenue_by_product
```

These views support fast analytical queries and dashboard visualizations.

---

# ⚙️ Automated Pipeline

A **Databricks Job Pipeline** orchestrates the entire workflow.

### Pipeline Tasks

```
Bronze Ingestion
      ↓
Silver Transformation
      ↓
Gold Analytics
```

### Benefits

* Automated data refresh
* Scheduled execution
* Dependency management
* Scalable processing

---

# 📊 Analytics Dashboard

A **Databricks SQL Dashboard** was created to visualize supply chain insights.

### Dashboard Metrics

The dashboard includes:

#### Revenue by Product

Shows which products generate the highest revenue.

#### Revenue Distribution by City

Breakdown of shipment revenue across cities.

#### Shipment Cost by City and Mode

Heatmap visualizing logistics cost patterns.

#### Shipment Trends Over Time

Time series analysis of shipment volumes.

#### Top Cities by Shipment Revenue

Identifies the highest performing logistics hubs.

---

# 🔎 Key Insights

The dashboard enables several powerful insights.

### 1️⃣ Road Transport Dominates Logistics Costs

Road shipping accounts for the majority of total shipment cost across all cities, indicating heavy reliance on ground transportation.

### 2️⃣ Kanpur Generates Highest Shipment Revenue

Kanpur appears as the top city contributing to overall logistics revenue.

### 3️⃣ Product Demand Varies Significantly

Products such as **Tomato and Sweet Potato** show higher shipment revenue compared to others.

### 4️⃣ Seasonal Shipment Patterns

Shipment quantities fluctuate across months, suggesting seasonal demand patterns.

### 5️⃣ Air Transport Used Selectively

Air shipping appears limited and primarily used for specific shipment scenarios due to higher costs.

---

# 🛠 Tech Stack

| Category        | Tools                     |
| --------------- | ------------------------- |
| Data Platform   | Databricks                |
| Storage         | Delta Lake                |
| Processing      | PySpark                   |
| Architecture    | Medallion Architecture    |
| Data Modeling   | Star Schema               |
| Orchestration   | Databricks Jobs           |
| Visualization   | Databricks SQL Dashboards |
| Version Control | GitHub                    |

---

# 📈 Skills Demonstrated

This project demonstrates the following data engineering skills:

* Data ingestion pipelines
* Data cleaning and validation
* PySpark transformations
* Delta Lake storage
* Dimensional modeling
* Analytical view creation
* Data pipeline orchestration
* Dashboard development
* Git integration

---

# 🚀 How to Run This Project

### Step 1

Upload raw dataset.

### Step 2

Run Bronze ingestion notebook.

```
01_bronze_food_supply_ingestion
```

### Step 3

Run Silver transformation notebook.

```
02_silver_food_supply_transformation
```

### Step 4

Run Gold analytics notebook.

```
03_gold_food_supply_analytics
```

### Step 5

Execute the Databricks Job Pipeline.

---

# 📌 Future Improvements

Possible enhancements include:

* Incremental ingestion pipelines
* Data quality monitoring
* Real-time streaming ingestion
* ML demand forecasting
* Supply chain optimization models
* Automated anomaly detection

---

# 👨‍💻 Author

**Mayank Deshwal**

Data Engineering Enthusiast | Python | PySpark | SQL | Databricks

---

# ⭐ Project Purpose

This project was built as a **portfolio project to demonstrate real-world data engineering capabilities**, including designing production-style pipelines, building analytics models, and creating executive dashboards.

The project simulates how modern organizations manage large scale data pipelines to power business intelligence and decision making.
