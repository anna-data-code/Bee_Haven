## 🐝 Bee Haven Data Pipeline & Enrichment

A end-to-end Data Engineering pipeline designed to process beehive telemetry data and enrich it with external historical weather observations using the **Medallion Architecture pattern** (Bronze → Silver → Gold).

---

## 🏗️ Architecture & Data Flow

1. **Bronze Layer (Raw Storage)**
   - Raw CSV telemetry files (hive weight, internal temperature, humidity, bee flow).
   - Unedited raw JSON responses fetched directly from external APIs.

2. **Silver Layer (Cleaned & Standardized)**
   - Processed telemetry data converted to optimized **Parquet** format.
   - Cleaned hourly weather dataset (temperature, humidity, precipitation, wind speed) aligned with hive observation timeframes.

3. **Gold Layer (Analytical & Business Ready)**
   - Aggregated metrics and feature-engineered datasets combining environmental and hive parameters for downstream analysis.

---

## 🛠️ Tech Stack & Tools

- **Language:** Python 3.13
- **Data Manipulation:** `pandas`
- **Storage Formats:** CSV, JSON, Apache Parquet
- **External Integration:** BrightSky Weather API (`requests`)
- **Environment & Control:** Jupyter Notebooks, Git / GitHub

---

## 📂 Repository Structure

```text
Bee_Haven/
├── bronze/                 # Raw telemetry CSVs and API JSON responses
│   ├── new/
│   └── weather/
├── silver/                 # Standardized, cleaned Parquet datasets
├── notebooks/
│   ├── 02_silver_layer_processing.ipynb   # Telemetry data transformation
│   └── 03_weather_api_processing.ipynb    # Weather API extraction & processing
├── .gitignore              # Version control ignore rules
├── README.md               # Project overview
└── requirements.txt        # Python dependencies

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
