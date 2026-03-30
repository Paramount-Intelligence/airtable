Task 1 Solution: Data Cleaning and Categorization

Overview
For this first task, I focused on getting the foundational data structured properly. New hire data can be pretty messy when it comes through initial forms, so my main goal was to clean up those inputs and automatically categorize candidates so the HR team has reliable data to work with.

How I Built It

1. The Data Structure
I set up an `Employees` table as the main hub. It catches the raw form submissions with the following fields:
Raw Name (Single line text)
Raw Email (Email)
Department (Single select)
Role (Single line text)
Start Date (Date)
Status (Dropdown: Pending, In Progress, Completed)
Documents Uploaded (Attachment)

2. The Logic (Formulas)
To fix inconsistencies and organize the pipeline, I added two formula fields:

Cleaning Emails (`Clean Email`): I used `LOWER(TRIM({Raw Email}))` to strip out accidental spaces and force everything to lowercase. This prevents errors later when we need to send automated emails.
Priority Routing (`Priority Level`): I wanted the system to automatically flag VIP hires. I wrote an `IF` statement (`IF(OR(FIND("Executive", {Role}), FIND("Director", {Role})), "High Value", "Standard")`) so that anyone coming in for a leadership role gets tagged as "High Value" right away.