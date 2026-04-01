# Task 2 Solution — Airtable Automations & HR Dashboard

## Overview

This document covers the complete automation workflows and HR Interface Dashboard built inside Airtable. The system automatically detects High Value hires, triggers priority notifications, and presents a real-time operational view for HR teams.

---

## 1. Automation 1 — High Value Hire Alert

**Trigger:** When a record matches the condition  
**Condition:** `Candidate Priority` is `High Value`

**Purpose:** As soon as a new hire is classified as High Value (via the formula field), the automation fires — notifying HR leadership and fast-tracking their onboarding actions.

### Configuration:

**Trigger Setup:**
```
Trigger type: When record matches conditions
Table: New Hires
Condition: Candidate Priority = "High Value"
Run: Once per record (prevents duplicate notifications)
```

**Action 1 — Send Email Notification to HR Lead:**
```
Action type: Send an email
To: hr-lead@company.com
Subject: [HIGH VALUE] New Hire Alert — {Clean Name} starting {Start Date}
Body:
Hi HR Team,

A High Value hire has been added to the onboarding system and requires priority attention.

Employee Details:
• Name: {Clean Name}
• Role: {Clean Job Title}
• Department: {Department}
• Seniority: {Seniority Level}
• Start Date: {Start Date}
• Location: {Office Location}
• Manager: {Manager Name}
• Urgency: {Urgency Flag}

Current Onboarding Stage: {Onboarding Stage}
Completion: {Onboarding Completion %}

Please review and ensure all onboarding tasks are prioritized for this hire.

Action required:
- Confirm IT setup is scheduled
- Verify all documents have been collected
- Assign compliance training immediately

View record: [Link to Airtable record]

— HR Onboarding Automation System
```

**Action 2 — Update Record Field:**
```
Action type: Update record
Field: Notes
Value: "⚡ HIGH VALUE — Priority onboarding initiated on {TODAY()}"
```

---

## 2. Automation 2 — Urgent Onboarding Alert (Starting in 7 Days)

**Trigger:** At a scheduled time (runs daily at 8:00 AM)  
**Purpose:** Every morning, scans all records starting within 7 days that still have incomplete onboarding. Sends a daily digest to HR.

### Configuration:

**Trigger Setup:**
```
Trigger type: At a scheduled time
Frequency: Daily
Time: 8:00 AM (local timezone)
```

**Action — Find Records:**
```
Action type: Find records
Table: New Hires
Filter: 
  - Days Until Start <= 7
  - Days Until Start >= 0
  - Onboarding Stage is NOT "✅ Complete"
  - Onboarding Stage is NOT "🟢 Ready for Day 1"
```

**Action — Send Email Summary:**
```
Action type: Send an email
To: hr-team@company.com
Subject: ⚠️ Daily Onboarding Alert — {count} hires need attention today
Body:
The following employees are starting within 7 days and have incomplete onboarding:

{list of records with name, start date, stage, and urgency flag}

Please log in to the HR Dashboard to take action.
```

---

## 3. Automation 3 — Welcome Email Trigger

**Trigger:** When record matches conditions  
**Condition:** `Onboarding Stage` changes to `🟢 Ready for Day 1`

**Purpose:** When all three checklist boxes are ticked (Documents, IT, Training), the employee is automatically sent a personalized welcome email.

### Configuration:

**Trigger Setup:**
```
Trigger type: When a record is updated
Table: New Hires
Field watched: Onboarding Stage
Condition: New value = "🟢 Ready for Day 1"
```

**Action — Send Welcome Email:**
```
Action type: Send an email
To: {Personal Email}
Subject: {Welcome Email Subject}   ← uses the formula field from Task 1
Body:
Hi {First Name},

We're thrilled to officially welcome you to the team! 🎉

Your onboarding is fully set up and you're ready for your first day on {Start Date}.

Here's what you need to know:
• Your manager {Manager Name} will be in touch before your start date
• Your company email and all system access will be ready on Day 1
• You've been enrolled in the required compliance training — please complete it within your first week

If you have any questions before you start, reach out to hr@company.com.

We can't wait to have you on board!

Warm regards,
The HR Team
```

**Action — Update Onboarding Status:**
```
Action type: Update record
Field: Onboarding Status
Value: "In Progress"
```

---

## 4. Automation 4 — 30-Day Milestone Check-In

