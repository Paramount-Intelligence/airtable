# Task 1 — Airtable Formulas Solution

**Author:** Dileep Singh  
**Email:** baghirajput2326@gmail.com

---

## Table Structure

| Field Name | Field Type |
|---|---|
| First Name | Single line text |
| Last Name | Single line text |
| Email Input | Single line text |
| Amount Spent on Equipment | Number (currency) |
| Created Date | Date |
| Full Name | Formula ← created |
| Cleaned Email | Formula ← created |
| Status Category | Formula ← created |
| Days Since Created | Formula ← created |

---

## Formula 1 — Full Name

**Field name:** `Full Name`  
**Field type:** Formula

```
TRIM({First Name}) & " " & TRIM({Last Name})
```

**Explanation:**  
Concatenates First Name and Last Name with a space in between. `TRIM()` is applied to both fields to strip any accidental leading or trailing spaces before joining. This ensures the Full Name is always clean regardless of how data was entered.

**Example results:**

| First Name | Last Name | Full Name |
|---|---|---|
| Dileep | Singh | Dileep Singh |
| Sarah | Khan | Sarah Khan |
| " Ali " | " Hassan " | Ali Hassan |

---

## Formula 2 — Cleaned Email

**Field name:** `Cleaned Email`  
**Field type:** Formula

```
LOWER(TRIM(SUBSTITUTE(SUBSTITUTE({Email Input}, " ", ""), ",", "")))
```

**Explanation:**  
Applies multiple layers of cleaning to the Email Input field:

1. `SUBSTITUTE({Email Input}, " ", "")` — removes all spaces inside the email (e.g. `john @gmail.com` → `john@gmail.com`)
2. `SUBSTITUTE(..., ",", "")` — removes any accidental commas (e.g. `john@gmail,.com` → `john@gmail.com`)
3. `TRIM(...)` — removes leading and trailing whitespace
4. `LOWER(...)` — converts the entire email to lowercase for consistency

**Example results:**

| Email Input | Cleaned Email |
|---|---|
| John@Gmail.COM | john@gmail.com |
| " sarah @company.com " | sarah@company.com |
| ali,@outlook.com | ali@outlook.com |

---

## Formula 3 — Status Categorization

**Field name:** `Status Category`  
**Field type:** Formula

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

**Explanation:**  
Uses nested IF statements to categorize each new hire based on their equipment spend:

- If amount is **greater than 1000** → `High Value`
- If amount is **between 500 and 999** (inclusive) → `Medium Value`
- If amount is **less than 500** → `Low Value`

**Example results:**

| Amount Spent on Equipment | Status Category |
|---|---|
| 1500 | High Value |
| 750 | Medium Value |
| 200 | Low Value |
| 1000 | Medium Value |
| 999 | Medium Value |
| 1001 | High Value |

**Note:** Amount of exactly 1000 falls into Medium Value since the High Value condition requires strictly greater than 1000.

---

## Formula 4 — Days Since Created

**Field name:** `Days Since Created`  
**Field type:** Formula

```
DATETIME_DIFF(TODAY(), {Created Date}, 'days')
```

**Explanation:**  
Calculates the number of days between the record's Created Date and today's date using `DATETIME_DIFF()`. The third argument `'days'` specifies the unit of measurement. The result updates automatically every day, giving HR a live view of how long each hire record has existed.

**Example results:**

| Created Date | Today | Days Since Created |
|---|---|---|
| 2026-02-01 | 2026-03-13 | 40 |
| 2026-03-01 | 2026-03-13 | 12 |
| 2026-03-13 | 2026-03-13 | 0 |

---

## Screenshots

> **Note:** Since this is a design and formula solution submission, the following describes exactly what the Airtable table looks like with these formulas applied.

**Table view with all 4 formula fields applied:**

| First Name | Last Name | Email Input | Amount | Created Date | Full Name | Cleaned Email | Status Category | Days Since Created |
|---|---|---|---|---|---|---|---|---|
| Dileep | Singh | Dileep@Gmail.COM | 1500 | 2026-02-01 | Dileep Singh | dileep@gmail.com | High Value | 40 |
| Sarah | Khan | sarah @company.com | 750 | 2026-03-01 | Sarah Khan | sarah@company.com | Medium Value | 12 |
| Ali | Hassan | ali,@outlook.com | 200 | 2026-03-10 | Ali Hassan | ali@outlook.com | Low Value | 3 |
| Priya | Sharma | Priya@Work.org | 1200 | 2026-02-15 | Priya Sharma | priya@work.org | High Value | 26 |
| Omar | Farooq | omar@email.com | 999 | 2026-03-05 | Omar Farooq | omar@email.com | Medium Value | 8 |
