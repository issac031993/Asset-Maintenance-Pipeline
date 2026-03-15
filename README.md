# 🏗️ Omexom Asset Health: Predictive Maintenance & NZ Grid Reliability

## 📖 Project Overview
This project demonstrates a production-grade **End-to-End Data Engineering Pipeline** built within **Microsoft Fabric**. It utilizes **programmatically generated telemetry** to simulate high-value electrical assets (Transformers, Circuit Breakers) across New Zealand substations. 

The solution calculates real-time health scores and solves geographic mapping issues, proving how a centralized Lakehouse can monitor a national grid.

---

## 🛠️ Tech Stack & Architecture
* **Platform:** Microsoft Fabric (SaaS)
* **Storage:** OneLake (Delta Lake format)
* **Orchestration:** Fabric Data Pipelines
* **Processing:** PySpark (Spark 3.4)
* **Data Generation:** Python-based Synthetic Telemetry Generator
* **Reporting:** Power BI (Direct Lake Mode)

### **End-to-End Data Lineage**

> ![Data Lineage View](PASTE_LINK_TO_LINEAGE_IMAGE_HERE)
> *This view shows the flow from the Landing Files through the Bronze, Silver, and Gold Delta tables, illustrating the full "OneLake" integration.*

---

## 🌊 Data Pipeline (Medallion Architecture)

### 1. **Data Generation & Ingestion (Bronze Layer)**
Because live SCADA access is restricted for this PoC, a **Synthetic Data Generator** was developed to produce realistic sensor pings (Temperature, Load, Oil Levels) for 30+ assets.
* **Process:** Python script generates CSV logs -> Ingested to `Tables/bronze_asset_health`.

### 2. **Transformation & Logic (Silver Layer)**
Data is cleaned, and business logic is applied to generate **Health Scores**.
* **Logic:** $HealthScore = (Temperature \times 0.5) + (OilLevel \times 0.3) + (Load \times 0.2)$
* **Asset Tagging:** Assets are categorized as **Healthy**, **Monitor**, or **Critical** based on performance thresholds.

### 3. **Business Optimization (Gold Layer)**
Data is structured into a **Star Schema** for high-performance reporting.
* **NZ Mapping Fix:** Programmatically appended ", New Zealand" to all substation names to ensure 100% accuracy on the ArcGIS map visual.

---

## 🚀 Orchestration & Automation
The entire workflow is automated using a **Fabric Data Pipeline**, allowing the "Random Generator" to trigger a full refresh of the reporting layer.

### **Pipeline Execution Flow**
> ![Pipeline Execution](PASTE_LINK_TO_PIPELINE_IMAGE_HERE)
> *This screenshot confirms the successful sequential execution of the Generator, Bronze, Silver, and Gold notebooks.*

---

## 📊 Semantic Model & Reporting
The final output is a high-performance Power BI report utilizing the **Direct Lake** engine for near-zero latency.

### **Semantic Model (Relationship Diagram)**
> ![Semantic Model](PASTE_LINK_TO_MODEL_IMAGE_HERE)
> *Showing the 1-to-Many relationship between `dim_asset` and `fact_asset_readings` using AssetID.*

### **Power BI Dashboard**
> ![Power BI Dashboard](PASTE_LINK_TO_DASHBOARD_IMAGE_HERE)
> *Highlighting the New Zealand map pins and the critical asset watchlist.*

---

## 📈 Key Achievements
* **Telemetry Simulation:** Created a robust generator that mimics real-world sensor drift and equipment failure patterns.
* **Geospatial Engineering:** Solved the "Hamilton, Canada" mapping error by programmatically localizing the dimension table in the Gold layer.
* **Scalable Framework:** Built a modular system that can easily transition from "Simulated Data" to "Production SCADA Data."
