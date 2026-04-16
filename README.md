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

# Phase 2: 📊 Exploratory Data Analysis (EDA)

## Objective

The goal of the exploratory data analysis was to uncover patterns, trends, and inefficiencies in maritime cargo operations, with a focus on:

* Identifying operational bottlenecks
* Understanding drivers of cargo movement delays
* Evaluating terminal and vessel performance
* Detecting the impact of external disruptions (e.g., Suez Canal incident)

## 📈 Descriptive Statistics

Summary statistics revealed the overall distribution of key variables:

* **Container Count**: Wide variation in cargo volumes across movements
* **Move Duration**: Significant spread, indicating variability in operational efficiency
* **Vessel Age**: Broad range, allowing analysis of age-related performance

### Observation

Extreme maximum values (e.g., very high container counts and movement durations) suggest the presence of **outliers**, likely due to simulated data generation.

These values may distort averages and were considered during interpretation.

## 📊 Distribution Analysis

**Container Count**

* Distribution is right-skewed
* Majority of movements involve moderate container volumes
* A small number of movements handle extremely high volumes

**Move Duration**

* Also right-skewed
* Indicates that while most operations complete within a reasonable time, some experience **significant delays**

**Time-Based Trends**

Monthly aggregation of cargo movements revealed patterns over time:

* Fluctuations in both **cargo volume** and **movement duration**
* Periods of increased delay potentially linked to operational disruptions

### 🚢 Suez Canal Disruption (March 2021)

The dataset was examined for anomalies around March 2021.

* Variations in cargo movement trends suggest **disruption effects**
* Changes in movement duration indicate temporary inefficiencies
* Recovery patterns can be observed in subsequent months

This demonstrates how global events can impact logistics performance.

## 🏗️ Terminal Performance Analysis

Terminal-level aggregation revealed:

* Certain terminals handle significantly higher cargo volumes
* High-volume terminals also exhibit **longer average movement durations**

### Key Insight

> High activity does not necessarily imply high efficiency.

**Bottleneck Detection**

A scatter plot of:

* **Total Container Count (X-axis)**
* **Average Move Duration (Y-axis)**

showed a **positive relationship**:

Terminals handling more cargo tend to experience longer delays

**Business Interpretation**

* Some terminals may be operating beyond optimal capacity
* Load imbalance across terminals contributes to inefficiency

## 🚢 Vessel Analysis

**By Vessel Category**

Average movement duration varies by vessel type:

* **Passenger vessels** → highest movement duration
* **Cargo/Container vessels** → relatively faster

**Insight**

Different vessel types have different operational requirements, impacting processing time.

**Vessel Age Impact**

Analysis of vessel age vs movement duration shows:

* No strong linear relationship
* Older vessels are not consistently slower

**Interpretation**

Vessel age is **not a primary driver** of inefficiency.

## 🌙 Shift Analysis

Comparison of operational shifts:

* **Day Shift** → slightly higher movement duration
* **Night Shift** → relatively faster operations

**Insight**

Night operations may benefit from:

* Reduced congestion
* Smoother workflow

**Key Findings**

* Data quality issues were identified and resolved prior to analysis
* High-volume terminals are associated with longer movement durations
* Cargo workload is a key driver of operational inefficiency
* Vessel category influences processing time
* Night shifts demonstrate better efficiency than day shifts
* Extreme outliers exist and should be handled cautiously

## 📌 Conclusion

The exploratory analysis highlights that **operational inefficiencies are not random**, but are influenced by:

* Terminal workload
* Vessel characteristics
* Operational timing

These findings provide a strong foundation for:

* Performance optimization
* Capacity planning
* Strategic decision-making

---

## 🚀 Next Steps

* Develop Power BI dashboards for executive reporting
* Quantify terminal capacity constraints
* Build predictive models for movement delays
* Further investigate disruption recovery patterns

**Limitations**
Dataset is simulated and may not fully reflect real-world complexity
Some assumptions (e.g., attribute selection during cleaning) may introduce minor bias
Terminal capacity data was not available and may be engineered in future analysis

**Key Learnings**
Data quality issues can invalidate analytical results if not addressed
Functional dependency violations are common in real-world datasets
Proper data validation is essential before any analysis or modeling
Structured data preparation improves reliability and interpretability

**Tools Used**
Python (Pandas, NumPy)
Google Colab
Power BI (planned)

**Repository Contents**
Data cleaning notebooks
Processed datasets
Documentation (this report)
Future dashboards and insights

