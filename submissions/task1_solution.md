# Task 1 – Airtable Formula Implementation

## Overview

The objective of Task 1 was to transform raw onboarding data into structured and usable HR information using Airtable formulas.

These formulas help normalize input data, categorize hires based on equipment spending, and track the age of each onboarding record.

---

## 1. Full Name Formula

**Formula**

{First Name} & " " & {Last Name}

**Explanation**

Concatenates first and last name with a space in between.

---

## 2. Cleaned Email Formula

**Formula**

TRIM(LOWER({Email Input}))

**Explanation**

Standardizes email by removing spaces and converting to lowercase.

---

## 3. Status Categorization Formula

**Formula**

IF({Amount Spent on Equipment} > 1000, "High Value", IF({Amount Spent on Equipment} >= 500, "Medium Value", "Low Value"))

**Explanation**

Categorizes hires into High, Medium, or Low Value based on equipment spending.

---

## 4. Days Since Created Formula

**Formula**

DATETIME_DIFF(TODAY(), {Created Date}, 'days')

**Explanation**

Calculates number of days since record was created.