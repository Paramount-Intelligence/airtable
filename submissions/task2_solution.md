Task 2 Solution: Automation and HR Dashboard

Overview
Building on the structured data from Task 1, I put together the automation and visual dashboard. The idea here is to get rid of manual tracking and give the HR team a clear, real-time look at where everyone is in the onboarding process.

How I Built It:

 1. The Automation Workflow
I set up a native Airtable automation to handle our VIP candidates so they don't slip through the cracks.
* The Trigger: The workflow watches the `Employees` table. Whenever a new or updated record gets tagged as "High Value" in the Priority Level field, the automation kicks off.
* The Action: It automatically sends an email alert to the HR team. I used dynamic fields to drop in the candidate's name and clean email, letting the team know they need to fast-track this specific onboarding.

 2. The HR Dashboard
I used Airtable's Interface Designer to build a clean, centralized view for the team. The dashboard includes:
* Total Hires: A simple number widget showing the total count of candidates in the pipeline.
* Department Breakdown:** A chart that groups incoming hires by department, which helps HR see where the bulk of their workload is going.
* Priority Queue: A filtered grid view that *only* shows candidates flagged as "High Value." This way, the team has a dedicated space to manage expedited onboarding without getting distracted by the rest of the list.