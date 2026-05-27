# HR Analytics — Employee Attrition Dashboard
### Built with Power BI | DAX | Star Schema | Row-Level Security

>Most companies know their attrition rate. Very few know why people are leaving, which teams are most at risk right now, and what a department head can actually do about it — without needing to ask HR for a custom report every time.
This dashboard changes that. It takes 1,470 employee records, builds a clean data model behind the scenes, and surfaces the answers that matter: Sales Representatives are leaving at nearly 40%. Employees on overtime are three times more likely to quit than those who are not. Leavers earn less than stayers on average. And every department head gets their own secure view of their team's data — without seeing anyone else's.


## Business Problem

A company with 1,470 employees is experiencing a **16.12% attrition rate** — significantly above the industry benchmark of 10%. HR leadership needs to understand:

- **Which departments and job roles** have the highest attrition?
- **What factors** — income, overtime, satisfaction, tenure — drive employees to leave?
- **How can department heads** monitor their own team's attrition without seeing other departments' data?

This dashboard answers all three questions through interactive visuals, statistical measures, and role-based data security.

---

## Dashboard Preview

### Page 1 — Executive Summary


![Page 1 Executive Summary](c:\Users\HP\Downloads\Executive summary.png)

### Page 2 — Department Deep-Dive


![Page 2 Deep Dive](c:\Users\HP\Downloads\Department deep dive.png)

---

## Key Findings

| Insight | Finding | Business Impact |
|---|---|---|
| **Highest attrition role** | Sales Representatives — 39.76% | 4 in 10 Sales Reps leave — urgent retention action needed |
| **Overtime effect** | OT workers attrite at ~30% vs ~10% non-OT | Overwork is the single strongest attrition driver |
| **Highest risk dept** | Sales — 20.63% attrition rate | Sales pipeline continuity at risk |
| **Income gap** | Leavers earned less than stayers on average | Compensation benchmarking review recommended |
| **Lowest risk dept** | R&D — 13.84% attrition rate | Retention strategies here are working |

---

## Technical Features

### Data Model — Star Schema
```
DimDepartment ←── FactEmployee ──→ DimJobRole
                        ↓
                  DimEducation
```
- **FactEmployee** — 1,470 rows, 32 columns (3 constant columns removed)
- **DimDepartment** — 3 rows (Human Resources, Research & Development, Sales)
- **DimJobRole** — 9 rows (all unique job roles)
- **DimEducation** — 6 rows (all education fields)
- Relationships built on natural text keys — no surrogate IDs needed

### DAX Measures (20 measures across 7 categories)

| Category | Measures |
|---|---|
| Headcount | Total Employees, Active Employees, Attrited Employees |
| Attrition | Attrition Rate, Attrition Rate by Dept, Overtime Attrition Rate, Attrition Status |
| Compensation | Avg Monthly Income, Avg Monthly Income (Attrited), Income Gap |
| Satisfaction | Avg Job Satisfaction, Avg Job Satisfaction (Attrited), % Overtime Workers |
| Ranking | Department Attrition Rank, Job Role Attrition Rank |
| Dynamic titles | Selected Department Title, KPI Summary Line |
| Conditional | Attrition Status (High/Moderate/Low Risk) |

**Sample DAX — Overtime Attrition Rate:**
```dax
Overtime Attrition Rate =
CALCULATE(
    [Attrition Rate],
    FactEmployee[OverTime] = "Yes"
)
```

**Sample DAX — Dynamic Dashboard Title:**
```dax
Selected Department Title =
VAR SelectedDept =
    SELECTEDVALUE( DimDepartment[Department], "All Departments" )
RETURN
    "Attrition Analysis — " & SelectedDept
```

### Row-Level Security (RLS)
4 roles configured to restrict data access by department:

| Role | Access | DAX Filter |
|---|---|---|
| HR Manager | All departments | None (unrestricted) |
| Department Head HR | HR data only | `[Department] = "Human Resources"` |
| Department Head R&D | R&D data only | `[Department] = "Research & Development"` |
| Department Head Sales | Sales data only | `[Department] = "Sales"` |

### Dashboard Pages

**Page 1 — Executive Summary**
- 4 KPI cards: Total Employees, Active Employees, Attrited Employees, Avg Monthly Income
- Bar chart: Attrition rate by Department
- Donut chart: Attrition by Gender
- 3 interactive slicers: Department, Gender, OverTime
- Dynamic page title (updates with slicer selection)
- KPI summary text line (live employee/attrition count)

**Page 2 — Department Deep-Dive**
- Matrix: Department × Job Role → Attrition Rate (conditional red/amber formatting)
- Bar chart: Attrition rate by OverTime (Yes vs No)
- Table: Department Attrition Rank (RANKX measure)
- Scatter plot: Avg Monthly Income vs Attrition Rate by Job Role

---

## Dataset

- **Source:** [IBM HR Analytics Employee Attrition — Kaggle](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset)
- **Size:** 1,470 employees × 35 columns
- **Columns removed:** EmployeeCount, Over18, StandardHours (zero variance — constant values)

---

## Tools Used

| Tool | Purpose |
|---|---|
| Power BI Desktop | Dashboard development, DAX measures, RLS |
| Power Query | Star schema creation, data cleaning |
| DAX | 20 custom measures across 7 categories |
| Row-Level Security | Department-level data access control |

---

## How to Open

1. Download the `.pbix` file from this repository
2. Open with **Power BI Desktop** (free download from Microsoft)
3. The dashboard opens with all measures, relationships, and RLS pre-configured
4. To test RLS: Modeling tab → View as → select a role

---

## Project Structure

```
hr-analytics-powerbi/
├── HR_Analytics_Dashboard.pbix    ← Main Power BI file
├── HR-Employee-Attrition.csv      ← Source dataset
├── README.md                      ← This file
└── images/
    ├── page1_executive_summary.png
    ├── page2_department_deepdive.png
    └── data_model.png
```

---

## Skills Demonstrated

- ✅ Star schema data modelling in Power Query
- ✅ Advanced DAX — CALCULATE, DIVIDE, RANKX, ALLEXCEPT, VAR...RETURN, SELECTEDVALUE
- ✅ Row-Level Security — 4 roles with department-level filters
- ✅ Dynamic titles and KPI summary text using DAX string measures
- ✅ Conditional formatting — colour-coded attrition risk (High/Moderate/Low)
- ✅ Cross-filtering with slicers across all visuals
- ✅ Business insight storytelling — findings translated to actionable recommendations

---

## Author

**Harshavardhan Gurav**
- 📧 Email: harshavardhangurav839@gmail.com
- 💼 LinkedIn: [harshavardhan-gurav](https://www.linkedin.com/in/harshavardhan-gurav-3284601a2/#:~:text=www.linkedin.com/in/harshavardhan%2Dgurav%2D3284601a2)
