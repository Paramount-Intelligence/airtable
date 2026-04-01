# Task 1: Airtable Formulas

## 1. Full Name Formula
```airtable
TRIM({First Name} & " " & {Last Name})
```
*Concatenates the First Name and Last Name with a space in between, and trims any extra whitespace.*

## 2. Cleaned Email Formula
```airtable
TRIM(LOWER({Email Input}))
```
*Removes leading/trailing spaces and converts the email to lowercase for consistency.*

## 3. Status Categorization Formula
```airtable
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
*Categorizes the record based on the numeric value in the Amount Spent on Equipment field.*

## 4. Days Since Created Formula
```airtable
DATETIME_DIFF(TODAY(), {Created Date}, 'days')
```
*Calculates the difference in days between the current date and the record's Created Date.*

## Screenshots
- **Full Name Column:**
  ![Full Name column](Screenshots/Full%20Name%20column.png)

- **Email Column:**
  ![Email column](Screenshots/Email%20column.png)

- **Status Column:**
  ![Status column](Screenshots/Status%20column.png)

- **Days Since Created Column:**
  ![Days Since Created column](Screenshots/Days%20Since%20Created%20column.png)
