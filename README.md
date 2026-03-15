# Airtable HR Onboarding Automation Dashboard

This project demonstrates how Airtable can be used to build an HR onboarding management system that combines structured data handling, formula based data processing, automation workflows, and a visual dashboard for HR teams.

The system processes new hire data, categorizes candidates, triggers automated workflows for high value hires, and provides a centralized dashboard interface for HR visibility.

The objective of this exercise is to showcase the practical use of Airtable formulas, automations, and interfaces to solve real world HR operational challenges.

---

# Project Outcome

The implemented solution transforms raw onboarding data into a structured workflow for HR operations.

Key outcomes include

- Automated cleaning and categorization of new hire data using Airtable formulas
- Identification of high value hires through calculated fields
- Automation triggers for important onboarding events
- A centralized HR dashboard for monitoring onboarding progress
- Improved operational visibility for HR teams managing multiple hires

The system demonstrates how Airtable can act as a lightweight operations platform for HR onboarding processes.

---

# System Overview

The onboarding system is built entirely using Airtable's native capabilities.

Data Layer
Airtable tables store records for new hires and onboarding data. The New Hires table contains five sample records with fields for First Name, Last Name, Email Input, Amount Spent on Equipment, and Created Date.

Logic Layer
Formula fields process and categorize employee information using four custom formulas for full name generation, email cleaning, status categorization, and days since record creation.

Automation Layer
Airtable automations trigger actions when specific conditions are met. The High Value Hire Notification automation detects high value hires and triggers conditional email notifications and record logging.

Interface Layer
Airtable Interface Designer provides a dashboard for HR teams to monitor onboarding activity. The HR Onboarding Dashboard displays summary metrics and filtered views of new hire data.

---

# Task 1 Outcome
## Data Cleaning and Categorization

Formulas were implemented to transform and standardize new hire records submitted through the onboarding table.

### Formulas Implemented

**Full Name**
```
{First Name} & " " & {Last Name}
```
Concatenates first and last name fields to generate a clean display name.

**Cleaned Email**
```
TRIM(LOWER({Email Input}))
```
Removes extra spaces and converts email to lowercase for consistent formatting.

**Status Categorization**
```
IF(
    {Amount Spent on Equipment} > 1000,
    "High Value",
    IF(
        {Amount Spent on Equipment} >= 500,
        "Medium Value",
        "Low Value"
    )
)
```
Categorizes each hire into High Value, Medium Value, or Low Value based on equipment spending.

**Days Since Created**
```
DATETIME_DIFF(TODAY(), {Created Date}, 'days')
```
Calculates how many days have passed since the record was created.

---

# Task 2 Outcome
## Automation and HR Dashboard

### Automation — High Value Hire Notification

An automation workflow was implemented to handle high value hires.

Trigger
When a record matches conditions — Status Categorization contains High Value.

Conditional Branch 1 — If Cleaned Email is not empty
- Sends a welcome notification email to the hire
- Logs the record in the High Value Tracking table with Full Name, Email, Equipment Amount, and Date Logged

Conditional Branch 2 — If Cleaned Email is empty
- Sends an alert email to HR at hr@company.com
- Message notifies HR that a high value hire record is missing an email address and requires manual review

### High Value Tracking Table

A dedicated tracking table was created to log all high value hires automatically.

Fields
- Full Name
- Email
- Equipment Amount
- Date Logged

### HR Dashboard Interface

An interface dashboard was created using Airtable Interface Designer named HR Onboarding Dashboard.

Dashboard Components

Summary Tiles
- High Value hire count
- Medium Value hire count
- Low Value hire count

Filtered List View
- Shows only High Value hires from the New Hires table
- Allows HR to quickly identify priority onboarding cases

New Hires Data Grid
- Complete list of all hires with key fields visible
- Fields shown: First Name, Last Name, Email Input, Amount Spent on Equipment

---

# Airtable Features Used

Formulas
Used to clean and categorize onboarding data across four formula fields.

Automations
Used to trigger conditional email notifications and record creation when high value hires are detected.

Interfaces
Used to build a visual dashboard with summary tiles and filtered grid views for HR operations.

Views and Filters
Used to segment onboarding records for easier monitoring of high value candidates.

---

# Repository Structure
```
hr-onboarding-automation-system

submissions
 ├── task1_solution.md
 └── task2_solution.md

assets
 ├── screenshots
 │   ├── airtable_table_structure.png
 │   ├── automation_trigger.png
 │   ├── automation_workflow.png
 │   ├── tracking_table.png
 │   └── dashboard_interface.png
 └── dashboard-preview

INSTRUCTIONS.md
TASK_1.md
TASK_2.md
SUBMISSION_TEMPLATE.md
README.md
```

---

# Screenshots

Screenshots included in the repository demonstrate

- Airtable base and table structure with all formula fields
- Automation trigger configuration showing Status Categorization condition
- Complete automation workflow with conditional branches
- High Value Tracking table with logged records
- HR Onboarding Dashboard interface

---

# Assumptions

- Equipment spending is used as the primary indicator of onboarding priority
- Email notifications are used as the main HR alert mechanism
- Sample data was used for demonstration purposes
- Airtable free plan was used during development which limits some advanced features such as emailing non-collaborators and certain interface components

---

# Potential Improvements

Future improvements for this system may include

- Integration with external HRIS systems
- Slack or email alerts for onboarding milestones
- Automated onboarding task tracking
- Employee lifecycle management beyond onboarding
- HR analytics and reporting dashboards

---

# Author

Candidate: Huzaifa Ahmed
Email: huzaifafabi15@gmail.com

This project was developed as part of an Airtable skills assessment focused on data processing, workflow automation, and dashboard creation for HR onboarding management.