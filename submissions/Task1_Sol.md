**Candidate Information**

Full Name: Abdullah Khan

Email: abdullahejazkhan14@gmail.com

GitHub Profile Link: https://github.com/abdullahejazkhan

Submission Date: 2026-03-15





**Task 1 – Airtable Formula Implementation**

**Overview:**

The objective of Task 1 was to use formulas to manipulate raw onboarding data into a more structured and consumable format for the HR department.



**1. Full Name Formula**

**Formula:**

{First Name} \& " " \& {Last Name}

**Explanation:**

This formula concatenates the first and last name of an individual and inserts a space between them.



**2. Cleaned Email Formula**

**Formula:**

TRIM(LOWER({Email Input}))

**Explanation:**

This formula standardizes an individual’s email by removing any spaces and making it lowercase.



**3. Status Categorization Formula**

**Formula:**

IF({Amount Spent on Equipment} > 1000, "High Value", IF({Amount Spent on Equipment} >= 500, "Medium Value", "Low Value"))

**Explanation:**

This formula categorizes individuals into three categories: High Value, Medium Value and of Low Value, depending on their equipment expenditure.



**4. Days Since Created Formula**

**Formula:**

DATETIME\_DIFF(TODAY(), {Created Date}, 'days')

**Explanation:**

This formula calculates the number of days since an individual was created/registered.





Key Design Decisions:

* All formulas use TRIM() defensively to handle inconsistent data entry
* The Status Categorization uses nested IF rather than SWITCH for clarity and compatibility
* DATETIME\_DIFF with 'days' unit gives HR an always-current view of record age
* Email cleaning handles the most common real-world issues: spaces, commas and of case inconsistency

