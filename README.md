# Bam in Gilead Hopsital - Patient Data Analysis uisng SQL 
> Bam in Gilead Hospital is a healthcare center that serves patients across different regions. The hospital collects data on patient visits, diagnoses, medications, cholesterol levels, and demographics.
This mini project uses real patient data to demonstrate how **SQL can be used** to analyze healthcare information, answer real-world questions, and extract meaningful insights from structured data.

---

## ⚙️ Project Type Flags
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

**Context:** Bam in Gilead Hospital is a healthcare centre that serves patients across different regions of Nigeria. The hospital collects data on patient visits, diagnoses, medications, cholesterol levels, blood pressure, and demographics.

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

1. **The average patient age is 41 years** - indicating the hospital primarily serves a middle-aged adult population, which may influence the types of conditions and treatments most in demand.

2. **27 patients were diagnosed with hypertension** - making it one of the most common diagnoses in the dataset, suggesting a significant portion of the patient population has cardiovascular health concerns.

3. **The North region has the highest number of patients** - indicating either a larger population base, greater healthcare awareness, or stronger hospital accessibility in that region compared to others.

4. **The average cholesterol level for diabetic patients is 203 mg/dL** - this is borderline high, suggesting diabetic patients at this hospital may also be at elevated risk for cardiovascular complications.

5. **Tamiflu is the most prescribed medication** - suggesting respiratory and flu-related conditions are common among the patient population, particularly given the dataset also includes Flu as a diagnosis.

6. **May and August recorded the highest patient visits (11 each), while November had the lowest (3)** - indicating clear seasonal patterns in hospital attendance that could inform staffing and resource planning.

7. **Gender distribution is nearly equal - Male 52, Female 48** - showing the hospital serves both genders almost equally with a slight male majority.
---

## 9. Recommendations

| Priority | Recommendation | Based On | Suggested Owner |
|----------|---------------|----------|-----------------|
| High | Develop a dedicated hypertension management programme including regular screening and follow-up appointments for at-risk patients | Insight 2 - 27 patients diagnosed with hypertension, one of the most common conditions | Clinical / Medical team |
| High | Increase staffing and medical supplies in May and August to meet peak patient demand | Insight 6 - May and August recorded the highest visits at 11 patients each | Hospital Operations team |
| Medium | Introduce cholesterol monitoring and dietary counselling for all diabetic patients given their average cholesterol of 203 mg/dL | Insight 4 - Diabetic patients show borderline high cholesterol levels | Nutrition / Clinical team |
| Medium | Investigate why the North region has the highest patient count - whether it reflects population size, referral patterns, or lack of alternative healthcare facilities | Insight 3 - North region has the highest patient concentration | Hospital Management |
| Low | Review November staffing levels downward to manage costs during the lowest attendance period of the year | Insight 6 - November recorded only 3 patient visits | Hospital Operations team |

---

## 10. Deliverables

| Deliverable | Description | Location |
|-------------|-------------|----------|
| SQL Query File | All 8 queries written and executed in MySQL Workbench | queries/final/gilead_hospital_queries.sql |
| Summary Report | Written Word document summarizing findings and insights | reports/Gilead_Hospital_Patient_Analysis_Report.docx |
| Raw Dataset | Original patient dataset file | data/raw/ |
| Query Screenshots | Selected screenshots of query results from MySQL Workbench | visuals/ |

---

## 11. Author

*Vivian Okwara*
Data Analyst | Lagos, Nigeria

- 🔗 [LinkedIn](https://linkedin.com/in/okwara-vivian)
- 🌐 [Portfolio](https://Vivian-Portfolio.github.io)
- 📧 okwaravivian26@gmail.com

---

Last updated: June 2026


