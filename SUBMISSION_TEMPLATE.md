# Candidate Submission Template

## Candidate Information
- **Full Name:** Bazil Bin Aamir
- **Email:** bazilaamir15@gmail.com
- **LinkedIn or Portfolio:** (https://www.linkedin.com/in/bazil-bin-aamir-105a952a7/)
- **Submission Date:** March 21, 2026

---

## Task 1: Intermediate Airtable Skills

### 1. Full Name Formula
To ensure clean data without trailing spaces from manual entry, I used a combination of `CONCATENATE` and `TRIM`:
```airtable
CONCATENATE(TRIM({First Name}), " ", TRIM({Last Name}))

### 2. Cleaned Email Formula
LOWER(TRIM({Email Input}))

### 3. Status Categorization Formula
IF(
  {Documents Uploaded} = BLANK(), 
  "Missing Documents", 
  IF(
    {Status} = "Pending", 
    "In Progress", 
    "Ready for Onboarding"
  )
)

### 4. Days Since Created Formula
DATETIME_DIFF(TODAY(), CREATED_TIME(), 'days')

## Task 2: Advanced Airtable Automation

1. Automation Steps
The automation orchestrates the handoff between HR and IT without manual data entry.

Trigger: "When record matches conditions" (Triggers when the Status Categorization formula outputs "Ready for Onboarding").

Conditional Branching: - If Department = "Engineering": Routes a high-priority equipment request.

Otherwise: Routes a standard equipment request.

Action 1 (Slack/Email Notification): Sends a dynamic welcome email to the candidate's Cleaned Email, and pings the internal IT Slack channel with the new hire's details and role.

Action 2 (Tracking Log): Executes a "Create Record" action in the secondary Audit Logs table, logging the Employee ID, timestamp, and the automation phase completed.

2. Interface Design
(See attached screenshots in the submissions folder)
The Interface was designed for two specific personas:

HR Dashboard: A high-level chart showing onboarding statuses by Department, and a metric number card highlighting any records where "Days Since Created" exceeds 7 days.

Operations Grid: A filtered list view showing only "Action Required" new hires. This allows HR coordinators to quickly update statuses or trigger reminder emails without viewing the cluttered backend database.

### 3. Formula Logic
CONCATENATE("New Hire Ready: ", {Full Name}, " is joining ", {Department}, " as a ", {Role}, ". Please provision access.")

### 4. Assumptions


### 5. Optional Notes
The base is designed to scale. By keeping raw inputs separated from cleaned formula fields (e.g., Email Input vs Cleaned Email), the architecture ensures that downstream automations will not fail due to human data-entry errors (like accidental spaces or capitalization).
