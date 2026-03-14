# Task 2: Advanced Airtable Automation

## 1. Automation Steps

The automation workflow was designed to detect and prioritize **High Value hires**.

**Step 1 — Trigger**

The automation is triggered when a record in the **New Hires** table meets the condition:

```
Status = High Value
```

**Step 2 — Conditional Branching**

A conditional check verifies whether the **Cleaned Email** field is empty.

**Branch A — Email Available**

If the email is available:

- A notification email is sent to HR
- A new record is created in the **High Value Tracking** table

**Branch B — Email Missing**

If the email is missing:

- A notification alert is sent indicating that the high value hire does not have a valid email.

**Step 3 — Tracking Log**

The automation logs high value hires into the **High Value Tracking Table** with the following fields:

- Full Name
- Email
- Amount Spent on Equipment
- Date Logged

This allows HR teams to monitor high priority onboarding cases.

---

## 2. Interface Design

An HR onboarding dashboard was created using **Airtable Interface Designer**.

**Dashboard components include:**

**Summary Tiles**

Three tiles displaying counts for:

- High Value hires
- Medium Value hires
- Low Value hires

**Filtered Grid View**

A grid view showing only **High Value hires** for quick HR review.

**Detail View**

A record detail panel allowing HR staff to view complete information for each new hire including:

- Full Name
- Email
- Amount Spent on Equipment
- Status
- Days Since Created

Screenshots of the dashboard interface are included in the submission.

---

## 3. Formula Logic

The automation relies on the **Status Categorization Formula**.

**Formula**

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

This formula automatically determines when a hire becomes a **High Value** candidate and triggers the automation.

---

## 4. Assumptions

- The **Cleaned Email** field is used as the validated email input for automation notifications.
- High Value hires are defined as employees with equipment spending greater than 1000.
- The **High Value Tracking table** acts as a monitoring and audit table for priority hires.
- The HR team uses the Airtable interface dashboard to track onboarding progress.

---

## 5. Optional Notes

This solution demonstrates how Airtable can function as a lightweight HR operations platform.

The system integrates:

- Structured data processing
- Formula based classification
- Workflow automation
- A centralized monitoring dashboard

**Potential future improvements include:**

- Slack notifications for HR teams
- Integration with HRIS platforms
- Automated onboarding task management
- Advanced HR analytics dashboards