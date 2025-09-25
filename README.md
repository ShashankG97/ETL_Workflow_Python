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
CODE
```
"""
ETL Pipeline for Multi-Format Data Extraction, Transformation, and Loading

Sections:
1. Imports & Setup
2. Logging Utility
3. Data Extraction Functions
4. Master Extraction Function
5. Data Transformation
6. Data Loading
7. ETL Execution Sequence
8. Basic Analysis Example
"""

# 1. Imports & Setup
import pandas as pd
from datetime import datetime
import os

# 2. Logging Utility
def log_event(message, log_file="log_file.txt"):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    with open(log_file, "a") as f:
        f.write(f"[{timestamp}] {message}\n")

# 3. Data Extraction Functions
def read_csv_file(path):
    return pd.read_csv(path)

def read_json_file(path):
    return pd.read_json(path, lines=True)

def read_xml_file(path):
    return pd.read_xml(path)

# 4. Master Extraction Function
def master_reader(file_paths):
    all_data = []
    for path in file_paths:
        if path.endswith(".csv"):
            df = read_csv_file(path)
        elif path.endswith(".json"):
            df = read_json_file(path)
        elif path.endswith(".xml"):
            df = read_xml_file(path)
        else:
            raise ValueError(f"Unsupported file type: {path}")
        all_data.append(df)
    final_df = pd.concat(all_data, ignore_index=True)
    return final_df

# 5. Data Transformation
def transform(df):
    # Convert heights from inches to meters
    if 'height' in df.columns:
        df['height_m'] = df['height'] * 0.0254
    # Convert weights from pounds to kilograms
    if 'weight' in df.columns:
        df['weight_kg'] = df['weight'] * 0.453592
    return df

# 6. Data Loading
def load_to_csv(df, output_path):
    df.to_csv(output_path, index=False)

# 7. ETL Execution Sequence
def run_etl():
    # Extraction Phase
    log_event("Extraction started")
    source_dir = "./source"
    files = [os.path.join(source_dir, f) for f in os.listdir(source_dir)
             if f.endswith(('.csv', '.json', '.xml'))]
    result = master_reader(files)
    log_event("Extraction completed")

    # Transformation Phase
    log_event("Transformation started")
    transformed_data = transform(result)
    log_event("Transformation completed")

    # Loading Phase
    log_event("Loading started")
    output_file = "transformed_data.csv"
    load_to_csv(transformed_data, output_file)
    log_event("Loading completed")

    return transformed_data


```
