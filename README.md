# ETL Project (Bronze → Silver → Gold)

This repository implements a simple **medallion architecture** ETL pipeline with three layers:

- **Bronze Layer**: Raw ingestion (as-is data landing)
- **Silver Layer**: Cleaned and standardized datasets
- **Gold Layer**: Curated, analytics-ready datasets (business aggregates)

The pipeline is executed via three Jupyter notebooks that **must be run in order**:
1. `Bronze_Mario.ipynb`
2. `Silver_Mario.ipynb`
3. `Gold_Mario.ipynb`

---

## Repository Structure

ETL PROJECT/
├─ mario_data/
│ ├─ mario_data_20250101.csv
│ ├─ mario_data_20250201.csv
│ ├─ mario_data_20250301.csv
│ ├─ mario_data_20250401.json
│ ├─ mario_data_20250501.json
│ └─ mario_data_20250601.json
│
├─ Bronze layer/
│ └─ Bronze.parquet
│
├─ Silver layer/
│ └─ Silver.parquet
│
├─ Gold layer/
│ ├─ gold_hits_team.parquet
│ ├─ gold_player_performance.parquet
│ ├─ gold_powerup_player.parquet
│ ├─ gold_risk_assessment.parquet
│ ├─ gold_spending_analysis.parquet
│ ├─ gold_team_summary.parquet
│ ├─ gold_top_player_per_team.parquet
│ ├─ gold_vehicle_counts.parquet
│ ├─ gold_world_completion.parquet
│ └─ gold_world_difficulty.parquet
│


---

## ETL Layers

### 1) Bronze Layer (Raw Ingestion)
**Notebook:** `Bronze_Mario.ipynb`  
**Input:** `mario_data/*.csv`, `mario_data/*.json`  
**Output:** `Bronze layer/Bronze.parquet`

Purpose:
- Load raw CSV/JSON files
- Apply minimal transformations (schema alignment, basic parsing)
- Persist a raw, queryable parquet dataset

---

### 2) Silver Layer (Clean + Conformed)
**Notebook:** `Silver_Mario.ipynb`  
**Input:** `Bronze layer/Bronze.parquet`  
**Output:** `Silver layer/Silver.parquet`

Purpose:
- Clean and standardize fields
- Handle missing values / types
- Deduplicate, validate, and conform dataset for downstream analytics

---

### 3) Gold Layer (Curated Analytics Outputs)
**Notebook:** `Gold_Mario.ipynb`  
**Input:** `Silver layer/Silver.parquet`  
**Output:** `Gold layer/*.parquet` (multiple curated tables)

Purpose:
- Create business/analytics-ready datasets and aggregates, such as:
  - team summaries
  - top players per team
  - spending analysis
  - world completion and difficulty
  - vehicle counts
  - risk assessment
  - powerup and performance metrics

---

## How to Run (Sequential Execution Required)

Run notebooks **in this exact order**:

1. **Bronze**
   - Open and run: `Bronze_Mario.ipynb`
   - Confirms creation of: `Bronze layer/Bronze.parquet`

2. **Silver**
   - Open and run: `Silver_Mario.ipynb`
   - Confirms creation of: `Silver layer/Silver.parquet`

3. **Gold**
   - Open and run: `Gold_Mario.ipynb`
   - Confirms creation of: `Gold layer/*.parquet`

> Important: The Silver notebook depends on Bronze output, and the Gold notebook depends on Silver output.

---

## Re-running the Pipeline

If you want a clean rebuild, delete prior outputs before running again:

- `Bronze layer/Bronze.parquet`
- `Silver layer/Silver.parquet`
- `Gold layer/*.parquet`

Then re-run: Bronze → Silver → Gold.

---

## Notes
- Ensure all input files are present under `mario_data/` before running Bronze.
- If you add new raw files, re-run the pipeline from Bronze to propagate changes.


├─ Bronze_Mario.ipynb
├─ Silver_Mario.ipynb
└─ Gold_Mario.ipynb
