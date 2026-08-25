# healthflow_platform
This project demonstrates how to integrate github and databricks and create medallion architecture for healthcare dataset and perform transformations and analytics. Using lakeflow create and schedule workflows that run periodically. All the tables created are governed and managed through unity catalog and data quality checks for data integrity. 

# 🏥 HealthFlow Platform

A production-grade, end-to-end Healthcare Data Engineering platform built on **Databricks**, **PySpark**, **Delta Lake**, and **Unity Catalog**. 

This project simulates a modern Lakehouse architecture processing synthetic patient records, provider data, and streaming clinical encounter logs to deliver analytics-ready data for healthcare insights and clinical reporting.

---

## 📐 Architecture & Data Lineage

The platform follows the **Medallion Architecture** pattern:

```text
[ Raw Synthetic Data ] (JSON / CSV landing in Volumes)
          │
          ▼
    ┌───────────┐
    │  BRONZE   │  Raw, unmodified ingestion with ingestion metadata
    └─────┬─────┘  (Auto Loader streaming for encounters, Batch for demographics)
          │
          ▼
    ┌───────────┐
    │  SILVER   │  Cleaned, deduplicated, enriched schemas
    └─────┬─────┘  (Patients, Providers, Flattened Encounter Logs)
          │
          ▼
    ┌───────────┐
    │   GOLD    │  Aggregated analytics & business metrics
    └───────────┘  (Patient lifetime costs, Length of Stay, Readmission rates)

healthflow_platform/
├── notebooks/
│   ├── 00_setup_catalog.py         # Schema initialization & Volume path setup
│   ├── 01_bronze_batch.py          # Batch ingestion (Provider & static reference data)
│   ├── 02_bronze_streaming.py      # Auto Loader streaming ingestion for clinical encounters
│   ├── 03_silver_patients.py       # Patient demographics cleaning & deduplication
│   ├── 04_silver_providers.py      # Provider credentials parsing & validation
│   ├── 05_silver_encounters.py     # Unnesting/flattening nested visit & diagnosis logs
│   ├── 06_gold_patient_billing.py  # Clinical & cost analytics via PySpark Window functions
│   ├── 07_data_quality.py          # Data Quality framework & integrity checks
│   └── 08_agent_demo.py            # AI summarization & LLM functions for clinical notes
├── workflows/
│   └── healthflow_pipeline.yml     # Databricks Lakeflow Job workflow definition (CI/CD)
├── tests/
│   └── test_silver_patients.py     # PyTest unit tests for patient transformations
└── README.md

Databricks services used in this project are below.
Databricks unity catalog
Databricks workspaces
Databricks lakeflow
Databricks medallion architecture (Bronze, silver, gold)
Databricks SQL warehouse
