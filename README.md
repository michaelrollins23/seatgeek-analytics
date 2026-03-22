# 🎫 SeatGeek Ticket Sales Analytics
**An end-to-end dbt & BigQuery Pipeline**

## 🚀 Project Overview
This repository contains a professional dbt (Data Build Tool) project that transforms raw SeatGeek sales and event data into a production-ready analytics layer. The project follows the **Medallion Architecture**, moving data from raw seeds through a cleaning (Staging) layer into refined reporting tables (Marts).



## 🛠️ Tech Stack
* **Warehouse:** Google BigQuery
* **Transformation:** dbt Cloud
* **Package Management:** `dbt_utils`
* **Version Control:** GitHub with distinct Dev/Prod environments

## 🏗️ Data Modeling & Engineering
I implemented several advanced Analytics Engineering patterns to ensure this pipeline is scalable and reliable:

### 1. Robust Dependency Management
* Migrated from `source()` to `ref()` for CSV seed data. This forced a **Hard Dependency** in the dbt graph, resolving race conditions and "404 Table Not Found" errors during parallel builds.

### 2. Automated Data Quality (Testing)
* Integrated `dbt_utils` to enforce data integrity.
* **Range Validation:** Used `accepted_range` to ensure `days_until_event` is never negative.
* **Schema Enforcement:** Applied `unique` and `not_null` tests to primary keys like `sale_id`.

### 3. Environment Separation
* Established a strict boundary between **Development** (`dbt_mrollins`) and **Production** (`dbt_prod`) to ensure code is vetted before affecting live datasets.



## 📊 Business Insights
The final `dm_event_performance` model provides high-level visibility into:
* **Booking Windows:** Which event types have the longest lead time between purchase and showtime?
* **Revenue Concentration:** Identifying high-value event categories.

## 🏁 Setup & Execution
1. **Install Dependencies:**
   ```bash
   dbt deps
