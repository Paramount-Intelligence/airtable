# Candidate Submission

## Candidate Information
- Full Name: Adeeb Ur Rahman
- Email: adeeburrahmankhuhro@gmail.com
- LinkedIn: www.linkedin.com/in/adeeb-ur-rahman
- Submission Date: 17-03-2026

## Task 1: Intermediate Airtable Skills

### 1. Full Name Formula
```airtable
TRIM({First Name} & " " & {Last Name})
```

### 2. Cleaned Email Formula
```airtable
TRIM(LOWER({Email Input}))
```

### 3. Status Categorization Formula
```airtable
IF({Amount Spent on Equipment} > 1000, "High Value", IF({Amount Spent on Equipment} >= 500, "Medium Value", "Low Value"))
```

### 4. Days Since Created Formula
```airtable
DATETIME_DIFF(TODAY(), {Created Date}, 'days')
```

## Task 2: Advanced Airtable Automation

### 1. Automation Steps

![Automation Setup](Screenshots/Eamil%20Automation.png)

1. **Trigger**: "When a record matches conditions" - The target table is the "New Hires" table, and the condition is `{Status Categorization} = "High Value"`.
2. **Conditional Logic (Branching)**: 
   - **Condition A (Valid Email)**: Check if `{Cleaned Email}` is not empty AND contains `@`.
   - **Condition B (Invalid/Missing Email)**: Check if `{Cleaned Email}` is empty OR does not contain `@`.
3. **Action (Valid Email)**: Send a dynamic notification (Slack or Email). The message can say: "New High Value hire: {Full Name}. Equipment cost: ${Amount Spent on Equipment}."
4. **Action (Invalid Email)**: Send a notification to HR to correct the email for {Full Name}.
5. **Action (Log to Tracking Table)**: "Create record" in the Tracking Table using the {Full Name}, {Created Date}, and {Amount Spent on Equipment}.

### 2. Interface Design

![Dashboard Interface](Screenshots/Dashboard%20Interface.png)

- **Layout Explanation**: The interface uses a Dashboard layout. At the top, there are three **Number (Summary) Tiles** summarizing the count of High, Medium, and Low Value hires using conditional filtering. Below the tiles, a **Grid element** displays only "High Value" hires. Clicking on a record in the grid opens a **Detail View** showing all fields (Full Name, Cleaned Email, Equipment Amount, etc.) for that specific new hire.

### 3. Formula Logic
For branching on email validity within the automation:
- Using Airtable's built-in condition builder: `{Cleaned Email} is not empty` and `{Cleaned Email} contains "@"`
- Or alternatively, if using a formula condition: `FIND("@", {Cleaned Email}) > 0`

### 4. Assumptions
- The "Tracking Table" is a separate table in the same base.
- Notification integrations (Slack/Email) are already authenticated in the workspace.
- The "Created Date" is a native Created Time field.

### 5. Optional Notes
The formulas were kept simple and robust. `TRIM` and `LOWER` ensure data cleanliness.
