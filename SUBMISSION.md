# Candidate Submission

## Candidate Information

**Full Name:** Touseef Hanif

**Email:** [touseef.hanif@gmail.com](mailto:touseef.hanif@gmail.com)

**LinkedIn or Portfolio:** https://www.linkedin.com/in/touseef-hanif

**GitHub:** https://github.com/touseefh/hr-onboarding-automation-system

**Branch:** solution-touseef

**Submission Date:** March 14, 2026

---

# Task 1: Intermediate Airtable Skills

## Sample Records Used

The following records were inserted into the **New Hires** table to test the formulas.

| First Name | Last Name | Email Input                                               | Amount Spent on Equipment |
| ---------- | --------- | --------------------------------------------------------- | ------------------------- |
| Touseef    | Hanif     | [touseef.hanif@gmail.com](mailto:touseef.hanif@gmail.com) | 1200                      |
| Baber      | Azam      | [baber.azam@gmail.com](mailto:baber.azam@gmail.com)       | 700                       |
| Imran      | Khan      | [imran.khan@gmail.com](mailto:imran.khan@gmail.com)       | 200                       |

These records allow testing of all categorization conditions (High, Medium, and Low Value hires).

---

## 1. Full Name Formula

**Formula used**

```
{First Name} & " " & {Last Name}
```

**Explanation**

This formula concatenates the **First Name** and **Last Name** fields into a single field called **Full Name**, making it easier for HR teams to identify employees.

**Example Output**

- Touseef Hanif
- Baber Azam
- Imran Khan

---

## 2. Cleaned Email Formula

**Formula used**

```
LOWER(TRIM({Email Input}))
```

**Explanation**

This formula standardizes the email input by:

- Removing extra spaces using TRIM
- Converting all characters to lowercase using LOWER

This ensures that email addresses are stored in a consistent format.

**Example Output**

- touseef.hanif@gmail.com
- baber.azam@gmail.com
- imran.khan@gmail.com

---

## 3. Status Categorization Formula

**Formula used**

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

**Explanation**

This formula categorizes new hires based on the **amount spent on equipment**.

**Rules**

- Amount greater than 1000 → High Value
- Amount between 500 and 999 → Medium Value
- Amount less than 500 → Low Value

**Example Results**

| Employee      | Amount | Status       |
| ------------- | ------ | ------------ |
| Touseef Hanif | 1200   | High Value   |
| Baber Azam    | 700    | Medium Value |
| Imran Khan    | 200    | Low Value    |

---

## 4. Days Since Created Formula

**Formula used**

```
DATETIME_DIFF(TODAY(), {Created Date}, 'days')
```

**Explanation**

This formula calculates the number of days that have passed since the record was created.

This helps HR track how long a hire has been in the onboarding process.

---

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