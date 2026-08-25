# healthflow_platform
This project demonstrates how to integrate github and databricks and create medallion architecture for healthcare dataset and perform transformations and analytics. Using lakeflow create and schedule workflows that run periodically. All the tables created are governed and managed through unity catalog and data quality checks for data integrity. 

project folder structure as below
healthflow_platform/
├── notebooks/
│   ├── 00_setup_catalog.py         ← Create schemas (bronze, silver, gold), volumes & paths
│   ├── 01_bronze_batch.py          ← Batch ingestion (Providers, Static Reference Data)
│   ├── 02_bronze_streaming.py      ← Auto Loader streaming (Clinical Encounters & Vitals)
│   ├── 03_silver_patients.py       ← Deduplicate & sanitize patient demographics
│   ├── 04_silver_providers.py      ← Validate & clean healthcare provider credentials
│   ├── 05_silver_encounters.py     ← Flatten/explode nested clinical visit logs & diagnoses
│   ├── 06_gold_patient_billing.py  ← Calculate readmission rates & length of stay using Window functions
│   ├── 07_data_quality.py          ← Data expectations & quality validation (Lakeflow / DLT rules)
│   └── 08_agent_demo.py            ← Mosaic AI Agent / AI Functions for clinical summarization
├── workflows/
│   └── healthflow_pipeline.yml     ← Databricks Lakeflow Jobs / Pipeline definition as code
├── tests/
│   └── test_silver_patients.py     ← PyTest unit tests for patient data transformations
└── README.md