**Trigger:** At a scheduled time (runs daily)  
**Condition:** `Days Since Start` = 30

**Purpose:** Automatically sends a 30-day feedback survey request to employees who started exactly 30 days ago.

### Configuration:

**Trigger:**
```
Trigger type: At a scheduled time
Frequency: Daily
Time: 9:00 AM
```

**Action — Find Records where Days Since Start = 30:**
```
Filter: Days Since Start = 30
```

**Action — Send Feedback Email:**
```
To: {Personal Email}
Subject: How's your first month going, {First Name}? 
Body:
Hi {First Name},

Congratulations on completing your first 30 days at the company! 🎊

We'd love to hear how your onboarding experience has been. Please take 2 minutes to share your feedback:

[Feedback Form Link]

Your input helps us improve the experience for future team members.

Thanks,
The HR Team
```

---

## 5. Automation 5 — Document Reminder

**Trigger:** At a scheduled time (runs daily at 9:00 AM)  
**Condition:** `Documents Submitted` is unchecked AND `Days Until Start` is between 3 and 14

**Purpose:** Sends a reminder to the employee and manager if documents are missing with less than 2 weeks to go.

### Configuration:

```
Trigger: Daily at 9:00 AM
Find records where:
  - Documents Submitted = false (unchecked)
  - Days Until Start <= 14
  - Days Until Start >= 3

Action: Send email to {Personal Email} AND {Manager Email}
Subject: Action Required: Missing documents for {Clean Name} — starts {Start Date}
Body: 
We noticed that required documents have not yet been submitted for {Clean Name}.

Outstanding documents must be received at least 3 business days before the start date.

Please submit documents to: hr@company.com or upload directly to the onboarding portal.

Start date: {Start Date}
Days remaining: {Days Until Start}

— HR Onboarding System
```

---

## 6. HR Dashboard — Interface Designer

The HR Dashboard is built using Airtable's Interface Designer. It provides a real-time operational view for HR teams.

### Dashboard Layout

**Page 1: Onboarding Overview (Home)**

```
┌─────────────────────────────────────────────────────────────┐
│  HR ONBOARDING DASHBOARD                      [Today's Date] │
├────────────┬──────────────┬───────────────┬─────────────────┤
│  Total     │  High Value  │  Starting     │  Needs Action   │
│  Active    │  Hires       │  This Week    │  Today          │
│  [Count]   │  [Count]     │  [Count]      │  [Count]        │
├────────────┴──────────────┴───────────────┴─────────────────┤
│  URGENCY PIPELINE                                            │
│  🚨 Urgent (≤7 days, incomplete): [Count] records           │
│  ⚠️  Starting Soon (≤14 days):    [Count] records           │
│  ✔  On Track:                    [Count] records            │
├──────────────────────────────────────────────────────────────┤
│  ONBOARDING COMPLETION BREAKDOWN                             │
│  ████████░░  Documents Submitted: 82%                        │
│  ██████░░░░  IT Setup Complete:   61%                        │
│  ███████░░░  Training Assigned:   74%                        │
├──────────────────────────────────────────────────────────────┤
│  NEW HIRES BY DEPARTMENT     │  PRIORITY BREAKDOWN           │
│  [Bar chart]                 │  High Value: [Count]          │
│  Engineering  ████  12       │  Standard:   [Count]          │
│  Sales        ███   8        │  Entry Level:[Count]          │
│  Product      ██    5        │  Contractor: [Count]          │
│  Marketing    ██    4        │                               │
└──────────────────────────────────────────────────────────────┘
```

**Interface Elements Used:**
- **Number widgets** (4 KPI cards at top) — Total Active, High Value, Starting This Week, Needs Action
- **Record list** filtered to Urgency Flag contains URGENT
- **Progress bars** — Documents Submitted %, IT Complete %, Training Assigned % (using summary formula across all records)
- **Chart widget** — Bar chart of new hires by Department
- **Donut chart** — Breakdown by Candidate Priority

---

**Page 2: Action Required**

```
Purpose: Daily HR work queue — shows only records that need immediate attention

Filters applied:
  - Onboarding Stage is NOT "✅ Complete"
  - Onboarding Stage is NOT "🟢 Ready for Day 1"

Sort: Days Until Start (ascending — most urgent first)

Fields shown:
  - Clean Name
  - Clean Job Title
  - Department
  - Candidate Priority  
  - Start Date
  - Days Until Start
  - Onboarding Stage
  - Urgency Flag
  - Onboarding Completion %
  - Manager Name

Conditional color coding:
  - Red row:    Urgency Flag contains "URGENT"
  - Yellow row: Urgency Flag contains "Soon"
  - Green row:  Onboarding Stage = "🟢 Ready for Day 1"
```

