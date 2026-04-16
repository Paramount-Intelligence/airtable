# Task 1 Solution — Data Cleaning and Categorization

**Submitted by:** Mohammed Ali  
**Date:** March 2026

---

## Airtable Base Setup

### Table: New Hires

The Airtable base was created with a **New Hires** table containing the following fields:

| Field Name | Field Type | Purpose |
|---|---|---|
| Full Name | Single Line Text | Raw employee name input |
| Email | Email | Employee email address |
| Department | Single Select | Engineering, Marketing, HR, Sales, Finance, Operations |
| Role | Single Line Text | Job title |
| Start Date | Date | Official start date |
| Salary | Currency | Annual salary |
| Cleaned Name | Formula | Standardized name formatting |
| Email Domain | Formula | Extracted domain from email |
| Seniority Level | Formula | Categorized by role keywords |
| Priority Category | Formula | High Value / Standard / Entry Level |
| Onboarding Status | Single Select | Not Started / In Progress / Completed |
| Days Until Start | Formula | Days remaining until start date |
| Hire Quarter | Formula | Q1/Q2/Q3/Q4 based on start date |

---

## Formula Implementations

### 1. Cleaned Name Formula
Standardizes inconsistent text capitalization:

```
UPPER(LEFT(TRIM({Full Name}), 1)) & LOWER(MID(TRIM({Full Name}), 2, LEN(TRIM({Full Name})) - 1))
```

### 2. Email Domain Formula
Extracts company domain for validation:

```
MID({Email}, FIND("@", {Email}) + 1, LEN({Email}) - FIND("@", {Email}))
```

### 3. Seniority Level Formula
Categorizes employees by role keywords:

```
IF(
  OR(
    FIND("Senior", {Role}),
    FIND("Lead", {Role}),
    FIND("Principal", {Role}),
    FIND("Director", {Role}),
    FIND("Head", {Role})
  ),
  "Senior",
  IF(
    OR(
      FIND("Junior", {Role}),
      FIND("Intern", {Role}),
      FIND("Associate", {Role})
    ),
    "Entry Level",
    "Mid Level"
  )
)
```

### 4. Priority Category Formula (High Value Detection)
Identifies high-value hires based on salary and seniority:

```
IF(
  OR(
    {Salary} >= 100000,
    {Seniority Level} = "Senior",
    FIND("Director", {Role}),
    FIND("Manager", {Role})
  ),
  "High Value",
  IF(
    {Salary} >= 60000,
    "Standard",
    "Entry Level"
  )
)
```

### 5. Days Until Start Formula
Calculates urgency of onboarding:

```
DATETIME_DIFF({Start Date}, TODAY(), 'days')
```

### 6. Hire Quarter Formula
Groups hires by fiscal quarter:

```
IF(
  MONTH({Start Date}) <= 3, "Q1",
  IF(
    MONTH({Start Date}) <= 6, "Q2",
    IF(
      MONTH({Start Date}) <= 9, "Q3",
      "Q4"
    )
  )
)
```

---

## Sample Data

| Full Name | Role | Salary | Priority Category | Seniority |
|---|---|---|---|---|
| alice johnson | Senior Software Engineer | 130,000 | High Value | Senior |
| BOB SMITH | Marketing Intern | 35,000 | Entry Level | Entry Level |
| Carol White | Product Manager | 95,000 | Standard | Mid Level |
| david brown | Director of Engineering | 160,000 | High Value | Senior |

---

## Views Created

1. **All Hires** — Default grid view with all fields
2. **High Value Hires** — Filtered to show only Priority Category = "High Value"
3. **Starting This Month** — Filtered to Days Until Start between 0 and 30
4. **By Department** — Grouped by Department field
5. **Onboarding Pipeline** — Grouped by Onboarding Status

---

## Key Outcomes

- Raw text inputs are automatically cleaned and standardized via formulas
- Employees are categorized into Priority tiers without manual assessment
- Seniority detection runs automatically based on role keywords
- HR team can filter and sort by any field for actionable insights
- Days Until Start field creates natural urgency for upcoming hires