# Task 2 — Advanced Airtable Automation & Interface

## 1. Automation Steps

### Overview
The automation triggers whenever a new hire's **Status Categorization** field changes to **"High Value"** and performs three actions: sends an HR notification, logs a tracking record, and handles missing/invalid email edge cases.

---

### Trigger
**Type:** "When a record matches conditions"  
**Table:** New Hires  
**Condition:** `Status Categorization` is `High Value`

> This trigger fires whenever a record is created or updated and the formula evaluates to "High Value" — covering both new records entered above $1,000 and existing records updated to exceed the threshold.

---

### Step 1 — Conditional Branch: Email Validation

**Action Type:** Conditional logic  
**Condition:**
```
AND(
  {Cleaned Email} != "",
  FIND("@", {Cleaned Email}) > 0,
  FIND(".", {Cleaned Email}) > FIND("@", {Cleaned Email})
)
```

This checks:
- Email is not blank
- Contains an `@` symbol
- Contains a `.` after the `@` (basic format validation)

**Branch A — Valid Email** → Proceed to Step 2  
**Branch B — Invalid/Missing Email** → Proceed to Step 3

---

### Step 2 (Branch A) — Send Email Notification to HR

**Action Type:** Send an email  
**To:** hr@company.com  
**Subject:**
```
🔔 High Value New Hire: {Full Name}
```
**Body:**
```
A new hire has been flagged as High Value.

Name:       {Full Name}
Email:      {Cleaned Email}
Equipment:  ${Amount Spent on Equipment}
Created:    {Created Date}

Please review their onboarding status in Airtable.
```

> If Slack is preferred, this step can be replaced with a "Send a Slack message" action using the same dynamic fields in the message body.

---

### Step 3 (Branch B) — Flag Missing Email to HR

**Action Type:** Send an email  
**To:** hr@company.com  
**Subject:**
```
⚠️ High Value Hire with Missing/Invalid Email: {Full Name}
```
**Body:**
```
A new High Value hire was detected but their email address is missing or invalid.

Name:       {Full Name}
Email (raw): {Email Input}
Equipment:  ${Amount Spent on Equipment}

Action required: Please update their email address in Airtable.
```

---

### Step 4 — Log Record to Tracking Table (Both Branches)

**Action Type:** Create record  
**Table:** High Value Tracking  

| Field | Value |
|---|---|
| Hire Name | `{Full Name}` |
| Email | `{Cleaned Email}` |
| Amount Spent | `{Amount Spent on Equipment}` |
| Original Created Date | `{Created Date}` |
| Flagged Date | `TODAY()` |
| Email Status | `IF({Cleaned Email}!="", "Valid", "Missing/Invalid")` |
| Source Record ID | `RECORD_ID()` (linked field to New Hires) |

---

## 2. Interface Design

### Layout Summary

The interface has three sections:

**Section A — Summary Dashboard (Top)**  
Three summary tiles side-by-side:
- **High Value Hires** — count of records where Status = "High Value" (highlighted in green)
- **Medium Value Hires** — count of records where Status = "Medium Value" (highlighted in yellow)
- **Low Value Hires** — count of records where Status = "Low Value" (highlighted in grey)

Each tile uses a Count element filtered to the relevant status.

---

**Section B — High Value Grid (Middle)**  
A filtered grid view showing only "High Value" records with the following columns:
- Full Name
- Cleaned Email
- Amount Spent on Equipment
- Days Since Created
- Status Categorization

The grid is sorted by Amount Spent (descending) so the highest spenders appear first.

---

**Section C — New Hire Detail View (Bottom / Side Panel)**  
Clicking any row in the grid opens a detail panel showing:
- Full Name (large heading)
- Email (with mailto link if valid)
- Amount Spent on Equipment
- Status badge (color-coded)
- Days Since Created
- Created Date
- Raw Email Input (for reference/audit)

---

## 3. Formula Logic Used in Automation

**Email validation check (used in conditional branch):**
```
AND(
  {Cleaned Email} != "",
  FIND("@", {Cleaned Email}) > 0,
  FIND(".", {Cleaned Email}) > FIND("@", {Cleaned Email})
)
```

**Email status label (used when logging to Tracking Table):**
```
IF(
  AND(
    {Cleaned Email} != "",
    FIND("@", {Cleaned Email}) > 0
  ),
  "Valid",
  "Missing/Invalid"
)
```

---

## 4. Assumptions

1. **Trigger behaviour:** Airtable's "when a record matches conditions" trigger fires on both record creation and field updates, so the automation will correctly catch new hires entered above $1,000 and existing hires updated to exceed the threshold.

2. **Email validation scope:** The validation formula performs a basic structural check (contains `@` and `.` after `@`). It does not perform DNS/MX lookups or SMTP verification, which would require an external service. This is sufficient for flagging obvious missing or malformed inputs.

3. **Slack vs. Email:** The notification step was designed for email. If the team prefers Slack, the exact same dynamic content can be used in a "Send a Slack message" action — no formula changes are required.

4. **Tracking Table schema:** The High Value Tracking table is assumed to be a separate table created specifically for this audit log. It is not the same as the New Hires table.

5. **Currency:** "Amount Spent on Equipment" is assumed to be stored as a numeric (currency) field in USD. The `$` prefix in notifications is hardcoded.

6. **Interface permissions:** The interface is intended for HR staff only and should be shared with the appropriate Airtable workspace members via Interface Designer permissions.

7. **Duplicate prevention:** If the same record is updated multiple times (e.g. amount fluctuates around $1,000), multiple tracking records could be created. A deduplication step (checking if a tracking record for that hire already exists) could be added if needed.
