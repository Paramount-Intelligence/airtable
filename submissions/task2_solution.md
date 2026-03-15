# Task 2 – Airtable Automation Workflow

## Overview

The objective of Task 2 was to build an automated onboarding workflow in Airtable that triggers when a new employee record is created and performs a series of actions automatically.

---

## Automation Trigger

**Trigger Type:** When a record is created  
**Table:** New Hires  

When any new record is added to the New Hires table, the automation fires automatically.

---

## Automation Actions

### Action 1 – Create Onboarding Tracking Record

**Action Type:** Create record  
**Table:** Onboarding Tracking  

A new record is created in the Onboarding Tracking table with the following mapped fields:

| Tracking Field        | Source (New Hires)         |
|-----------------------|----------------------------|
| Employee Name         | Full Name (formula field)  |
| Department            | Department                 |
| Start Date            | Start Date                 |
| Onboarding Status     | "In Progress" (static)     |
| Equipment Budget      | Amount Spent on Equipment  |

---

### Action 2 – Send Welcome Email

**Action Type:** Send email  

| Email Field | Value                                      |
|-------------|--------------------------------------------|
| To          | Cleaned Email (formula field)              |
| Subject     | Welcome to the Team!                       |
| Body        | Hi [Full Name], welcome aboard! Your onboarding has started. |

---

## Screenshots

All screenshots are located in `/assets/screenshots/`:

- `airtable_table_structure.png` – New Hires table with all fields
- `automation_trigger.png` – Trigger configuration
- `automation_workflow.png` – Full automation steps
- `tracking_table.png` – Onboarding Tracking table
- `dashboard_interface.png` – Final dashboard view
- `AND MORE PICTURES/SCRENNSHOTS`


## Dashboard Screenshots

All dashboard screenshots are located in `/dashboard-preview`

