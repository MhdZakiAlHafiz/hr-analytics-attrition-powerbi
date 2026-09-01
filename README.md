# HR Analytics & Employee Attrition Dashboard (Power BI)

## Overview
This repository contains an end-to-end **HR Analytics Dashboard** built using **Microsoft Power BI**. The project focuses on diagnosing workforce attrition patterns, evaluating employee engagement levels, and visualizing demographic distributions across 1,417 employee records. The interactive dashboard translates transactional HR data into actionable workforce management strategies.

---

## Business Objectives
The primary purpose of this dashboard is to assist Human Resources and organizational leadership in identifying risk factors driving employee turnover. Key business questions answered include:

1. **Overall Workforce Health:** What are the company's total headcount, active workforce, and overall attrition rate?
2. **Departmental Vulnerability:** Which departments experience the highest volume and percentage of employee turnover?
3. **Compensation Impact:** How does employee attrition distribute across different salary brackets (`LPA`)?
4. **Role & Satisfaction Drivers:** Which job roles suffer the highest attrition, and how does job satisfaction correlate with resignations?
5. **Tenure & Risk Window:** At what career/experience stage are employees most likely to leave the organization?
6. **Demographic Balance:** What are the age group and gender distributions among exiting employees?

---

## Dataset Overview
* **Dataset Size:** 1,417 unique employee records (after ETL deduplication)
* **Scope:** Employee demographics, organizational roles, compensation tiers, and engagement metrics
* **Key Dimensions:** `Department`, `JobRole`, `JobSatisfaction`, `AgeGroup`, `Gender`, `SalarySlab`, `BusinessTravel`
* **Key Numeric Metrics:** `TotalEmployees`, `ActiveEmployees`, `AttritionCount`, `AttritionRate%`, `Age`, `TotalExperience(Years)`, `MonthlyIncome`

---

## Tools & Technologies
* **Business Intelligence:** Microsoft Power BI Desktop
* **Data Transformation:** Power Query (ETL, deduplication, string cleanup, type detection)
* **Calculations:** DAX (Data Analysis Expressions) & Conditional Columns
* **Data Visualization:** KPI Scorecards, Donut Charts, Clustered Bar Charts, Heatmap Matrix, Area Charts, Funnel Charts, Tile Slicers

---

## Data Preparation & ETL (Power Query)
Before visual development, data preprocessing was performed in Power Query:
1. **Null & Blank Handling:** Audited column quality to detect empty records and removed incomplete/blank rows.
2. **Deduplication:** Performed full-table deduplication across all columns (removing 16 duplicate records).
3. **Standardization:** Fixed categorical string inconsistencies using *Find and Replace* (e.g., standardizing `travel_rarely` to `travel rarely`).
4. **Data Type Correction:** Checked and converted numeric fields (`Age`, `Experience`, `Income`) from text to appropriate whole/decimal number types.
5. **Conditional Logic:** Built the `AttritionCount` column via Power Query conditional logic (`IF Attrition = "Yes" THEN 1 ELSE 0`).

---

## DAX Measures & Metric Calculations

| Measure | Formula / Logic | Business Purpose |
| :--- | :--- | :--- |
| **Total Employees** | `COUNT(EmployeeID)` | Total headcount evaluated in the dataset (1,417). |
| **Active Employees** | `COUNTROWS(FILTER(Table, Attrition = "No"))` | Current retained workforce (1,186). |
| **Attrition Count** | `SUM(AttritionCount)` | Total number of employees who have left (231). |
| **Attrition Rate %** | `DIVIDE(SUM(AttritionCount), COUNT(EmployeeID), 0)` | Overall turnover percentage formatted as % (16.3%). |
| **Average Age** | `AVERAGE(Age)` | Mean workforce age (36.94 years). |
| **Average Experience**| `AVERAGE(YearsAtCompany)` / `AVERAGE(TotalExperience)` | Mean tenure/experience across the workforce (7.04 years). |

---

## Dashboard Features & Visualizations

| Visual Feature | Visual Type | Key Metric / Dimension | Business Insight |
| :--- | :--- | :--- | :--- |
| **Executive KPI Summary** | Card Scorecards | Total Headcount, Active Staff, Attrition Count, Attrition Rate %, Avg Age, Avg Experience | High-level operational health snapshot. |
| **Attrition by Department** | Donut Chart | `Department`, `AttritionCount` | Identifies department-level turnover share (*Administration* leads at 36%, followed by *Sales* at 23%). |
| **Attrition by Salary Slab** | Clustered Bar Chart | `SalarySlab`, `Attrition (Yes/No)` | Evaluates turnover across income brackets (*6–10 LPA* has the highest absolute turnover). |
| **Job Role & Satisfaction** | Matrix (Heatmap) | `JobRole`, `JobSatisfaction (1–4)`, `AttritionCount` | Highlights turnover hotspots (*Laboratory Technicians* and *Sales Executives* show highest exits). |
| **Age Group Distribution** | Column Chart | `AgeGroup`, `EmployeeCount` | Visualizes workforce demographic structure (predominantly *26–35* and *36–45* cohorts). |
| **Attrition by Gender** | Pie Chart | `Gender`, `AttritionCount` | Shows gender distribution among departed employees (63.2% Male, 36.8% Female). |
| **Attrition by Experience** | Area Chart | `TotalExperience(Years)`, `AttritionCount` | Uncovers the critical risk window (highest attrition occurs in Year 1). |
| **Department Headcount** | Funnel Chart | `Department`, `EmployeeCount` | Displays organizational workforce weight (*Operations* and *Administration* hold the largest headcount). |
| **Interactive Slicers** | Tile Slicers | `Department`, `AgeGroup` | Allows dynamic multi-dimensional filtering across all report elements. |

---

## Key Business Insights
* **Overall Turnover Baseline:** The organization maintains an overall attrition rate of **16.3%** (231 exits out of 1,417 total employees).
* **Department Concentration:** *Administration* (84 exits / 36%) and *Sales* (52 exits / 23%) account for **nearly 60% of all organizational turnover**.
* **Critical Early-Tenure Risk:** Attrition peaks sharply at **Year 1 of total experience (40 exits)**, indicating potential onboarding bottlenecks or early expectations misalignment.
* **High-Risk Roles:** *Laboratory Technicians* (59 exits) and *Sales Executives* (56 exits) demonstrate the highest attrition across job functions.
* **Demographic Core:** The majority of the workforce belongs to the **26–35 age group (588 employees)**, representing the primary operational base.

---

## Strategic HR Recommendations
1. **First-Year Onboarding & Mentorship:** Address the Year 1 attrition spike by revamping 30-60-90 day onboarding check-ins, structured mentorship, and early career path clarity.
2. **Targeted Retention in Administration & Sales:** Conduct exit interviews and compensation benchmarking specifically for *Administration* and *Sales* departments to identify root causes behind their combined 59% turnover contribution.
3. **Role-Specific Engagement for Technicians & Executives:** Implement workload balancing, skill-upgrading paths, and retention bonuses for *Laboratory Technicians* and *Sales Executives*.
4. **Compensation Tier Review:** Re-evaluate incentives in the 6–10 LPA bracket to ensure competitive retention against market standards.

---

## Dashboard Preview

![HR Analytics Dashboard](images/hr_dashboard.png)

---

## Project Repository Structure
```text
hr-analytics-attrition-powerbi/
│
├── README.md
├── data/
│   └── HR_Employee_Data.csv
├── dashboard/
│   └── HR_Analytics_Dashboard.pbix
└── images/
    └── hr_dashboard.png
