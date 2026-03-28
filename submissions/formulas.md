# Task 1 — Airtable Formula Solutions

## 1. Full Name Formula

**Field Type:** Formula  
**Formula:**
```
TRIM({First Name}) & " " & TRIM({Last Name})
```

**Explanation:**  
`TRIM()` removes any accidental leading/trailing spaces from each name before joining them with a space. This ensures clean output even if the source data has padding.

---

## 2. Cleaned Email Formula

**Field Type:** Formula  
**Formula:**
```
LOWER(TRIM(SUBSTITUTE({Email Input}, " ", "")))
```

**Explanation:**  
- `SUBSTITUTE(..., " ", "")` — removes all spaces (including internal spaces like `user @domain.com`)
- `SUBSTITUTE(..., "")` — removes tab characters
- `TRIM()` — removes leading/trailing whitespace
- `LOWER()` — normalises to lowercase for consistent email formatting

---

## 3. Status Categorization Formula

**Field Type:** Formula  
**Formula:**
```
IF({Amount Spent on Equipment} > 1000, "High Value",
  IF({Amount Spent on Equipment} >= 500, "Medium Value",
    "Low Value"
  )
)
```

**Explanation:**  
Nested `IF()` statements evaluate in order:
1. If amount > 1000 → **High Value**
2. Else if amount >= 500 (i.e. 500–1000) → **Medium Value**
3. Else (amount < 500) → **Low Value**

---

## 4. Days Since Created Formula

**Field Type:** Formula  
**Formula:**
```
DATETIME_DIFF(TODAY(), {Created Date}, 'days')
```

**Explanation:**  
`DATETIME_DIFF()` calculates the difference between two dates in the specified unit (`'days'`). `TODAY()` returns the current date so the result updates dynamically every day.

---

## Notes

- All formulas assume the field names match exactly as described (case-sensitive in Airtable).
- The Status Categorization formula uses `>=500` for the Medium Value boundary, which captures amounts of exactly 500 (as "500–999" is inclusive of 500).
- The Cleaned Email formula handles the most common data quality issues (spaces, tabs, mixed case) but does not validate email format — a separate validation formula could be added if required.
