# Healthcare Claims Data Analysis

---

## Project Overview

This project analyzes healthcare claims data from Stony Brook University Hospital to support compliance and revenue cycle management. The analysis examines billing patterns, common diagnoses, procedures, and payer relationships using real-world prospective claims data.

---

## Dataset Description

The analysis uses three interconnected CSV files forming a relational database:

### Files:
1. **STONYBRK_20240531_HEADER.csv** - Claim-level information
   - Provider NPIs and names
   - Service dates
   - Primary payer information
   - Place of service

2. **STONYBRK_20240531_LINE.csv** - Service line details
   - CPT/HCPCS procedure codes
   - Charges and units
   - Procedure modifiers
   - Diagnosis mapping

3. **STONYBRK_20240531_CODE.csv** - Diagnosis codes
   - ICD-10 diagnosis codes
   - Code positions and qualifiers

**Note:** Data files are NOT included in this repository due to size and privacy considerations. Files should be stored locally in a `data/` directory.

---

## How to Run

### Option 1: Google Colab (Recommended)
1. Open the notebook in [Google Colab](https://colab.research.google.com/)
2. Upload the three data files to the Colab environment
3. Run each cell sequentially
4. Visualizations will appear inline

### Option 2: Local Jupyter Notebook
1. Clone this repository

2. Install dependencies

3. Place data files in the `data/` directory

4. Launch Jupyter Notebook

---

## Analysis Components

### Part 1: Data Loading & Exploration
- Loaded and validated three relational claims files
- Explored data structure, missing values, and basic statistics
- Identified **388 unique claims** spanning **2023-09-25 to 2024-05-29**
- Calculated averages: **1.34** service lines per claim, **3.96** diagnosis codes per claim

### Part 2: Relational Data Analysis

**Question 1: Top Billing Providers**
- Identified top 5 providers by claim volume
- **Key Finding:** [SB INTERNISTS] submitted the most claims with 152 claims

**Question 2: Payer Mix**
- Analyzed claim distribution across insurance payers
- **Key Finding:** Top 5 payers represent 87.89% of total claims

**Question 3: Common Diagnoses**
- Identified 10 most frequent ICD-10 diagnosis codes
- **Key Finding:** J96.01 appeared 62 times

**Question 4: Common Procedures**
- Analyzed most frequently billed CPT/HCPCS codes
- **Key Finding:** CPT 99291 (CRITICAL CARE, INITIAL FIRST HOUR) was most common with 68 occurrences

**Question 5: Service Locations**
- Compared inpatient vs. outpatient service distribution
- **Key Finding:** 48.85% of claims were inpatient, 44.23% were office-based

### Part 3: Advanced Analysis with Joins

**Question 6: High-Complexity Claims**
- Identified claims with ≥5 service lines
- **Key Finding:** 5 claims had 5+ service lines, indicating complex cases

**Question 7: Diagnosis-Procedure Combinations**
- Analyzed diagnosis codes associated with CPT 99291 (Critical Care)
- **Key Finding:** J96.01 was most commonly paired with critical care services

**Question 8: Charges by Payer**
- Calculated total and average charges per payer
- **Key Finding:** Medicare had highest total charges at $131,008, averaging $541.36 per claim

### Part 4: Creative Analysis

**Question 9: Provider Complexity Analysis**
- **Research Question:** Which providers handle the most complex cases?
- **Methodology:** Created complexity score based on:
  - Number of diagnosis codes (40% weight)
  - Number of service lines (30% weight)  
  - Total charges (30% weight)
- **Key Findings:**
  - NEW YORK SPINE AND BRAIN SURGERY handles the most complex cases (Average complexity score: 41.33)
  - This provider averages 9.23 diagnosis codes per claim compared to simpler cases with 1-3 codes
  - Complexity strongly correlates with diagnosis count, indicating that patients with multiple conditions drive case complexity more than service volume or charges alone

---

## Key Insights

1. **Provider Patterns:** SB INTERNISTS leads in claim volume with 152 claims, representing the primary care entry point. Specialty providers like NEW YORK SPINE AND BRAIN SURGERY handle significantly more complex cases with an average of 9.23 diagnosis codes per claim, indicating treatment of patients with multiple comorbidities.

2. **Payer Mix:** The top 5 payers account for 87.89% of all claims, with Medicare dominating both volume (242 claims) and total charges ($131,008). However, commercial payers like AETNA show higher average charges per claim ($1,155.00), suggesting they cover more complex or specialized procedures.

3. **Clinical Focus:** Critical care services (CPT 99291) and acute respiratory failure (ICD-10 J96.01) are the most common procedure and diagnosis codes, appearing 68 and 62 times respectively. This indicates a significant focus on acute care and respiratory conditions, with J96.01 frequently paired with critical care billing.

4. **Case Complexity:** Complexity is primarily driven by diagnosis count rather than service volume, with specialized surgical practices averaging 9+ diagnosis codes per claim versus 1-3 for routine cases. Only 5 claims had ≥5 service lines, suggesting most encounters are focused rather than fragmented, though they may involve multiple conditions requiring simultaneous management.

---

## Required Libraries

- `pandas` - Data manipulation and analysis
- `matplotlib` - Data visualization
- `seaborn` - Statistical visualizations
- `numpy` - Numerical operations

See `requirements.txt` for specific versions.

---

## Notes

- **Data Privacy:** All data files contain prospective/sample data and should be handled according to healthcare data guidelines
- **ICD-10 Codes:** Diagnosis codes can be looked up at [icd10data.com](https://www.icd10data.com/)
- **CPT Codes:** Procedure codes follow standard CPT/HCPCS coding conventions
