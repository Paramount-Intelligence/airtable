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