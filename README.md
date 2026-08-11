# Bee Haven — Data Engineering Pipeline (Bronze to Silver)

This repository contains the data preparation pipeline for the **Bee Haven** project. Raw IoT sensor metrics are collected, cleaned, standardized, and stored in optimized Parquet format for downstream analytics.

---

## 🏗 Project Architecture & Structure

```text
BEE_HAVEN/
 ├── 📁 bronze/          # Raw input data layer (CSV files)
 │    ├── 📁 archive/
 │    └── 📁 new/
 ├── 📁 silver/          # Cleaned & standardized Parquet layer
 ├── 📁 gold/            # Business aggregations layer
 ├── 📁 notebooks/       # Jupyter Notebooks
 │    └── 02_silver_layer_processing.ipynb
 ├── 📄 .gitignore
 ├── 📄 README.md
 └── 📄 requirements.txt

## Datasets Handled

- Flow: Hive entry/exit counts (CSV to flow_silver.parquet)
- Humidity: Ambient humidity metrics (CSV to humidity_silver.parquet)
- Temperature: Hive temperature readings (CSV to temperature_silver.parquet)
- Weight: Hive total weight metrics (CSV to weight_silver.parquet)

---

## Data Transformations Applied (Bronze to Silver)

1. Column Standardization: Transformed all column names to snake_case format and removed special characters.
2. Timestamp Normalization: Converted all date-time strings to UTC datetime64.
3. Flow Logic Resolution: Disambiguated duplicated timestamps in traffic flow metrics by categorizing events into departure vs arrival.
4. Data Cleaning & Outlier Filtering: Removed exact duplicate entries and filtered out impossible sensor readings.
5. Format Optimization: Exported all datasets to Parquet files to reduce storage footprint and speed up query performance.

---

## How to Run Locally

1. Clone the repository:
   git clone <your-github-repo-link>
   cd Bee_Haven

2. Set up virtual environment & dependencies:
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt

3. Execute the notebook:
   Open notebooks/02_silver_layer_processing.ipynb in VS Code and run all cells sequentially.
