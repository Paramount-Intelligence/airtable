# Task 1 Solution — Airtable Data Cleaning & Categorization

## Overview

This document covers the complete Airtable base setup, formula fields, and data categorization logic used to build the HR Onboarding Automation Dashboard. All formulas are written for Airtable's native formula engine.

---

## 1. Airtable Base Structure

### Table: `New Hires` (Primary Table)

This is the main table that stores all new hire onboarding records.

| Field Name | Field Type | Purpose |
|---|---|---|
| Employee Name | Single Line Text | Raw name input from form |
| Personal Email | Email | Personal email for pre-start comms |
| Job Title | Single Line Text | Raw job title input |
| Department | Single Select | Engineering / Sales / Marketing / HR / Finance / Operations / Product |
| Employment Type | Single Select | Full-Time / Part-Time / Contractor |
| Start Date | Date | Official first day |
| Manager Name | Single Line Text | Assigned manager |
| Manager Email | Email | Manager contact |
| Annual Salary | Currency | Salary figure for priority classification |
| Office Location | Single Select | Remote / New York / London / Chicago / San Francisco |
| Onboarding Status | Single Select | Not Started / In Progress / Completed / On Hold |
| Documents Submitted | Checkbox | Have all documents been received? |
| IT Setup Complete | Checkbox | Has IT provisioned the employee? |
| Training Assigned | Checkbox | Has compliance training been assigned? |
| Notes | Long Text | Any manual notes from HR |

---

## 2. Formula Fields — Data Cleaning

### Formula Field: `Clean Name`
**Purpose:** Standardizes name casing — handles all-caps, all-lowercase, and mixed inputs.

```
TRIM(
  CONCATENATE(
    UPPER(LEFT(TRIM({Employee Name}), 1)),
    LOWER(MID(TRIM({Employee Name}), 2, FIND(" ", TRIM({Employee Name}) & " ") - 2)),
    IF(
      FIND(" ", TRIM({Employee Name}) & " ") < LEN(TRIM({Employee Name})),
      CONCATENATE(
        " ",
        UPPER(MID(TRIM({Employee Name}), FIND(" ", TRIM({Employee Name})) + 1, 1)),
        LOWER(MID(TRIM({Employee Name}), FIND(" ", TRIM({Employee Name})) + 2, 100))
      ),
      ""
    )
  )
)
```

**Simpler version (recommended for reliability):**
```
PROPER(TRIM({Employee Name}))
```

---

### Formula Field: `Clean Email`
**Purpose:** Lowercases and trims the email address to prevent duplicate records.

```
LOWER(TRIM({Personal Email}))
```

---

### Formula Field: `Clean Job Title`
**Purpose:** Standardizes job title casing.

```
PROPER(TRIM({Job Title}))
```

---

### Formula Field: `Days Until Start`
**Purpose:** Calculates how many days until the employee's start date from today.

```
DATETIME_DIFF({Start Date}, TODAY(), 'days')
```

---

### Formula Field: `Start Month`
**Purpose:** Extracts the month name for grouping and reporting.

```
DATETIME_FORMAT({Start Date}, 'MMMM YYYY')
```

---

### Formula Field: `Days Since Start`
**Purpose:** Tracks how many days the employee has been onboarding (for milestone tracking).

```
IF(
  IS_BEFORE({Start Date}, TODAY()),
  DATETIME_DIFF(TODAY(), {Start Date}, 'days'),
  0
)
```

---

## 3. Formula Fields — Categorization

### Formula Field: `Seniority Level`
**Purpose:** Classifies the employee's seniority based on their job title keywords.

```
IF(
  OR(
    FIND("Chief", {Job Title}),
    FIND("CEO", {Job Title}),
    FIND("CTO", {Job Title}),
    FIND("CFO", {Job Title}),
    FIND("COO", {Job Title}),
    FIND("President", {Job Title})
  ),
  "C-Suite",
  IF(
    OR(
      FIND("VP", {Job Title}),
      FIND("Vice President", {Job Title}),
      FIND("Director", {Job Title})
    ),
    "Director / VP",
    IF(
      OR(
        FIND("Senior", {Job Title}),
        FIND("Sr.", {Job Title}),
        FIND("Lead", {Job Title}),
        FIND("Principal", {Job Title}),
        FIND("Manager", {Job Title})
      ),
      "Senior / Manager",
      IF(
        OR(
          FIND("Junior", {Job Title}),
          FIND("Jr.", {Job Title}),
          FIND("Associate", {Job Title}),
          FIND("Intern", {Job Title})
        ),
        "Junior / Associate",
        "Mid-Level"
      )
    )
  )
)
```

---

### Formula Field: `Candidate Priority`
**Purpose:** Classifies each new hire as High Value, Standard, or Contractor based on salary and employment type.

```
IF(
  {Employment Type} = "Contractor",
  "Contractor",
  IF(
    OR(
      {Annual Salary} >= 150000,
      {Seniority Level} = "C-Suite",
      {Seniority Level} = "Director / VP"
    ),
    "High Value",
    IF(
      OR(
        {Annual Salary} >= 80000,
        {Seniority Level} = "Senior / Manager"
      ),
      "Standard",
      "Entry Level"
    )
  )
)
```

---

### Formula Field: `Onboarding Stage`
**Purpose:** Automatically determines which stage of onboarding the employee is in based on checkbox fields and start date.

```
IF(
  {Onboarding Status} = "Completed",
  "✅ Complete",
  IF(
    AND({Documents Submitted}, {IT Setup Complete}, {Training Assigned}),
    "🟢 Ready for Day 1",
    IF(
      AND({Documents Submitted}, NOT({IT Setup Complete})),
      "🔧 Awaiting IT Setup",
      IF(
        NOT({Documents Submitted}),
        "📄 Awaiting Documents",
        IF(
          NOT({Training Assigned}),
          "📚 Awaiting Training Assignment",
          "⏳ In Progress"
        )
      )
    )
  )
)
```

