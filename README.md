# Maritime-Logistics-Data-Analysis

**Data Quality Assessment & Operational Insights**

**Project Overview**

This project explores a simulated international maritime logistics dataset to assess data quality, structural consistency, and operational performance across terminals, vessels, and time.

**The analysis was conducted in two main phases:**

1. Data Quality & Structural Validation
2. Exploratory Analysis for Operational Insights

The goal is to ensure that insights derived from the dataset are reliable, consistent, and meaningful.

**Dataset Description**

The dataset consists of four relational tables:
1. fact_cargo_movements: cargo movement records
2. dim_vessel: vessel attributes
3. dim_terminal: terminal and regional information
4. dim_time: temporal attributes

These tables are linked via foreign key relationships:
vessel_id
terminal_id
date_id

**Phase 1: Data Quality Assessment**

1. Referential Integrity Check
It was verified that all foreign keys in the fact table correctly map to corresponding dimension tables.
Missing vessel IDs: 0
Missing terminal IDs: 0
Missing date IDs: 0
Result: The dataset maintained referential integrity

2. Functional Dependency Analysis
The assumption below was tested:
vessel_id → vessel_name, vessel_category, build_year
However, this dependency was violated.
 **Issue Identified:** A single vessel_id mapped to multiple:
vessel names
categories
build years
Total inconsistent records: 264 vessels

**3. Data Cleaning Approach**
To resolve inconsistencies, a grouping-based strategy was applied:
Grouped data by vessel_id
Selected:
Most consistent (frequent) attribute values
Maximum build_year where necessary
This ensured each vessel had a single, consistent identity

***4. Validation**
After cleaning:
Inconsistent vessels reduced from 264 → 0
Result: Functional dependency restored
vessel_id now behaves as a valid primary key

**Data Preparation**
The cleaned vessel dataset was merged with:
cargo movement data
terminal data
time data
Additional features were created:
vessel_age = current year – build year
year_month for time-based analysis

# Phase 2: Exploratory Analysis (Overview)
With a clean dataset, the analysis focused on identifying operational inefficiencies.
Key Areas Explored:
Cargo movement trends over time
Terminal-level performance
Vessel category impact on movement duration
Regional variations in efficiency
Suez Canal Disruption Analysis (Planned)
A key focus of the analysis is to investigate the impact of the 2021 Suez Canal blockage on:
Cargo volumes
Movement delays
Regional performance
This will help determine:
Whether disruptions are visible in operational data
How long recovery took

**Limitations**
Dataset is simulated and may not fully reflect real-world complexity
Some assumptions (e.g., attribute selection during cleaning) may introduce minor bias
Terminal capacity data was not available and may be engineered in future analysis

**Key Learnings**
Data quality issues can invalidate analytical results if not addressed
Functional dependency violations are common in real-world datasets
Proper data validation is essential before any analysis or modeling
Structured data preparation improves reliability and interpretability

**Next Steps**
Build Power BI dashboards for operational insights
Perform bottleneck and efficiency analysis
Quantify impact of global disruptions (Suez event)
Introduce capacity modeling for terminals

**Tools Used**
Python (Pandas, NumPy)
Google Colab
Power BI (planned)

**Repository Contents**
Data cleaning notebooks
Processed datasets
Documentation (this report)
Future dashboards and insights

