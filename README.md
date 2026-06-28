# 📊 Salary Decoder — Bangalore Tech Compensation Analyzer

Salary Decoder is an automated data cleaning and business intelligence pipeline built in Python to decode real-world compensation trends. Processing a messy, raw dataset of 1,015 tech professionals in Bangalore, the pipeline purges structural inconsistencies to extract high-value career insights and identify relative compensation disparities.

This project was built as part of **The Unlox Academy Minor Project**.

---

## 🛠️ The Data Challenge: Real-World Inconsistencies
Raw HR and corporate datasets are notoriously messy. Before extracting insights, the pipeline tackles significant structural issues:
* **Unit Fragmentation Trap:** Salaries are mixed up between numerical scales (e.g., Lakhs vs. absolute Rupees), creating massive statistical skews[cite: 2].
* **Fragmented Categorization:** Inconsistent naming conventions for the same attributes (e.g., `mnc` vs `MNC`, `Tier 1` vs `Tier-1`, `Ds` vs `Data Scientist`)[cite: 2].
* **Missing & Duplicate Blocks:** Structural gaps across `previous_ctc`, `skills`, and `location` columns alongside duplicate employee logs[cite: 2].

---

## ⚙️ Pipeline Stages & Features

### 1. Robust Data Cleansing & Standardization (`pandas`)
* **Snake_Case Normalization:** Standardizes all DataFrame features for clean programmatic access[cite: 2].
* **Numeric Sanitization:** Strips text punctuation, white spaces, and currency symbols to safely cast character objects into clean floating-point metrics[cite: 2].
* **Categorical Mapping:** Maps and collapses fragmented string variations into uniform, high-level structural dimensions for corporate roles, company tiers, and educational brackets[cite: 2].
* **Deduplication:** Cleans baseline data integrity by purging duplicate employee records[cite: 2].

### 2. Business Intelligence & Analytics Modules
* **CTC Distribution by Role:** Aggregates and sorts median, mean, minimum, and maximum salaries across all engineering and management positions[cite: 2].
* **Experience Curve Analytics:** Groups continuous experience vectors into distinct career bands (`0-1`, `2-3`, `4-5`, `6+`) and measures chronological growth rates between milestones[cite: 2].
* **Skill Premium Evaluation:** Isolates specific software roles to evaluate the direct monetary premium of secondary specializations (e.g., Machine Learning, AWS, System Design, Kubernetes) using logical string matching[cite: 2].
* **Market Disparity Mapping:** Dynamically slices the data across macro company types (Unicorns vs. MNCs) to evaluate cross-organizational compensation premiums[cite: 2].
* **Underpaid Professional Identification Engine:** Implements customized peer-group comparison logic. By grouping rows dynamically by `role`, `company_type`, and `exp_band`, it calculates the group median and flags the top 10 professionals facing the largest negative compensation gap relative to their exact market peers[cite: 2].

---

## 💡 Key Business Insights Discovered

1. **The Management Premium:** Product Managers (PMs) hold the highest median compensation structure across the analyzed corporate dataset[cite: 2].
2. **The High-Income Specialization:** Integrating **Machine Learning (ML)** yields the highest positive salary premium for Software Development Engineers compared to alternative architectural domains[cite: 2].
3. **The Data Integrity Lesson:** Due to extreme unit fragmentation in raw inputs (Rupees vs. LPA), mathematical outliers emerge clearly when comparing mean vs. median metrics[cite: 2]. This underscores why raw data must undergo thorough unit normalization before being fed into business reporting layers[cite: 2].

---

## 📊 Pipeline Output Preview

When executing the terminal report module, the system generates a clean executive breakdown[cite: 2]:

```text
======================================================================
               SALARY DECODER REPORT
======================================================================

TASK 2 - DATA CLEANING
----------------------------------------------------------------------
Columns converted to snake_case
CTC columns converted to numeric
Role names standardized
Company types standardized
Education tiers standardized
Duplicate records removed

TASK 3 - BUSINESS ANALYSIS
----------------------------------------------------------------------
Q3.1 CTC Distribution by Role
Highest Paying Role : PM
Lowest Paying Role  : Backend Developer

Q3.2 Experience Curve
exp_band
0-1         16.20
2-3         23.30
4-5         27.25
6+     3360000.00
Name: current_ctc, dtype: float64

Q3.3 Skill Premium
           Skill  Median CTC (With Skill)  Median CTC (Without Skill)  Premium
1             ML                    31.80                       26.05     5.75
0            AWS                    27.15                       26.20     0.95
2  System Design                    21.40                       27.30    -5.90
3     Kubernetes                    16.50                       28.15   -11.65

Q3.4 Company Type Premium
company_type
Early-stage    1939999.0
MNC                 24.2
Mid-size            55.0
Unicorn        1370000.0
Name: current_ctc, dtype: float64
Unicorn Premium over MNC: 5661057.02 %

Q3.5 Underpaid Professionals
    employee_id            role  years_exp  current_ctc    company company_type      gap
761     BLR0887  Data Scientist          2         19.7     Google          MNC     -6.9
248     BLR0757  Data Scientist          3         20.7        IBM          MNC     -5.9
135     BLR0120  Data Scientist          3         21.8  Microsoft          MNC     -4.8

======================================================================
END OF REPORT
======================================================================
