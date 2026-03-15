# Candidate Submission

## Candidate Information
- Full Name: Syeda Fariya Raza
- Email: sy.faraza2899@gmail.com
- LinkedIn or Portfolio: https://github.com/FariyaR
- Submission Date: 2026-03-15

## Task 1: Intermediate Airtable Skills

### 1. Full Name Formula

**Field name:** `Full Name`

```text
TRIM(CONCATENATE({First Name}, " ", {Last Name}))
```

This formula combines `First Name` and `Last Name` into one clean full-name field.

Supporting screenshots:
- [task1-formula-full-name.png](./screenshots/task1-formula-full-name.png)
- [task1-table-new-hires-with-formulas.png](./screenshots/task1-table-new-hires-with-formulas.png)

### 2. Cleaned Email Formula

**Field name:** `Cleaned Email`

```text
LOWER(TRIM({Email}))
```

This formula trims extra spaces and normalizes the email value to lowercase.

Implementation note:
- The prompt refers to `Email Input`, but the captured Airtable build uses `Email`.
- The captured formula only trims and lowercases; it does not apply extra character cleanup.

Supporting screenshots:
- [task1-formula-cleaned-email.png](./screenshots/task1-formula-cleaned-email.png)
- [task1-table-new-hires-with-formulas.png](./screenshots/task1-table-new-hires-with-formulas.png)

### 3. Status Categorization Formula

**Field name:** `Status Categorization`

```text
IF(
  {Amount Spent on Equipment} >= 1000,
  "High Value",
  IF(
    {Amount Spent on Equipment} >= 500,
    "Medium Value",
    "Low Value"
  )
)
```

This formula categorizes each hire based on equipment spend.

Implementation note:
- The original prompt describes `High Value` as amount `> 1000`.
- The captured Airtable formula uses `>= 1000`.
- This submission reflects the implemented formula shown in Airtable.

Supporting screenshots:
- [task1-formula-status-categorization.png](./screenshots/task1-formula-status-categorization.png)
- [task1-table-new-hires-with-formulas.png](./screenshots/task1-table-new-hires-with-formulas.png)

### 4. Days Since Created Formula

**Field name:** `Days Since Created`

```text
IF(
  {Created Date},
  DATETIME_DIFF(TODAY(), {Created Date}, 'days'),
  BLANK()
)
```

This formula calculates the number of days between `Created Date` and the current date.

Implementation note:
- The formula editor for this field is not shown in the screenshot set.
- The formula above is inferred from the displayed values in the table screenshot.
- For example, `Created Date = 2024-12-01` and `Days Since Created = 469` matches the workspace date of March 15, 2026.

Supporting screenshot:
- [task1-table-new-hires-with-formulas.png](./screenshots/task1-table-new-hires-with-formulas.png)

## Task 2: Advanced Airtable Automation

### 1. Automation Steps

The Airtable automation uses `When record matches conditions` with the condition:

- `Status Categorization is "High Value"`

The core flow shown in the screenshots is:

1. Trigger when a record becomes `High Value`
2. Send an email notification
3. Create a record in `High Value Tracking`

The final workflow also adds conditional branching using `Email Check Status`:

- If `Email Check Status is Not Valid`
  - send an email to `hr@company.com`
  - create a record in `High Value Tracking`
- Otherwise if `Email Check Status is Valid`
  - send an email to `hr@company.com`
  - create a record in `High Value Tracking`

This satisfies the Task 2 requirements for:
- a high-value trigger
- HR notification
- tracking-table logging
- conditional branching for invalid or missing email cases

Supporting screenshots:
- [task2-automation-basic-workflow.png](./screenshots/task2-automation-basic-workflow.png)
- [task2-automation-invalid-email-branch.png](./screenshots/task2-automation-invalid-email-branch.png)
- [task2-automation-email-check-branches.png](./screenshots/task2-automation-email-check-branches.png)
- [task2-automation-final-branching-workflow.png](./screenshots/task2-automation-final-branching-workflow.png)
- [task2-automation-repeat-for-each.png](./screenshots/task2-automation-repeat-for-each.png)

### 2. Interface Design

The interface screenshot shows a `Dashboard` page for the `New Hires` base.

It includes:
- a `Total Count` tile showing `10`
- a `High Value Hires` tile showing `3`
- a `Medium Value Hires` tile showing `5`
- a `Low Value Hires` tile showing `2`
- a donut chart summarizing the high-value set
- a filtered grid listing the three high-value hires:
  - `Lucas Brown`
  - `John Doe`
  - `Emily Wong`

Visible grid columns include:
- `First Name`
- `Last Name`
- `Full Name`
- `Email`

This satisfies the summary-tile and filtered-grid requirements from the prompt.

Detail-view note:
- A separate detail-view screenshot is not included.
- In Airtable, this is typically handled by selecting a grid row and opening the record details panel.

Supporting screenshot:
- [task2-interface-dashboard.png](./screenshots/task2-interface-dashboard.png)

### 3. Formula Logic

Task 2 depends on the Task 1 high-value classification formula:

```text
IF(
  {Amount Spent on Equipment} >= 1000,
  "High Value",
  IF(
    {Amount Spent on Equipment} >= 500,
    "Medium Value",
    "Low Value"
  )
)
```

The automation also branches on a helper field called `Email Check Status`. Its field configuration is not shown directly, so the following formula is inferred from the branch labels in the automation screenshots:

```text
IF(
  {Cleaned Email},
  IF(
    REGEX_MATCH(
      {Cleaned Email},
      "^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}$"
    ),
    "Valid",
    "Not Valid"
  ),
  "Not Valid"
)
```

### 4. Assumptions

- The final submission is based primarily on [task2-automation-final-branching-workflow.png](./screenshots/task2-automation-final-branching-workflow.png), because it is the most complete automation screenshot.
- The other automation screenshots appear to show intermediate build stages.
- The `Email Check Status` formula is inferred from the visible condition labels because the field configuration is not shown directly.
- The dashboard screenshot clearly covers summary tiles and a filtered grid, but a standalone detail-view screenshot is not included.
- The tracking table is confirmed by the `Create record` action label `In High Value Tracking`.

### 5. Optional Notes

- The captured Airtable build uses `Email` and `Amount Spent on Equipment` as field names, which differ slightly from the prompt wording.
- The Task 1 `Days Since Created` formula is documented from observed table output because its formula editor was not captured.
- The three previous standalone submission docs have been consolidated into this single template-based submission file.
