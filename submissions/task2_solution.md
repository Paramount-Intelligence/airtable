# Task 2 Solution — Advanced Airtable Automation & Interface

**Author:** Dileep Singh  
**Email:** baghirajput2326@gmail.com  
**Submission Date:** 2026-03-13

---

## Overview

This solution builds an Airtable automation that detects High Value new hires and triggers a notification + tracking workflow, plus an Interface dashboard for HR visibility across all onboarding tiers.

---

## Part 1 — Automation Workflow

### Automation Name: `High Value Hire Alert & Tracker`

---

### Step 1 — Trigger

**Type:** When a record matches a condition  
**Table:** New Hires  
**Condition:** `Status Category` is `High Value`

This trigger fires whenever a record's Status Category formula evaluates to "High Value" — which happens automatically when the Amount Spent on Equipment exceeds 1000. No manual action is needed from HR to activate this automation.

---

### Step 2 — Conditional Branch: Email Valid?

**Type:** Conditional logic  
**Condition:** `Cleaned Email` is not empty AND `Cleaned Email` contains `@`

This branch checks whether the new hire has a valid email before attempting to send a notification.

**If email is VALID → proceed to Step 3**  
**If email is MISSING or INVALID → proceed to Step 4**

**Formula used for email validation check:**
```
AND(
  {Cleaned Email} != "",
  FIND("@", {Cleaned Email}) > 0
)
```

---

### Step 3a — Send Email Notification (Valid Email path)

**Type:** Send an email  
**To:** hr@company.com  
**Subject:** `🔔 High Value New Hire Alert — {Full Name}`  
**Body:**
```
Hi HR Team,

A new hire has been categorized as High Value and requires priority onboarding attention.

Name: {Full Name}
Email: {Cleaned Email}
Equipment Spend: {Amount Spent on Equipment}
Record Created: {Created Date}
Days Since Created: {Days Since Created}

Please ensure priority onboarding tasks are assigned immediately.

— Onboarding Automation System
```

---

### Step 3b — Send Slack Notification (Valid Email path)

**Type:** Send a Slack message  
**Channel:** `#hr-onboarding-alerts`  
**Message:**
```
🔔 *High Value New Hire Detected*

*Name:* {Full Name}
*Email:* {Cleaned Email}
*Equipment Spend:* ${Amount Spent on Equipment}
*Days Since Record Created:* {Days Since Created}

Please prioritize this hire's onboarding immediately.
```

---

### Step 4 — HR Alert: Missing Email (Invalid Email path)

**Type:** Send an email  
**To:** hr@company.com  
**Subject:** `⚠️ High Value Hire Missing Email — Action Required`  
**Body:**
```
Hi HR Team,

A new hire has been flagged as High Value but does not have a valid email address on record.

Name: {Full Name}
Equipment Spend: {Amount Spent on Equipment}
Record Created: {Created Date}

Please update the email address in Airtable so the onboarding notification can be sent.

— Onboarding Automation System
```

---

### Step 5 — Log to Tracking Table

**Type:** Create record  
**Table:** High Value Tracking  

**Fields to populate:**

| Field | Value |
|---|---|
| Hire Name | `{Full Name}` |
| Email | `{Cleaned Email}` |
| Equipment Spend | `{Amount Spent on Equipment}` |
| Alert Sent Date | `TODAY()` |
| Email Valid | `{Cleaned Email} contains @` → Yes / No |
| Status | `Logged` |

This creates a permanent audit log of every High Value hire detected, with a record of whether the email notification was successfully sent.

---

### Full Automation Flow Diagram

```
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
```

---

## Part 2 — Interface Design

### Interface Name: `HR Onboarding Dashboard`

---

### Page 1 — Overview Dashboard

**Layout: 3 Summary Tiles (top row)**

**Tile 1 — High Value Count**
- Element type: Count
- Filter: `Status Category = "High Value"`
- Label: `🔴 High Value Hires`
- Color: Red

**Tile 2 — Medium Value Count**
- Element type: Count
- Filter: `Status Category = "Medium Value"`
- Label: `🟡 Medium Value Hires`
- Color: Yellow

**Tile 3 — Low Value Count**
- Element type: Count
- Filter: `Status Category = "Low Value"`
- Label: `🟢 Low Value Hires`
- Color: Green

**Below tiles: Full Grid View**
- Shows all new hires
- Columns: Full Name, Cleaned Email, Amount Spent on Equipment, Status Category, Days Since Created
- Sorted by: Days Since Created (ascending — oldest records first)

---

### Page 2 — High Value Hires

**Layout: Filtered Grid**

- Filter: `Status Category = "High Value"`
- Columns: Full Name, Cleaned Email, Amount Spent on Equipment, Created Date, Days Since Created
- Sorted by: Amount Spent on Equipment (descending)
- Purpose: Gives HR a focused view of only the priority hires requiring immediate attention

---

### Page 3 — New Hire Detail View

**Layout: Record detail view**

- Triggered by clicking any record in the grid
- Shows full detail for the selected new hire:
  - Full Name
  - Cleaned Email
  - Amount Spent on Equipment
  - Status Category (with color coding)
  - Created Date
  - Days Since Created
  - Original Email Input (for reference)

---

## Assumptions

1. The `Status Category` formula field from Task 1 is the trigger source for the automation — no separate field is needed.
2. Email validation checks for presence of `@` symbol as a basic validity check. Full regex validation is not natively available in Airtable automations.
3. The Tracking Table (`High Value Tracking`) is a separate table in the same Airtable base, created manually before the automation runs.
4. Slack integration is configured in Airtable under the workspace's connected apps. If Slack is not connected, the email notification alone serves as the primary alert.
5. The automation runs on record update as well as record creation — so if a hire's equipment spend is updated later and crosses the 1000 threshold, the automation will still trigger.
6. The interface is built using Airtable Interface Designer and is shared with the HR team via Airtable's share link feature.
7. Mock/sample data is used for the screenshots and example table in `formulas.md`.

---

## Optional Notes

- The automation is designed to be idempotent where possible — the Tracking Table log provides a history, so even if the automation fires twice for the same record, the audit trail is preserved.
- The conditional email validation branch is a practical workaround for Airtable's lack of native regex support in automations.
- For a production deployment, I would recommend adding a "Notification Sent" checkbox field to the New Hires table so HR can confirm receipt and prevent duplicate alerts.
- The interface pages are designed for non-technical HR users — minimal clicks, clear labels, and color-coded status tiles.
