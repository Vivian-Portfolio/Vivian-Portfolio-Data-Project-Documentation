# Bam in Gilead Hopsital - Patient Data Analysis uisng SQL 
> Bam in Gilead Hospital is a healthcare center that serves patients across different regions. The hospital collects data on patient visits, diagnoses, medications, cholesterol levels, and demographics.
This mini project uses real patient data to demonstrate how **SQL can be used** to analyze healthcare information, answer real-world questions, and extract meaningful insights from structured data.

---

## ⚙️ Project Type Flags
> *Check what applies. This helps reviewers and collaborators understand the nature of the work at a glance. Delete this block before publishing.*

- [ ] Exploratory Data Analysis (EDA)
- [x] SQL Analysis / Querying
- [ ] Dashboard / Data Visualization
- [ ] Data Pipeline / ETL
- [ ] Predictive Modelling / Machine Learning
- [x] Data Cleaning / Wrangling
- [ ] End-to-End (multiple of the above)
- [ ] Other: ___________

---

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Project Scope & Tools](#3-project-scope--tools)
4. [Repository Structure](#4-repository-structure)
5. [Data Workflow](#5-data-workflow)
6. [Data Model & Schema](#6-data-model--schema)
7. [SQL Analysis & Queries](#7-SQL-Analysis--&-Queries)
8. [Key Insights](#8-key-insights)
9. [Recommendations](#9-recommendations)
10. [Deliverables](#10-deliverables)
11. [Author](#11-author)

---

## 1. Project Overview

**Context:**Bam in Gilead Hospital is a healthcare centre that serves patients across different regions of Nigeria. The hospital collects data on patient visits, diagnoses, medications, cholesterol levels, blood pressure, and demographics.

**Problem Statement:**  The hospital had patient records stored in a database but no structured analysis to answer key operational and clinical questions - such as which regions have the most patients, what conditions are most common, and which medications are most prescribed.

**Approach:** Used SQL in MySQL Workbench to query the patient database, writing structured queries using SELECT, WHERE, GROUP BY, ORDER BY, aggregate functions (AVG, COUNT), date functions (STR_TO_DATE, MONTH, MONTHNAME), and DML statements (UPDATE) to answer seven key business questions about the patient population.

**Outcome:**  Successfully extracted meaningful insights from the patient dataset, revealing that the average patient age is 41, 27 patients were diagnosed with hypertension, the North region has the highest patient count, the average cholesterol level for diabetic patients is 203 mg/dL, Tamiflu is the most prescribed medication, and patient visits vary significantly by month.

## Key Questions Answered
- What is the average age of patients?
- How many patients have been diagnosed with hypertension?
- Which region has the highest number of patients?
- What is the average cholesterol level for patients with diabetes?
- Which medication is prescribed most often?
- How many patients visited the hospital in each month of the year?
- What is the distribution of patients by gender?

---

## 2. Objectives

- **Primary Objective:** Write and execute SQL queries in MySQL Workbench to analyze a hospital patient dataset and extract meaningful clinical and operational insights.
- **Secondary Objective 1:** Identify patient demographic patterns - including age distribution, gender breakdown, and regional distribution.
- **Secondary Objective 2:** Analyze clinical data to determine the most common diagnoses, most prescribed medications, and average cholesterol levels among diabetic patients.
- **Secondary Objective 3:** Examine patient visit patterns across months to identify peak and low attendance periods.
- **Secondary Objective 4:** Demonstrate practical SQL skills including aggregate functions, date functions, filtering, grouping, sorting, and data updates.

> 💡 Every query in this project traces back to one of these objectives.

---

## 3. Project Scope & Tools

### Scope

| Dimension | Details |
|------------|---------|
| **In Scope** | Patient-level records including demographics, diagnoses, medications, cholesterol levels, blood pressure, visit dates, and regional data |
| **Out of Scope** | Hospital financial data, staff records, and treatment outcomes - these were not available in the dataset |
| **Time Period** | Patient visit records across multiple months within the dataset period |
| **Granularity** | Row-level patient data (one row per patient record) |

### Tools & Technologies

| Category | Tool(s) Used |
|----------|--------------|
| Database Management | MySQL |
| Query Writing & Execution | MySQL Workbench |
| Data Querying | SQL (SELECT, WHERE, GROUP BY, ORDER BY) |
| Aggregate Functions | AVG, COUNT |
| Date Functions | STR_TO_DATE, MONTH, MONTHNAME |
| Data Manipulation | UPDATE (with safe update mode) |
| Documentation | Microsoft Word, GitHub |

---

## 4. Repository Structure

```
Vivian-Portfolio-Bam-in-Gilead-Hospital-Analysis/
|
├── data/
|   └── raw/              # Original, unmodified patient dataset
|
├── docs/                 # Data dictionary and project notes
|
├── queries/
|   ├── exploratory/      # Initial investigative queries
|   └── final/            # Final production-ready queries
|
├── reports/              # Written summary report
|
├── visuals/              # Screenshots of query results
|
├── README.md             # You are here
└── project_metadata.yml  # Project metadata

``` 
---

## 5. Data Workflow

1. **Source:** One patient table (bam_in_gilead_hospital.patient) containing 100 patient records with demographics, diagnoses, medications, cholesterol levels, blood pressure, visit dates, and regional data.
2. **Ingestion:** Dataset loaded into MySQL Workbench as a structured database table (bam_in_gilead_hospital).
3. **Cleaning:** Identified and corrected a data entry error - Patient ID 99 had an incorrect gender value which was updated using an UPDATE statement with safe update mode disabled temporarily.
4. **Analysis:** Wrote and executed 7 SQL queries covering aggregate analysis, filtering, grouping, sorting, date extraction, and data updates to answer key clinical and operational questions.
5. **Output:** Query results documented in README, SQL script saved as a .sql file, selected screenshots of query outputs saved in the visuals/ folder, and a written summary report saved in the reports/ folder.
---

## 6. Data Model & Schema

The dataset contains 100 patient records from `Bam in Gilead Hospital`.

### Data Dictionary

 Field Name | Data Type | Description | Example Value |
|------------|-----------|-------------|---------------|
| `first_name` | Text | Patient's first name | John |
| `last_name` | Text | Patient's last name | Smith |
| `age` | Integer | Patient age in years | 62 |
| `gender` | Text | Gender (Male/Female) | Male |
| `visit_date` | Date | Date of hospital visit | 22/03/2024 |
| `diagnosis` | Text | Diagnosed medical condition | Diabetes |
| `medication` | Text | Prescribed medication | Metformin |
| `blood_pressure` | Text | Blood pressure reading (e.g. 120/80) | 130/85 |
| `cholesterol_mg_dl` | Integer | Cholesterol level in mg/dL | 190 |
| `region` | Text | Patient's region of residence | East |

> *Row count:* 100 patient records
> *Key table:* bam_in_gilead_hospital.patient
> *Date format:* DD/MM/YYYY (stored as text — converted using STR_TO_DATE in queries)
---

## 7. SQL Analysis & Queries
**Q1: What is the average age of patients visiting Bam in Gilead Hospital?*
```sql
select avg(age) as Averageage
from bam_in_gilead_hospital.patient;
-- The aveeage age of the patients is 41
```
**Q2 How many patients has been diagnosed with hypertention?*
``` sql
select count(*) as Patientcount_Hypertention
from bam_in_gilead_hospital.patient
where diagnosis = 'Hypertension'; 
-- 27 pateints were diagnosed with Hypertension
```
**-- Q3 Which region has the highest number of patients?*
``` sql
select region, count(*) as Patientcount
from bam_in_gilead_hospital.patient
group by region
order by patientcount desc;
-- The north has the hightest number of patients
```
**-- Q4 What is the average cholesterol level for patients with diabetes?*
``` sql
select avg(cholesterol_mg_dl) as AvgCholesterol_diabetics
from bam_in_gilead_hospital.patient
where diagnosis ='Diabetes';
-- The average cholesterol for pateints with diabestes is 203
```
**-- Q5 Which medication is prescribed most often?*
 ``` sql
 select medication,count(*) as Prescription_count
 from bam_in_gilead_hospital.patient
 where medication <> 'None'
 group by medication
 order by 2 desc;
 -- The most prescribed medication is Tamiflu
```
**- Q6 How patients visited the hospital in each month of the year?*
```sql
select month(str_to_date(visit_date, '%d/%m/%Y')) as monthnum,
	monthname(str_to_date(visit_date, '%d/%m/%Y')) as Visit_Month,
    count(*) as Patient_count
from bam_in_gilead_hospital.patient
group by monthnum, Visit_Month
order by monthnum;
-- Result:* Patient visits vary by month as follows:
- January: 6, February: 8, March: 9, April: 10, May: 11, June: 10
- July: 10, August: 11, September: 9, October: 8, November: 3, December: 5

Peak months are May and August (11 patients each). November recorded the lowest visits (3 patients).
```
**-- Q7 What is the distribution of patients gender?*
```sql
set sql_safe_updates = 0;

update bam_in_gilead_hospital.patient
set gender = 'Male'
where patient_id = 99;

select gender, count(*) as patientcount
from bam_in_gilead_hospital.patient
group by gender;
-- *Result:* The distribution of gender is Male 52 and Female 48.
```
![ERD Diagram](visuals/erd.png)
*[Brief caption: e.g., "Three-table schema - orders, customers, and products joined on shared IDs."]*

---

## 8. Key Insights

<!--
  Findings + implications. Not just what happened - what it means.

  WHAT GOOD LOOKS LIKE:
  ✅ "Return rates, not sales volume, explain Region A's underperformance.
      Region A's return rate on home goods was 34% - more than double the
      company average. Revenue was not lost at the point of sale; it was
      lost post-sale through refunds. This points to a fulfilment or
      product quality issue specific to that region, not a demand problem."

  WHAT TO AVOID:
  ❌ "Region A had lower revenue than other regions in Q4."
     (That's an observation. It describes what happened.
      An insight says what it means and where to look next.)

  Aim for 3–6 insights. Quality over quantity.
-->

**Insight 1: [Short descriptive headline]**
[What you found + what it suggests. One short paragraph.]

**Insight 2: [Short descriptive headline]**
[What you found + what it suggests.]

**Insight 3: [Short descriptive headline]**
[What you found + what it suggests.]

**Insight 4 (if applicable): [Short descriptive headline]**
[What you found + what it suggests.]

---

## 10. Recommendations

<!--
  Action-oriented. Addressed to a real audience.
  Tied explicitly to the insight that supports each one.

  WHAT GOOD LOOKS LIKE:
  Priority: High
  Recommendation: "Conduct a fulfilment audit for home goods deliveries
                   in Region A - specifically investigating whether returns
                   correlate with a particular warehouse, carrier, or SKU batch."
  Based On: Insight 1 - return rate anomaly in Region A
  Owner: Operations / Supply Chain team

  WHAT TO AVOID:
  ❌ "Improve the return rate."
     (Not actionable. Doesn't say who, how, or where to start.)
  ❌ "Further analysis is needed."
     (This is a placeholder, not a recommendation.)
-->

| Priority | Recommendation | Based On | Suggested Owner |
|----------|---------------|----------|-----------------|
| High | [Specific, actionable step] | [Insight it comes from] | [Who should act] |
| Medium | [Specific, actionable step] | [Insight it comes from] | [Who should act] |
| Low | [Exploratory or longer-term suggestion] | [Insight it comes from] | [Who should act] |

---

## 11. Assumptions & Limitations

<!--
  WHAT GOOD LOOKS LIKE:
  Assumption: "Transaction records were assumed to be complete for all five regions.
               No validation was performed against source system record counts."
  Limitation: "The analysis cannot distinguish between returns initiated by
               the customer vs. returns initiated by the business (e.g., recalls).
               If business-initiated returns are concentrated in Region A, the
               return rate finding may reflect a policy decision, not a quality issue."

  WHAT TO AVOID:
  ❌ Leaving this section blank or writing "None known."
     Every project has limitations. Documenting them is a sign of
     analytical maturity - not a confession of failure.
-->

### Assumptions
- [What did you treat as true without being able to verify?]
- [What simplifications did you make for scope or feasibility?]
- [What domain rules or definitions did you accept as given?]

### Limitations
- [What gaps exist in the data?]
- [What analysis was out of scope but could affect interpretation?]
- [What would a more rigorous version of this project include?]
- [Are there known biases in the data source or collection method?]

> *The goal here is pre-emptive Q&A. What would a thoughtful skeptic push back on? Document the answer here, before they ask.*

---

## 12. Future Enhancements

<!--
  WHAT GOOD LOOKS LIKE:
  ✅ "Automate the monthly data pull from the POS export folder using
      a scheduled Python script, replacing the current manual process."
  ✅ "Expand the return rate analysis to include carrier-level data,
      which was unavailable in this dataset but exists in the logistics system."

  WHAT TO AVOID:
  ❌ "Add a machine learning model."
     (Vague, and disconnected from the actual findings of this project.)
  ❌ Listing aspirational features that don't follow logically from the work.
-->

- [ ] [Enhancement 1 - specific and traceable to a real gap in this project]
- [ ] [Enhancement 2]
- [ ] [Enhancement 3]
- [ ] [Enhancement 4]

---

## 13. Deliverables

| Deliverable | Description | Location |
|-------------|-------------|----------|
| [Name] | [What it contains] | [`/path/to/file`] |
| [Name] | [What it contains] | [`/path/to/file`] |
| [Name] | [What it contains] | [`/path/to/file`] |

---

## 14. Author

**[Your Name]**
[Your role or title - current or target]

- 🔗 [LinkedIn URL]
- 💼 [Portfolio or GitHub profile URL]
- 📧 [Email - optional]

---

*Last updated: [Month YYYY]*
*If this template helped you, consider starring the repository.*


# [Project Title]
> *One sentence. What did you analyze, build, or solve - and why does it matter?*

---

## ⚙️ Project Type Flags
> *Check what applies. This helps reviewers and collaborators understand the nature of the work at a glance. Delete this block before publishing.*

- [ ] Exploratory Data Analysis (EDA)
- [ ] SQL Analysis / Querying
- [ ] Dashboard / Data Visualization
- [ ] Data Pipeline / ETL
- [ ] Predictive Modelling / Machine Learning
- [ ] Data Cleaning / Wrangling
- [ ] End-to-End (multiple of the above)
- [ ] Other: ___________

---
