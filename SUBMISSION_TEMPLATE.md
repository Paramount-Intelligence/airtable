# Candidate Submission Template

## Candidate Information
- Full Name: Huzaifa Ahmed
- Email: huzaifafabi15@gmail.com
- LinkedIn: https://www.linkedin.com/in/huzaifa-ahmed-b15214225/
- Airtable Base Link: https://airtable.com/appAzUsisuj0MTmgG/shroD94ZCpWpax061
- Submission Date: March 15th, 2026.

## Task 1: Intermediate Airtable Skills

### 1. Full Name Formula
```
{First Name} & " " & {Last Name}
```
This formula concatenates the First Name and Last Name fields with a space in between to generate a full name for each new hire.

### 2. Cleaned Email Formula
```
TRIM(LOWER({Email Input}))
```
This formula converts the email to lowercase and removes any leading/trailing whitespace to ensure consistent and clean email formatting.

### 3. Status Categorization Formula
```
IF({Amount Spent on Equipment} > 1000, "High Value",
  IF({Amount Spent on Equipment} >= 500, "Medium Value", "Low Value"))
```
This formula categorizes each new hire into three tiers based on their equipment budget:
- **High Value** → spent more than $1000
- **Medium Value** → spent between $500 and $1000
- **Low Value** → spent less than $500

### 4. Days Since Created Formula
```
DATETIME_DIFF(TODAY(), {Created Date}, 'days')
```
This formula calculates the number of days elapsed since the onboarding record was created, helping HR track how long each hire has been in the system.

---

## Task 2: Advanced Airtable Automation

### 1. Automation Steps

The automation was built with the following steps:

**Trigger:** When a record is created in the **New Hires** table.

**Action 1 – Create Onboarding Tracking Record:**
A new record is automatically created in the **Onboarding Tracking** table with the following mapped fields:
- Employee Name → Full Name (formula field)
- Department → Department
- Start Date → Start Date
- Onboarding Status → "In Progress" (static value)
- Equipment Budget → Amount Spent on Equipment

**Action 2 – Send Welcome Email:**
An automated welcome email is sent to the new hire's cleaned email address with the following details:
- **To:** Cleaned Email (formula field)
- **Subject:** Welcome to the Team!
- **Body:** Hi [Full Name], welcome aboard! Your onboarding process has officially started.

### 2. Interface Design

The Airtable interface was designed with the following layout:

- **New Hires Table View** – Displays all incoming employee records with key fields: Full Name, Department, Start Date, Equipment Status, and Days Since Created.
- **Onboarding Tracking Table** – Linked table that shows real-time onboarding progress for each hire.
- **Dashboard** – A visual summary interface showing total hires, status distribution (High/Medium/Low Value), and onboarding progress.

Screenshots are available in `/assets/screenshots/`.

### 3. Formula Logic

The following formula fields were used within the automation context:

- **Full Name** – Used in automation to personalize the welcome email and tracking record.
- **Cleaned Email** – Used as the recipient address in the automated email action.
- **Status Categorization** – Used in the dashboard to visually group hires by equipment value tier.
- **Days Since Created** – Used to monitor and flag records that have been in onboarding for too long.

### 4. Assumptions

- The **Created Date** field uses Airtable's built-in `Created time` field type for accuracy.
- Email addresses entered in `Email Input` may have inconsistent formatting, hence the TRIM + LOWER formula.
- Equipment spending threshold values ($500 and $1000) were assumed based on standard HR budget tiers.
- Onboarding Status is set to **"In Progress"** by default upon record creation; manual update is needed for completion.
- The automation sends emails via Airtable's built-in email action (no third-party integration required).

### 5. Optional Notes

- The dashboard was designed keeping non-technical HR users in mind — simple layout, clear labels, and color-coded status fields.
- All formula fields are read-only and auto-calculated to reduce manual data entry errors.
- The automation is scalable — additional actions (e.g., Slack notification, task assignment) can be added as future enhancements.