---

**Page 3: High Value Hires**

```
Purpose: Dedicated view for monitoring priority employees

Filter: Candidate Priority = "High Value"

Layout: Gallery view with key fields highlighted

Fields shown per card:
  - Clean Name (heading)
  - Clean Job Title
  - Department
  - Start Date
  - Onboarding Stage (color-coded chip)
  - Urgency Flag
  - Manager Name
  - Onboarding Completion %
```

---

**Page 4: Department Overview**

```
Purpose: Department-level visibility for HR managers and department heads

Layout: Grouped record list, grouped by Department Group

For each department shows:
  - Count of new hires
  - Count of High Value hires
  - Count with incomplete onboarding
  - Earliest start date in the group

Filters: Start Date is within the next 90 days
```

---

**Page 5: New Hire Detail (Record Detail View)**

```
Purpose: Click into any employee record for full details and the ability to update checkboxes

Fields shown:
  - Clean Name
  - Clean Job Title
  - Department, Seniority Level
  - Start Date, Days Until Start
  - Candidate Priority, Urgency Flag
  - Onboarding Stage, Onboarding Completion %
  - Documents Submitted ✅ / ❌
  - IT Setup Complete ✅ / ❌
  - Training Assigned ✅ / ❌
  - Manager Name, Manager Email
  - Notes (editable)
  - Welcome Email Subject (auto-generated)
```

---

## 7. How the System Works End-to-End

```
New hire record added (manual or form)
          │
          ▼
Formulas fire instantly:
  - Name cleaned → Clean Name
  - Priority calculated → Candidate Priority
  - Stage determined → Onboarding Stage
  - Urgency evaluated → Urgency Flag
          │
          ▼
If Candidate Priority = "High Value"
  → Automation 1 fires: HR Lead notified by email, record flagged
          │
          ▼
Daily at 8 AM:
  → Automation 2 scans for starts within 7 days
  → Sends digest to HR team
          │
          ▼
When all 3 checkboxes are ticked:
  → Onboarding Stage becomes "🟢 Ready for Day 1"
  → Automation 3 fires: Welcome email sent to new hire
          │
          ▼
30 days after start:
  → Automation 4 fires: Feedback survey sent to employee
          │
          ▼
HR Dashboard updates in real time:
  → KPI cards update
  → Charts reflect current state
  → Action Required list shows who needs attention today
```

---

## 8. Screenshots Checklist

> Include the following screenshots in the `assets/screenshots/` folder:

- [ ] `01_base_structure.png` — Grid view of New Hires table showing all field columns
- [ ] `02_formula_fields.png` — Formula editor open on the Candidate Priority formula
- [ ] `03_seniority_formula.png` — Formula editor open on the Seniority Level formula
- [ ] `04_automation_high_value.png` — Automation 1 config showing trigger + actions
- [ ] `05_automation_welcome_email.png` — Automation 3 config showing email template
- [ ] `06_dashboard_overview.png` — Interface Designer — Page 1 overview with KPI cards
- [ ] `07_dashboard_action_required.png` — Interface Designer — Page 2 action queue
- [ ] `08_high_value_gallery.png` — Interface Designer — Page 3 high value hire gallery
- [ ] `09_sample_records.png` — Grid view showing sample records with formula outputs colored

---

## 9. Business Value

| Problem | Solution |
|---------|----------|
| HR manually checking who is starting soon | `Urgency Flag` formula + daily automation digest |
| High-value hires treated same as entry-level | `Candidate Priority` formula + instant alert automation |
| Inconsistent name/data formatting | `Clean Name`, `Clean Email`, `Clean Job Title` formulas |
| No visibility into onboarding completeness | `Onboarding Completion %` + dashboard progress bars |
| Welcome emails sent manually and inconsistently | Automation triggers email automatically when ready |
| No feedback on onboarding experience | 30-day milestone automation sends survey automatically |
| HR juggling spreadsheets across departments | Unified Interface Dashboard with department grouping |

---

*Submitted as Task 2 of the Airtable HR Onboarding Automation Assessment.*
