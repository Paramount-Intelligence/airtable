# Candidate Submission Template

## Candidate Information
- Full Name: Momal Saleem
- Email:momalsaleem7@gmail.com
- LinkedIn or Portfolio: https://www.linkedin.com/in/momal-saleem-872505305/ , https://momalportfolio.netlify.app/ 
- Submission Date: 5/4/2026

## Task 1: Intermediate Airtable Skills

### 1. Full Name Formula
Formula:
{First Name} & " " & {Last Name}
Screenshot: task1ss/full name formula.png

### 2. Cleaned Email Formula
Formula:
LOWER(TRIM({Email}))
Screenshot: task1ss/email clean.png

### 3. Status Categorization Formula
Formula:
IF(
  {Amount Spent on Equipment} > 1000,
  "High Value",
  IF(
    {Amount Spent on Equipment} >= 500,
    "Medium Value",
    "Low Value"
  )
)
Screenshot: task1ss/status.png

### 4. Days Since Created Formula
DATETIME_DIFF(TODAY(), {Create date}, 'days')
Screenshot: task1ss/days since created.png

## Task 2: Advanced Airtable Automation

### 1. Automation Steps
Describe the steps taken to build the automation (trigger, Slack/Email notification, tracking log, conditional branching).
Screenshot: task2ss/automation.png
# trigger
The automation is triggered whenever a new record satisfies the condition i.e Status = 'High Value'
# AirTable condition Check
After the trigger, the following cases are dealt :
# CASE 1
In case 1 , the following condition is checked
1. The email is not empty and email contain '@'
If the condition meets, an email is sent to hr notifying them of high value and record and the record is stored in High Value Tracking
# CASE 2
If the email is missing or doesn't contain '@', an alert is sent to HR informing them of missingg email address

### 2. Interface Design
The interface provides structure and user friendly dashboard for tracking and monitoring records of new hires. The top summary banner shows count of records with High Value , Medium Value and Low Value. The second section shows the details of records present in High Value Tracking Table and the last section shows details of all records present in New Hire Table
Screenshot: task2ss/interface.png

### 3. Formula Logic
1. Status = "High Value"
2. IF Email is not empty AND Email contains "@"


### 4. Assumptions
An assumption was made that the New Hire Record already contains the following data
# Record 1
First Name: Momal
Last Name: Saleem
Full Name: Momal Saleem
Email: momalsaleem02@gmail.com
Amount Spent on Equipment: 2,300.0
Created Date: April 3, 2026
# Record 2
First Name: Ali
Last Name: Khan
Email: alikhan@gmail.com
Amount Spent on Equipment: 1,999.0
Created Date: April 3, 2026
### 5. Optional Notes
Anything else you'd like us to know.
