# Submission Template — Airtable HR Onboarding Automation Dashboard

## Candidate Information

**Assessment:** Airtable HR Onboarding Automation Dashboard  
**Full Name:** Bilal Imran
**Email:** acc.bilalimran@gmail.com
**Linkedln:** bilalimran73ai
**Submission Date:** [16/03/2026]  
**GitHub Fork:** https://github.com/Bilal-73/hr-onboarding-automation-system  


---

## Task 1 Summary — Data Cleaning & Categorization

**File:** `submissions/task1_solution.md`

### What Was Built

A complete Airtable base (`New Hires` table) with the following formula fields:

**Data Cleaning Formulas:**
- `Clean Name` — Uses `PROPER(TRIM())` to normalize all name casing
- `Clean Email` — Uses `LOWER(TRIM())` to standardize email addresses
- `Clean Job Title` — Uses `PROPER(TRIM())` for consistent title display
- `Days Until Start` — `DATETIME_DIFF` from today to start date
- `Start Month` — Extracts month/year for grouping

**Categorization Formulas:**
- `Seniority Level` — Classifies C-Suite / Director-VP / Senior-Manager / Mid-Level / Junior based on job title keywords
- `Candidate Priority` — Classifies High Value / Standard / Entry Level / Contractor based on salary + seniority
- `Onboarding Stage` — Tracks 6 stages from "Awaiting Documents" to "Ready for Day 1" to "Complete"
- `Urgency Flag` — Flags URGENT (≤7 days, incomplete), Starting Soon (≤14 days), or On Track
- `Onboarding Completion %` — Calculates percentage based on 3 checkbox fields
- `Department Group` — Groups departments into Tech/Product, Revenue, Operations/Support

### 6 Views Configured
All New Hires | High Value Hires | Urgent Actions | Incomplete Onboarding | By Department | Contractors

---

## Task 2 Summary — Automations & HR Dashboard

**File:** `submissions/task2_solution.md`

### Automations Built (5 Total)

| # | Automation | Trigger | Action |
|---|---|---|---|
| 1 | High Value Hire Alert | Record matches: Priority = High Value | Email HR Lead + flag record |
| 2 | Daily Urgency Digest | Daily at 8 AM | Find records starting ≤7 days, incomplete → email HR team |
| 3 | Welcome Email | Onboarding Stage → Ready for Day 1 | Send personalized welcome email to new hire |
| 4 | 30-Day Feedback Survey | Daily: Days Since Start = 30 | Send feedback survey to employee |
| 5 | Document Reminder | Daily: Docs missing + starting ≤14 days | Email employee and manager reminder |

### HR Dashboard — 5 Pages Built

| Page | Purpose |
|---|---|
| Onboarding Overview | KPI cards, urgency pipeline, completion stats, department chart |
| Action Required | Daily HR work queue — filtered to incomplete, sorted by urgency |
| High Value Hires | Gallery view of all priority employees |
| Department Overview | Grouped by department with hire counts and completion stats |
| New Hire Detail | Full record detail with editable checkboxes |

---

## Key Design Decisions

**Why formula-based priority classification?**
Automatically recalculates when salary or title changes — no manual re-tagging needed.

**Why 5 automations instead of just 1?**
Each automation handles a distinct business need. A single monolithic automation would be harder to debug and maintain.

**Why the Interface Designer over just views?**
The Interface Designer provides a purpose-built HR experience — non-technical HR managers can use it without needing to understand Airtable's base structure. It also supports charts, KPI metrics, and filtered layouts not available in standard views.

---

## Files Included

```
submissions/
  ├── task1_solution.md    ← Base structure, formulas, views, sample data
  ├── task2_solution.md    ← Automations, dashboard layout, end-to-end flow
assets/
  ├── screenshots/         ← Screenshots of base, formulas, automations, dashboard
```
