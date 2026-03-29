# Task 2 — Advanced Airtable Automation

## Candidate Information
- **Full Name:** Khawaja Zeeshan
- **Email:** khawajazeeshan225@gmail.com
- **LinkedIn or Portfolio:** https://personal-portfolio-swart-xi.vercel.app/
- **Submission Date:** [14 March 2026]

---

## Automation Steps

### 1. Form Submission → Trigger
- When a new hire form is submitted (or dummy data is created), the automation **is triggered**.  
- This ensures that the workflow starts automatically.

### 2. AI Data Extraction → Process Data
- In the Python code, the `new_hire` dictionary extracts **name, email, and department**.  
- In a real scenario, this AI node would clean the input data and convert it into a standard format.

### 3. Task Routing → Automation
- The system decides which **HR member to assign** and logs the record in a **tracking table**.  
- This ensures the workflow remains **organized and automated**.

### 4. Onboarding Plan Generation → AI
- AI generates a **personalized onboarding plan**.  
- Example (from Python code): `"Welcome John Doe to Engineering!"`  
- In a real scenario, it could generate detailed tasks, training sessions, and resources for the new hire.

### 5. Notifications → Email / Slack
- The system sends a **dynamic notification** to HR including the Name, Department, and Onboarding Plan.  
- If the email is missing or invalid → HR is alerted, or a follow-up task is created.

---

## Formula / Logic (Optional)
- Example Python conditional check for missing email:
```python
if new_hire["email"] == "":
    print("Email missing: notify HR")