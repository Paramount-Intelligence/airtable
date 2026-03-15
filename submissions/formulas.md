# Airtable Formulas

### 1. Full Name Formula
Concatenates First Name and Last Name.
```airtable
{First Name} & " " & {Last Name}
```

### 2. Cleaned Email Formula
Removes extra spaces, strips accidental special characters (commas, semicolons), and normalizes to lowercase.
```airtable
LOWER(TRIM(SUBSTITUTE(SUBSTITUTE({Email Input}, ",", ""), ";", "")))
```

### 3. Status Categorization Formula
Categorizes hires based on equipment spend.
```airtable
IF({Amount Spent on Equipment} > 1000, "High Value", 
  IF({Amount Spent on Equipment} >= 500, "Medium Value", 
    "Low Value"
  )
)
```

### 4. Days Since Created Formula
Calculates the age of the record.
```airtable
DATETIME_DIFF(NOW(), {Created Date}, 'days')
```

## Logic Explanations
- **Full Name**: Uses standard concatenation with a space separator.
- **Cleaned Email**: `TRIM` handles accidental leading/trailing spaces, and `LOWER` ensures unique matches in case-sensitive lookups.
- **Status**: Nested `IF` statements provide a clear hierarchy for spend-based priority.
- **Days Since Created**: Uses `DATETIME_DIFF` for an accurate integer count of days.
