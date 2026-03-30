# Task 2 — Airtable Automation

This automation identifies high-value hires and notifies HR while logging the event in a tracking table.

## Automation Trigger

Trigger Type: When record matches conditions

Condition:

Status = "High Value"

This ensures the automation runs whenever a new hire becomes categorized as High Value.

---

## Conditional Logic

The automation checks whether the cleaned email field contains a valid value.

Condition:

Cleaned Email is empty

This creates two execution paths.

---

## Path 1 — Email Missing

If the Cleaned Email field is empty:

Actions performed:

1. Send Email Notification

The system sends an email notification indicating that a high-value hire has been added but the email is missing.

Example email content:

Subject: High Value Hire Missing Email

Body:
Name: {Full Name}
Amount Spent: {Amount Spent on Equipment}

2. Create Record in Tracking Table

A new record is logged with the following fields:

Name → Full Name  
Status → High Value  
Email Status → Missing  
Amount → Amount Spent on Equipment  

---

## Path 2 — Email Exists

If the Cleaned Email field contains a value:

Actions performed:

1. Send Email Notification

Subject: New High Value Hire

Body:
Name: {Full Name}  
Email: {Cleaned Email}  
Amount Spent: {Amount Spent on Equipment}

2. Create Record in Tracking Table

A record is created with the following information:

Name → Full Name  
Status → High Value  
Email Status → Valid  
Amount → Amount Spent on Equipment  

---

## Assumptions

- Email validation only checks whether the field is empty.
- HR notifications are sent via Airtable email automation.
- The tracking table is used to maintain a log of high-value hires.
- Amount thresholds follow the specification provided in the assignment.