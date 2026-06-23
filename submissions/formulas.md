# Task 1 Solution: Airtable Formulas

## Candidate Information

- Full Name: Syeda Fariya Raza
- Email: sy.faraza2899@gmail.com
- GitHub Profile Link: https://github.com/FariyaR
- Submission Date: 2026-03-15

This document records the Task 1 formulas shown in the current `New Hires` screenshot set.

One important note: the captured Airtable build uses the field names `Email` and `Amount Spent on Equipment`, which differ slightly from the wording in the original task prompt.

## 1. Full Name Formula

**Field name:** `Full Name`

```text
TRIM(CONCATENATE({First Name}, " ", {Last Name}))
```

**Logic**

- Combines `First Name` and `Last Name` into one field.
- `CONCATENATE()` joins the values with a single space.
- `TRIM()` removes extra leading or trailing spaces.

**Screenshot evidence**

- [task1-formula-full-name.png](./screenshots/task1-formula-full-name.png)
- [task1-table-new-hires-with-formulas.png](./screenshots/task1-table-new-hires-with-formulas.png)

## 2. Cleaned Email Formula

**Field name:** `Cleaned Email`

```text
LOWER(TRIM({Email}))
```

**Logic**

- Uses the source `Email` field shown in the screenshot set.
- `TRIM()` removes extra spaces at the beginning or end of the email value.
- `LOWER()` standardizes the final output to lowercase.
- The captured formula does not perform additional cleanup beyond trimming and lowercasing.

**Note**

- The prompt refers to `Email Input`, but the captured build uses `Email`.

**Screenshot evidence**

- [task1-formula-cleaned-email.png](./screenshots/task1-formula-cleaned-email.png)
- [task1-table-new-hires-with-formulas.png](./screenshots/task1-table-new-hires-with-formulas.png)

## 3. Status Categorization Formula

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

**Logic**

- Checks the numeric equipment-spend amount for each new hire.
- Returns `High Value` when the amount is `1000` or higher.
- Returns `Medium Value` when the amount is `500` or higher and not already classified as high.
- Returns `Low Value` for amounts below `500`.

**Implementation note**

- The original prompt describes `High Value` as amount `> 1000`.
- The captured Airtable formula uses `>= 1000`.
- This document reflects the implemented formula visible in Airtable.

**Screenshot evidence**

- [task1-formula-status-categorization.png](./screenshots/task1-formula-status-categorization.png)
- [task1-table-new-hires-with-formulas.png](./screenshots/task1-table-new-hires-with-formulas.png)

## 4. Days Since Created Formula

**Field name:** `Days Since Created`

The formula editor for this field is not shown in the screenshot set, but the visible values in the table match the following formula:

```text
IF(
  {Created Date},
  DATETIME_DIFF(TODAY(), {Created Date}, 'days'),
  BLANK()
)
```

**Logic**

- Checks whether `Created Date` has a value.
- Uses `DATETIME_DIFF()` to calculate the number of days between `TODAY()` and the record's `Created Date`.
- Returns blank if the source date is empty.

**Why this formula is inferred**

- In the screenshot, `John Doe` has `Created Date = 2024-12-01` and `Days Since Created = 469`.
- That value matches the date difference through March 15, 2026, which is the workspace date for this submission.
- The rest of the visible rows follow the same pattern.

**Screenshot evidence**

- [task1-table-new-hires-with-formulas.png](./screenshots/task1-table-new-hires-with-formulas.png)

## Screenshot Coverage

The current Task 1 screenshot set includes:

- [task1-table-new-hires-with-formulas.png](./screenshots/task1-table-new-hires-with-formulas.png)
- [task1-formula-full-name.png](./screenshots/task1-formula-full-name.png)
- [task1-formula-cleaned-email.png](./screenshots/task1-formula-cleaned-email.png)
- [task1-formula-status-categorization.png](./screenshots/task1-formula-status-categorization.png)

The `Days Since Created` field is visible in the table screenshot, but a separate formula-editor screenshot for that field is not included.
