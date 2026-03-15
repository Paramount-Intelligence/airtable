# Task 1 — Airtable Formula Implementation

This document describes the formulas used in the New Hires table.

## 1. Full Name Formula

**Field Type:** Formula

**Formula:**

{First Name} & " " & {Last Name}

**Logic:**

This formula concatenates the First Name and Last Name fields with a space between them to generate the employee's full name.

---

## 2. Cleaned Email Formula

**Field Type:** Formula

**Formula:**

LOWER(TRIM({Email Input}))

**Logic:**

- TRIM() removes leading and trailing spaces from the email input.
- LOWER() converts the email address to lowercase to maintain consistent formatting.

This ensures email addresses are standardized and free of extra spaces.

---

## 3. Status Categorization Formula

**Field Type:** Formula

**Formula:**

IF(
{Amount Spent on Equipment} > 1000,
"High Value",
IF(
{Amount Spent on Equipment} >= 500,
"Medium Value",
"Low Value"
))

**Logic:**

The formula categorizes each hire based on the equipment spending amount.

- Amount greater than 1000 → High Value
- Amount between 500 and 999 → Medium Value
- Amount less than 500 → Low Value

---

## 4. Days Since Created Formula

**Field Type:** Formula

**Formula:**

DATETIME_DIFF(TODAY(), {Created Date}, 'days')

**Logic:**

This formula calculates the number of days between the current date and the record's Created Date.

It helps track how long the record has existed in the system.