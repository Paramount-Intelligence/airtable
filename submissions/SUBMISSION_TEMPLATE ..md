# Candidate Submission Template

## Candidate Information

- **Full Name:** Dileep Singh
- **Email:** baghirajput2326@gmail.com
- **LinkedIn or Portfolio:** Available on request
- **Submission Date:** 2026-03-13

---

## Task 1: Intermediate Airtable Skills

### 1. Full Name Formula

```
TRIM({First Name}) & " " & TRIM({Last Name})
```

Concatenates First Name and Last Name with a space. `TRIM()` applied to both fields removes accidental leading/trailing whitespace before joining.

---

### 2. Cleaned Email Formula

```
LOWER(TRIM(SUBSTITUTE(SUBSTITUTE({Email Input}, " ", ""), ",", "")))
```

Removes internal spaces and commas from the email, trims whitespace, and converts to lowercase. Handles the most common data entry inconsistencies in free-text email fields.

---

### 3. Status Categorization Formula

```
IF(
  {Amount Spent on Equipment} > 1000,
  "High Value",
  IF(
    AND({Amount Spent on Equipment} >= 500, {Amount Spent on Equipment} <= 999),
    "Medium Value",
    "Low Value"
  )
)
```

- Amount > 1000 → **High Value**
- Amount 500–999 → **Medium Value**
- Amount < 500 → **Low Value**

---

### 4. Days Since Created Formula

```
DATETIME_DIFF(TODAY(), {Created Date}, 'days')
```

Calculates days between the Created Date and today. Updates automatically every day — no manual refresh needed.

---

## Task 2: Advanced Airtable Automation

### 1. Automation Steps

**Automation name:** `High Value Hire Alert & Tracker`

**Step 1 — Trigger**
When a record matches a condition: `Status Category` = `High Value` in the New Hires table.

**Step 2 — Conditional Branch: Email Valid?**
Check if `Cleaned Email` is not empty and contains `@`. Routes to two different paths based on result.

**Step 3a — Valid Email path**
Send email notification to hr@company.com with hire's full details (name, email, equipment spend, days since created). Then send Slack message to `#hr-onboarding-alerts` channel.

**Step 3b — Invalid/Missing Email path**
Send HR alert email flagging that the hire has no valid email and action is required to update the record.

**Step 4 — Log to Tracking Table**
Create a new record in the `High Value Tracking` table with: hire name, email, spend amount, alert date, email valid flag, and status set to `Logged`.

---

### 2. Interface Design

**Page 1 — Overview Dashboard**
Three summary count tiles at the top showing High Value, Medium Value, and Low Value hire counts with color coding (red, yellow, green). Full grid of all hires below, sorted by Days Since Created.

**Page 2 — High Value Hires**
Filtered grid showing only High Value hires, sorted by equipment spend descending. Designed for HR to immediately see priority cases.

**Page 3 — New Hire Detail View**
Record detail view triggered by clicking any hire. Shows full name, cleaned email, equipment spend, status category, created date, and days since created.

---

### 3. Formula Logic

Email validation formula used in automation conditional branch:
```
AND(
  {Cleaned Email} != "",
  FIND("@", {Cleaned Email}) > 0
)
```

Status Category formula (from Task 1) is the primary trigger condition — no additional formula needed in the automation itself.

---

### 4. Assumptions

- `Status Category` formula from Task 1 is used directly as the automation trigger condition
- Email validation uses `@` presence as a basic check since Airtable automations do not support regex natively
- `High Value Tracking` is a separate table created manually in the same base before the automation runs
- Slack integration is assumed to be connected in Airtable workspace settings
- Automation triggers on both record creation and record update so late edits to equipment spend are captured
- Interface is shared with HR team via Airtable's built-in share link

---

### 5. Optional Notes

- All formula files and detailed step-by-step documentation are in the `submissions/` folder
- `formulas.md` contains the complete formula reference with examples and a sample data table
- `task1_solution.md` and `task2_solution.md` contain full explanations of each solution
- The automation is designed so HR can confirm receipt using a "Notification Sent" checkbox field in production
