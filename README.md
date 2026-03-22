# 🎫 SeatGeek Ticket Sales Analytics
**An End-to-End dbt & BigQuery Data Pipeline**

## 🚀 Project Overview
This project transforms raw SeatGeek sales and event data into a production-ready analytics layer. Using dbt and BigQuery, I've built a scalable pipeline that follows the **Medallion Architecture**—moving data from raw seeds through a cleaning (Staging) layer into refined reporting tables (Marts).

---

### 📈 Data Lineage & Architecture
The power of this project lies in its modularity. Each step is documented and tested to ensure data flows correctly from source to insight.


<img width="1290" height="506" alt="image" src="https://github.com/user-attachments/assets/d504db1f-7c93-43c1-8ca3-7283852de450" />

My dbt lineage showing the flow from CSV seeds into Staging and finally into the Performance Marts.*

---

## 🛠️ Tech Stack
* **Warehouse:** Google BigQuery
* **Transformation:** dbt Cloud
* **Language:** SQL (BigQuery Dialect) & YAML (Configuration)
* **Package Management:** `dbt_utils` for advanced testing

---

## 🏗️ Engineering Highlights & Decisions

### 1. Robust Dependency Management
I resolved a critical "404 Table Not Found" race condition by migrating from a loose `source()` configuration to a strict `ref()` pattern for seed data. This ensures dbt respects the execution order, building the static seed tables before attempting to create downstream views.

### 2. Automated Data Quality (Testing)
Data trust is a priority. I implemented automated tests using the `dbt_utils` package to ensure the "Vitals" of the data are always healthy:
* **Custom Range Validation:** Used `accepted_range` to ensure `days_until_event` is never negative.
* **Integrity Checks:** Applied `unique` and `not_null` constraints to all Primary Keys.

<img width="1308" height="443" alt="image" src="https://github.com/user-attachments/assets/57711c19-3fc6-469f-98c0-c9387e73c03e" />

*A successful 'dbt build' execution showing all 10+ data integrity tests passing in the Production environment.*

### 3. Environment Separation
I established a strict boundary between **Development** (`dbt_mrollins`) and **Production** (`dbt_prod`) environments. This allows for safe iteration in a sandbox without affecting live executive dashboards.

---

## ⚙️ Orchestration & Deployment
To ensure data reliability, I configured a dbt Cloud Job to automate the production build. I successfully troubleshot early environment mismatches by implementing a "Seed-First" strategy, ensuring all static lookup tables are refreshed before the transformation models execute.

<img width="2140" height="687" alt="image" src="https://github.com/user-attachments/assets/8b74ba36-502e-4195-87f1-28e3b066e639" />

*Orchestration history showing the successful resolution of dependency errors through a refined build strategy.*

---

## 📊 Final Data Product: BigQuery Output
The final `dm_event_performance` model provides high-level visibility into:
* **Booking Windows:** Average lead time between purchase and showtime per category.
* **Revenue Concentration:** Identifying high-value event types.

<img width="882" height="165" alt="image" src="https://github.com/user-attachments/assets/36aa9f54-6a07-418b-bf60-f017c25003b5" />

*A preview of the final 'dm_event_performance' table in BigQuery, ready for visualization in Looker Studio.*

---

## 🏁 How to Run This Project
1. **Clone the repo**
2. **Install Dependencies:**
   ```bash
   dbt deps
