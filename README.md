# 🏗️ National Asset Health: Rapid Prototype (Auckland Grid)

## 📖 Project Overview
This project is a **Rapid Prototype (Proof of Concept)** designed to demonstrate an end-to-end data engineering lifecycle within **Microsoft Fabric**. The solution ingests simulated telemetry from electrical assets (Transformers, Circuit Breakers) across the New Zealand grid, with a specific focus on the **Auckland metropolitan area.**

The goal was to validate the speed-to-insight for infrastructure monitoring, transforming raw sensor data into a high-accuracy geospatial dashboard.

---

## 🛠️ Tech Stack & Architecture
* **Platform:** Microsoft Fabric (SaaS)
* **Storage:** OneLake (Delta Lake)
* **Orchestration:** Fabric Data Pipelines
* **Processing:** PySpark (Spark 3.4)
* **Reporting:** Power BI (Direct Lake Mode)

### **Data Lineage (Medallion Flow)**
> ![Data Lineage View]<img width="2192" height="1099" alt="Image" src="https://github.com/user-attachments/assets/93e4ace8-f13f-43c1-a02b-e21e46d58da1" />
> *The prototype follows a streamlined Medallion architecture, moving data from raw ingestion to a business-ready Gold layer.*

---

## 🌊 Data Pipeline Strategy

### 1. **Ingestion (Bronze Layer)**
Raw CSV telemetry—simulating Temperature, Oil Levels, and Load—is landed in the Lakehouse. This stage ensures a permanent record of all incoming sensor pings.

### 2. **Logic & Scoring (Silver Layer)**
Using PySpark, I implemented a **Weighted Health Scoring** algorithm. 
* **Calculation:** $HealthScore = (Temp \times 0.5) + (Oil \times 0.3) + (Load \times 0.2)$
* **Outcome:** Assets are automatically categorized (Healthy, Monitor, Critical) to drive maintenance priorities.

### 3. **Reporting Optimization (Gold Layer)**
The data is structured into a clean Star Schema. 
* **Geospatial Engineering:** I implemented a programmatic fix to append "New Zealand" to substation locations (e.g., Penrose, Albany, Henderson), ensuring 100% mapping accuracy for Auckland-based assets.

---

## 🚀 Orchestration & Performance
* **Automation:** Managed via a **Fabric Data Pipeline**, ensuring that the telemetry generation and transformation stages run in a reliable sequence.
* **Direct Lake:** The dashboard utilizes Fabric's **Direct Lake** engine, providing the performance of Import mode with the real-time nature of DirectQuery.

> ![Pipeline Execution]<img width="1580" height="350" alt="Image" src="https://github.com/user-attachments/assets/d5ff209d-42af-4252-8789-f71a79235c8e" />
> *Successful execution of the automated end-to-end workflow.*

---

## 📊 Business Intelligence
The final dashboard provides an executive "Mission Control" for the grid:
* **Auckland Map:** Interactive ArcGIS pins localized to the North Island.
* **KPI Cards:** Real-time counts of critical assets and average fleet health.
* **Investigation Slicers:** Ability to drill down by Substation or Asset Type.

* > ![Semantic Model]<img width="1122" height="588" alt="Image" src="https://github.com/user-attachments/assets/48686e74-0b26-4cfb-81ff-cb7454b69e92" />

> ![Power BI Dashboard]<img width="1979" height="1107" alt="Image" src="https://github.com/user-attachments/assets/aac790fa-597c-407c-8f5d-4b4a6746079e" />

---

## 📈 Future Production Enhancements
To evolve this prototype into a full enterprise-grade system, the following features are planned:
* **Advanced Data Modeling:** Implementation of **Surrogate Keys** and **Hashing (MD5/SHA2)** for robust SCD Type 2 tracking.
* **Real-Time Streaming:** Replacing batch ingestion with **Fabric Eventstreams**.
* **Predictive ML:** Integrating Spark MLlib to forecast **Remaining Useful Life (RUL)**.

---

### **How to use this Repo**
1. Review the `Notebooks/` folder for the PySpark logic.
2. View the `Pipelines/` folder for orchestration metadata.
