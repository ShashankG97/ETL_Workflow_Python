# ETL_Workflow_Python
A simple ETL workflow in Python using Pandas. This project extracts data from multiple file formats (CSV, JSON, Excel), processes them with a master function, and combines them into a single DataFrame for analysis. A beginner-friendly example of building ETL pipelines for data engineering.
# ETL Project: Multi-Format Data Pipeline

## Problem Statement
Extract, transform, and load data from multiple file formats (CSV, JSON, XML) into a unified dataset for analysis and storage.

## Tools Used
- Python
- Pandas
- datetime (for logging)
- CSV, JSON, XML file formats

## Approach
1. **Extraction:** Read all supported files from the source directory.
2. **Transformation:** Convert heights (inches to meters) and weights (pounds to kilograms).
3. **Loading:** Save the transformed data to a CSV file.
4. **Logging:** Log each ETL phase with timestamps for traceability.

## How to Run
1. Place your source files in the `source` folder.
2. Run the pipeline:
   ```bash
   python etl_pipeline.py
   ```
3. Check `transformed_data.csv` and `log_file.txt` for results and logs.

## Insights Found
- Unified data enables easier analysis.
- Standardized units improve data consistency.
- Logging provides traceability for auditing and troubleshooting.

## Project Structure
```
ETL Project/
├── etl_pipeline.py
├── README.md
├── source/
│   ├── source1.csv
│   ├── source1.json
│   └── source1.xml
├── transformed_data.csv
└── log_file.txt
```
