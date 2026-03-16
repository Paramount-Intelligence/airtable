Candidate Information
Full Name: Abdullah Khan
Email: abdullahejazkhan14@gmail.com
GitHub Profile Link: https://github.com/abdullahejazkhan
Submission Date: 2026-03-15


Task 2 – Airtable Automation Workflow

Overview:
The objective of Task 2 was to build an automated onboarding workflow in Airtable that triggers when a new employee record is created and performs a series of actions automatically.


Automation Trigger:
Trigger Type: When a record is created  
Table: New Hires  

When any new record is added to the New Hires table, the automation fires automatically.


Automation Actions:

Action 1 – Create Onboarding Tracking Record:

Action Type: Create record  
Table: Onboarding Tracking  

A new record is created in the Onboarding Tracking table with the following mapped fields:

| Tracking Field        | Source (New Hires)         |
|-----------------------|----------------------------|
| Employee Name         | Full Name (formula field)  |
| Department            | Department                 |
| Start Date            | Start Date                 |
| Onboarding Status     | "In Progress" (static)     |
| Equipment Budget      | Amount Spent on Equipment  |

and with some other fields too


Action 2 – Send Welcome Email

Action Type: Send email  

| Email Field | Value                                      |
|-------------|--------------------------------------------|
| To          | Cleaned Email (formula field)              |
| Subject     | Welcome to the Team!                       |
| Body        | Hi [Full Name], welcome aboard! Your onboarding has started. |



Screenshots:

All screenshots are located in '/assets/Overall_View/':

- 'Table_View.png' – New Hires table with all fields
- 'automation_Check.png' – Trigger configuration
- 'Automation_View.png' – Full automation view
- 'Formulas_Made.png' – All Formulas View


Dashboard Screenshots:
All dashboard screenshots are located in '/dashboards'


Formulas Used in Building the Automation:
Email validation check (used in conditional branch):

AND(
  {Cleaned Email} != "",
  FIND("@", {Cleaned Email}) > 0,
  FIND(".", {Cleaned Email}) > FIND("@", {Cleaned Email})
)


Email status label (used when logging to Tracking Table):

IF(
  AND(
    {Cleaned Email} != "",
    FIND("@", {Cleaned Email}) > 0
  ),
  "Valid",
  "Missing/Invalid"
)


Full Automation Flow Diagram:S
[Trigger: Status Category = "High Value"]
              │
              ▼
[Check: Is email valid?]
       │              │
      YES             NO
       │              │
       ▼              ▼
[Send Email    [Send HR Alert:
 to HR]         Missing Email]
       │
       ▼
[Send Slack
 Notification]
       │
       ▼
[Log record to
 Tracking Table]