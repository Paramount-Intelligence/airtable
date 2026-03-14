# Task 1 Solution — Intermediate Airtable Skills

**Author:** Dileep Singh  
**Email:** baghirajput2326@gmail.com  
**Submission Date:** 2026-03-13

---

## Overview

This solution implements four formula fields in an Airtable New Hires table to clean, standardize, and categorize new hire onboarding data. All formulas use native Airtable formula syntax and require no external tools or integrations.

---

## Formula 1 — Full Name

**Purpose:** Combine First Name and Last Name into a single clean Full Name field.

**Formula:**
```
TRIM({First Name}) & " " & TRIM({Last Name})
```

**How it works:**
- `TRIM()` removes leading/trailing whitespace from both name fields
- `&` concatenates the two values with a space in between
- Result is always a clean, properly spaced full name

---

## Formula 2 — Cleaned Email

**Purpose:** Normalize email addresses by removing spaces, commas, and converting to lowercase.

**Formula:**
```
LOWER(TRIM(SUBSTITUTE(SUBSTITUTE({Email Input}, " ", ""), ",", "")))
```

**How it works:**
- Removes internal spaces from the email string
- Removes accidental commas
- Trims leading/trailing whitespace
- Converts to lowercase for consistency

---

## Formula 3 — Status Categorization

**Purpose:** Categorize new hires as High, Medium, or Low Value based on equipment spend.

**Formula:**
```
IF(
  {Amount Spent on Equipment} > 1000,
  "High Value",
  IF(
    AND({Amount Spent on Equipment} >= 500, {Amount Spent on Equipment} <= 999),
    "Medium Value",
    "Low Value"
  )
)
```

**Categorization logic:**
- Amount > 1000 → **High Value**
- Amount 500–999 → **Medium Value**
- Amount < 500 → **Low Value**

---

## Formula 4 — Days Since Created

**Purpose:** Calculate how many days have passed since the hire record was created.

**Formula:**
```
DATETIME_DIFF(TODAY(), {Created Date}, 'days')
```

**How it works:**
- `TODAY()` returns the current date (updates daily automatically)
- `DATETIME_DIFF()` calculates the difference between two dates
- Result is a live number that increases each day automatically

---

## Key Design Decisions

- All formulas use `TRIM()` defensively to handle inconsistent data entry
- The Status Categorization uses nested `IF` rather than `SWITCH` for clarity and compatibility
- `DATETIME_DIFF` with `'days'` unit gives HR an always-current view of record age
- Email cleaning handles the most common real-world issues: spaces, commas, and case inconsistency

See `formulas.md` for the full formula reference with examples and sample data table.