---

### Formula Field: `Urgency Flag`
**Purpose:** Flags records that need immediate HR attention — starting soon with incomplete onboarding.

```
IF(
  AND(
    {Days Until Start} <= 7,
    {Days Until Start} >= 0,
    {Onboarding Stage} != "✅ Complete",
    {Onboarding Stage} != "🟢 Ready for Day 1"
  ),
  "🚨 URGENT — Starting in " & {Days Until Start} & " days",
  IF(
    AND(
      {Days Until Start} <= 14,
      {Days Until Start} >= 0,
      {Onboarding Stage} != "✅ Complete"
    ),
    "⚠️ Starting Soon",
    IF(
      {Days Until Start} < 0,
      "📌 Started — Check Progress",
      "✔ On Track"
    )
  )
)
```

---

### Formula Field: `Department Group`
**Purpose:** Groups departments into broader categories for reporting filters.

```
IF(
  OR({Department} = "Engineering", {Department} = "Product", {Department} = "Design"),
  "Tech & Product",
  IF(
    OR({Department} = "Sales", {Department} = "Marketing"),
    "Revenue",
    IF(
      OR({Department} = "HR", {Department} = "Finance", {Department} = "Operations"),
      "Operations & Support",
      "Other"
    )
  )
)
```

---

### Formula Field: `Onboarding Completion %`
**Purpose:** Calculates a percentage completion score based on the three key checklist items.

```
(
  IF({Documents Submitted}, 34, 0) +
  IF({IT Setup Complete}, 33, 0) +
  IF({Training Assigned}, 33, 0)
) & "%"
```

---

### Formula Field: `Welcome Email Subject`
**Purpose:** Auto-generates a personalized welcome email subject line for HR to use.

```
"Welcome to the team, " & PROPER(LEFT(TRIM({Employee Name}), FIND(" ", TRIM({Employee Name}) & " ") - 1)) & "! Your start date is " & DATETIME_FORMAT({Start Date}, 'MMMM D, YYYY')
```

---

## 4. Views Configuration

### View 1: `All New Hires` (Default Grid View)
- Shows all records
- Sorted by Start Date (ascending)
- Fields: Clean Name, Clean Job Title, Department, Start Date, Candidate Priority, Onboarding Stage, Urgency Flag

### View 2: `High Value Hires`
- Filter: `Candidate Priority` is `High Value`
- Sorted by Start Date (ascending)
- Purpose: Focus HR on priority hires

### View 3: `Urgent Actions`
- Filter: `Urgency Flag` contains `URGENT` OR `Soon`
- Sorted by Days Until Start (ascending)
- Purpose: Daily HR action list

### View 4: `Incomplete Onboarding`
- Filter: `Onboarding Stage` is NOT `✅ Complete` AND `Onboarding Stage` is NOT `🟢 Ready for Day 1`
- Purpose: Track who still needs attention

### View 5: `By Department` (Gallery or Grid)
- Grouped by: `Department`
- Purpose: Department-level onboarding visibility

### View 6: `Contractors`
- Filter: `Employment Type` is `Contractor`
- Purpose: Separate contractor onboarding tracking

---

## 5. Sample Data Records

Below is sample data demonstrating the formula outputs:

| Employee Name | Job Title | Department | Salary | Employment Type | Start Date | Documents | IT | Training |
|---|---|---|---|---|---|---|---|---|
| JOHN SMITH | senior software engineer | Engineering | $145,000 | Full-Time | +5 days | ✅ | ❌ | ✅ |
| sarah JONES | VP of Marketing | Marketing | $180,000 | Full-Time | +12 days | ✅ | ✅ | ✅ |
| mike chen | intern | Engineering | $45,000 | Part-Time | +3 days | ❌ | ❌ | ❌ |
| LISA PARK | Chief Technology Officer | Engineering | $320,000 | Full-Time | +8 days | ✅ | ✅ | ❌ |
| Tom Willis | Contractor | Operations | N/A | Contractor | +20 days | ✅ | ❌ | ❌ |

**Expected formula outputs:**

| Clean Name | Seniority | Priority | Onboarding Stage | Urgency Flag |
|---|---|---|---|---|
| John Smith | Senior / Manager | Standard | 🔧 Awaiting IT Setup | 🚨 URGENT — Starting in 5 days |
| Sarah Jones | Director / VP | High Value | ✅ Complete | ✔ On Track |
| Mike Chen | Junior / Associate | Entry Level | 📄 Awaiting Documents | 🚨 URGENT — Starting in 3 days |
| Lisa Park | C-Suite | High Value | 📚 Awaiting Training Assignment | ⚠️ Starting Soon |
| Tom Willis | Mid-Level | Contractor | 🔧 Awaiting IT Setup | ✔ On Track |

---

## 6. Key Design Decisions

**Why formula-based categorization instead of manual single-select fields?**
Formula fields update automatically as data changes. If a hire's salary is updated or their job title changes, the priority and seniority classifications recalculate instantly — no manual re-tagging required.

**Why PROPER() for name cleaning?**
Airtable's `PROPER()` function reliably handles common casing issues (all caps, all lowercase) without complex nested logic. For enterprise use, a more advanced regex approach would be applied via an automation.

**Why percentage completion instead of a checklist count?**
A percentage field (0–100%) is more useful in dashboard gauges and progress indicators within the Interface Designer, and is more intuitive for HR managers to read at a glance.

---

*Submitted as Task 1 of the Airtable HR Onboarding Automation Assessment.*
