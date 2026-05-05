# Candidate Submission Template

## Candidate Information
- **Full Name:** Mohtashim usmani
- **Email:** mohtashimusmani09gmail.com
- **LinkedIn or Portfolio:** www.linkedin.com/in/mohtashim-usmani
- **Submission Date:** May 6, 2026

## Task 1: Intermediate Airtable Skills

### 1. Full Name Formula
`{First Name} & " " & {Last Name}`

### 2. Cleaned Email Formula
`TRIM({Email Input})`

### 3. Status Categorization Formula
`IF({Amount Spent on Equipment} > 1000, "High Value", IF({Amount Spent on Equipment} >= 500, "Medium Value", "Low Value"))`

### 4. Days Since Created Formula
`DATETIME_DIFF(NOW(), {Created Date}, 'days')`

## Task 2: Advanced Airtable Automation

### 1. Automation Steps
* **Trigger:** The automation is set to trigger when a record in the **New Hires** table matches the condition: `Status Categorization` is "High Value".
* **Conditional Branching:** * **Branch A (Valid Email):** If the `Cleaned Email` field is not empty, the system proceeds with standard notifications.
    * **Branch B (Missing Email):** If the email field is empty, the system sends an urgent alert to HR titled "Missing Data: Action Required".
* **Slack/Email Notification:** A dynamic message is sent to the HR team including the hire's Full Name and Department to ensure immediate attention.
* **Tracking Log:** The automation automatically creates a new record in a separate **Tracking Table** to maintain a permanent audit log of all high-priority hires.

### 2. Interface Design
The HR Dashboard Interface is designed for high-level visibility and focused task management:
* **Summary Tiles:** Three numeric tiles at the top display the real-time counts of High, Medium, and Low value hires.
* **Filtered Grid:** A central list view that only displays hires marked as "High Value" to help HR prioritize their workflow.
* **Detail View:** A side-peek configuration that allows users to click a record and view all fields, including the specific equipment spend and contact details.

### 3. Formula Logic
The automation utilizes the **Status Categorization** formula logic from Task 1 as its primary trigger condition:
`IF({Amount Spent on Equipment} > 1000, "High Value", IF({Amount Spent on Equipment} >= 500, "Medium Value", "Low Value"))`.

### 4. Assumptions
* Assumed that "High Value" hires require a faster onboarding response time, justifying the use of instant Slack alerts.
* Assumed the "Tracking Table" is used for executive-level reporting and permanent record keeping rather than daily editing.
* Assumed the organization uses a standard currency format for equipment spend inputs.

### 5. Optional Notes
All logic and automation workflows were tested for data integrity, particularly focusing on the conditional branching for missing emails to prevent system failures during high-volume onboarding periods.
