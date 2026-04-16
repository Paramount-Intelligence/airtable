# Submission Template

**Full Name:** Mohammed Ali
**Email:** mohammedali5072008@gmail.com
**GitHub:** [MohammadAli-14](https://github.com/MohammadAli-14) | [Muhammad5Ali](https://github.com/Muhammad5Ali)
**LinkedIn:** [mohammedali-dev](https://www.linkedin.com/in/mohammedali-dev/)
**Portfolio:** [mohammedali.dev](https://www.mohammedali.dev/)
**Submission Date:** March 18, 2026

---

## Task 1 — Data Cleaning and Categorization

Completed. See `task1_solution.md`.

Six Airtable formula fields implemented:
- **Cleaned Name** — standardizes inconsistent text capitalization
- **Email Domain** — extracts domain from email for validation
- **Seniority Level** — categorizes by role keywords (Senior / Mid Level / Entry Level)
- **Priority Category** — High Value / Standard / Entry Level based on salary + role
- **Days Until Start** — urgency calculation from today's date
- **Hire Quarter** — Q1/Q2/Q3/Q4 grouping by start date month

Five custom views created for HR team filtering and monitoring:
1. All Hires — default grid view
2. High Value Hires — filtered by Priority Category
3. Starting This Month — filtered by Days Until Start
4. By Department — grouped by Department field
5. Onboarding Pipeline — grouped by Onboarding Status

---

## Task 2 — Automation and HR Dashboard

Completed. See `task2_solution.md`.

**Airtable Automation configured:**
- Trigger: record matches condition → Priority Category = "High Value"
- Action 1: Update Onboarding Status field → "In Progress"
- Action 2: Send email alert to HR team with full employee details

**Interface Designer Dashboard built with 3 pages:**
- Page 1: Onboarding Overview — summary metrics, kanban pipeline, high value hires table
- Page 2: Department Analytics — bar chart, seniority pie chart, upcoming starts calendar
- Page 3: Individual Hire Records — editable profile view with HR notes

---

## Assumptions

- Airtable free tier used (no paid external integrations required)
- Sample data added manually to demonstrate formula and automation behavior
- High Value hire threshold: salary >= $100,000 OR role contains Senior/Director/Manager
- Onboarding scope covers Day 0 pre-arrival setup only
- Screenshots represent live Airtable environment behavior