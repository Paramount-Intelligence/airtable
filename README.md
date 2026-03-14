# Airtable HR Onboarding Automation Dashboard

This project demonstrates how Airtable can be used to build an HR onboarding management system that combines structured data handling, formula-based data processing, automation workflows, and a visual dashboard for HR teams. The system processes new hire data, categorizes candidates, triggers automated workflows for high-value hires, and provides a centralized dashboard interface for HR visibility.

The objective of this exercise is to showcase the practical use of Airtable formulas, automations, and interfaces to solve real-world HR operational challenges.

## Project Outcome

The implemented solution transforms raw onboarding data into a structured workflow for HR operations. Key outcomes include:
* **Automated cleaning and categorization** of new hire data using Airtable formulas.
* **Identification of high-value hires** through calculated fields.
* **Automation triggers** for important onboarding events.
* **A centralized HR dashboard** for monitoring onboarding progress.
* **Improved operational visibility** for HR teams managing multiple hires.

The system demonstrates how Airtable can act as a lightweight operations platform for HR onboarding processes.

---

## System Overview

The onboarding system is built entirely using Airtable's native capabilities:
* **Data Layer:** Airtable tables store records for new hires and onboarding data.
* **Logic Layer:** Formula fields process and categorize employee information.
* **Automation Layer:** Airtable automations trigger actions when specific conditions are met.
* **Interface Layer:** Airtable Interface Designer provides a dashboard for HR teams to monitor onboarding activity.

---

## Task 1: Data Cleaning and Categorization

Formulas were implemented to transform and standardize new hire records submitted through the onboarding table.

### Capabilities Implemented:
* **Full Name Integration:** `{First Name} & " " & {Last Name}` seamlessly combines names.
* **Email Standardization:** `LOWER(TRIM({Email Input}))` ensures consistent format.
* **Status Categorization:** Identifies "High Value", "Medium Value", and "Low Value" candidates based on onboarding equipment spend (>$1000 = High, $500-$999 = Medium, <$500 = Low).
* **Onboarding Tracking:** `DATETIME_DIFF(TODAY(), {Created Date}, 'days')` tracks pipeline progress.

These formulas help convert raw onboarding submissions into structured and actionable HR data.

---

## Task 2: Automation and HR Dashboard

### Automation Workflow
An automation workflow was implemented to handle high-value hires:
1. **Trigger:** Detect records classified as "High Value" hires.
2. **Conditional Branching:** Verifies if an email is present.
   - *If Email Available:* Notifies HR and logs the record in the **High Value Tracking** table.
   - *If Email Missing:* Sends an alert that the high-value hire lacks a valid email.
3. **Tracking Log:** Automates entry into the High Value Tracking table for ongoing monitoring.

### HR Dashboard Interface
Built using Airtable Interface Designer to provide real-time operational visibility:
* **Summary Tiles:** Displays instant counts of High, Medium, and Low Value hires.
* **Filtered Grid View:** Focused view strictly on High Value hires for immediate HR review.
* **Detail View:** Complete onboarding profiles allowing staff to view Name, Email, Equipment Spend, Status, and Days Since Created.

---

##  Implementation Screenshots

The `assets/screenshots/` directory contains comprehensive visual proof of the Airtable base operations, field configurations, automation logic, and interface designs. 

### Selected Previews:

<details>
<summary>Click to view all screenshot references</summary>

- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 214119.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 214524.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 214740.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 214749.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 214830.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 215022.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 215111.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 215304.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 215322.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 220021.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 220630.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 221032.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 221235.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 221329.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 221408.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 221547.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 221553.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 221611.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 222135.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 222140.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 222346.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 222727.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 222821.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 224742.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 224814.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 224838.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-12 224844.png>)
- ![Screenshot](<./assets/screenshots/Screenshot 2026-03-14 132659.png>)
</details>

---

##  Potential Improvements

Future enhancements for this system may include:
* Integration with external HRIS systems.
* Slack or email alerts for onboarding milestones.
* Automated onboarding task tracking.
* Employee lifecycle management beyond onboarding.
* HR analytics and reporting dashboards.

---

##  Author

**Touseef Hanif**
* LinkedIn: https://www.linkedin.com/in/touseefhanif
* GitHub: https://github.com/touseefh/hr-onboarding-automation-system
