## 1. Automation Steps
To streamline the onboarding of priority candidates, I built the following automation:
* **Trigger**: The workflow triggers automatically when a record in the **New Hires** table is updated to "High Value" based on the equipment spend formula.
* **Conditional Branching (Data Integrity)**:
    * **Branch A (Email Present)**: If the `Cleaned Email` field contains a valid entry, the system proceeds to the next steps.
    * **Branch B (Email Missing)**: If the email field is empty, the system sends an urgent alert to the HR Slack channel titled "Missing Data: Action Required".
* **Action - Slack/Email Notification**: A dynamic message is sent to the HR team including the hire's Full Name and Department.
* **Action - Logging**: The automation automatically creates a new record in a separate **Tracking Table** to maintain a permanent log of all high-priority onboarding events.

## 2. Interface Design
I designed a centralized HR Dashboard with the following components:
* **Summary Tiles**: Three large numeric displays at the top showing the current count of **High**, **Medium**, and **Low** value hires for a quick workload overview.
* **Filtered Grid**: A dedicated section that displays only hires marked as **High Value**, ensuring the team prioritizes these records first.
* **Detail View**: A detailed sidebar that expands when a hire is selected, showing their Full Name, Cleaned Email, and Equipment Amount.

## 3. Formula Logic
The automation relies on the **Status Categorization** formula from Task 1 to trigger:
`IF({Amount Spent on Equipment} > 1000, "High Value", IF({Amount Spent on Equipment} >= 500, "Medium Value", "Low Value"))`.

## 4. Assumptions
* I assumed that "High Value" hires require a faster response time, justifying the use of instant Slack notifications.
* I assumed the "Tracking Table" should be used for auditing purposes rather than daily active management.
