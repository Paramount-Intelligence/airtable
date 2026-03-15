# Candidate Submission Template

## Candidate Information
- Full Name: Omer F
- Email: omer@example.com
- LinkedIn or Portfolio: 
- Submission Date: 2026-03-14

## Task 1: Intermediate Airtable Skills

### 1. Full Name Formula
```airtable
{First Name} & " " & {Last Name}
```
Concatenates First Name and Last Name with a space separator.

### 2. Cleaned Email Formula
```airtable
LOWER(TRIM(SUBSTITUTE(SUBSTITUTE({Email Input}, ",", ""), ";", "")))
```
Removes extra spaces with `TRIM`, strips accidental commas/semicolons with `SUBSTITUTE`, and normalizes to lowercase with `LOWER`.

### 3. Status Categorization Formula
```airtable
IF({Amount Spent on Equipment} > 1000, "High Value",
  IF({Amount Spent on Equipment} >= 500, "Medium Value",
    "Low Value"
  )
)
```
Uses nested `IF` statements: >1000 = High Value, 500-1000 = Medium Value, <500 = Low Value.

### 4. Days Since Created Formula
```airtable
DATETIME_DIFF(NOW(), {Created Date}, 'days')
```
Calculates integer days between the Created Date and the current time.

## Task 2: Advanced Airtable Automation

### 1. Automation Steps
**Trigger**: When a record in `New Hires` table is created or updated and the `Status Categorization` formula field equals `"High Value"`.

**Action 1 - Slack/Email Notification**:
- Send a dynamic Slack/Email notification to the HR channel:
  - Message: "🚨 New High Value hire: **{Full Name}** ({Cleaned Email}). Equipment Spend: ${Amount Spent on Equipment}. Please prioritize their onboarding setup."

**Action 2 - Log to Tracking Table**:
- Create a new record in the `Tracking Table`:
  - Hire Name: `{Full Name}`
  - Priority Level: `"Urgent"`
  - Logged At: `{Created Date}`
  - Link to New Hires: Link to the original record

**Action 3 - Conditional Branching**:
- **If** `Cleaned Email` is empty OR does not contain `"@"`:
  - Create a task in Airtable for HR: "Manually verify email for {Full Name}"
  - Skip sending the email notification
- **Else**: Proceed with the standard Slack/Email notification

### 2. Interface Design
The interface is designed as an HR dashboard with three main sections:

1. **Summary Tiles (Top Row)**: Three tiles showing counts of High/Medium/Low Value hires using `COUNTIF` logic filtered on the `Status Categorization` field. Color-coded: Red for High, Yellow for Medium, Green for Low.

2. **Filtered Grid (Center)**: A grid view titled "Priority Onboarding Queue" filtered to show only "High Value" records. Columns displayed: Full Name, Cleaned Email, Amount Spent, Created Date, Days Since Created.

3. **Detail View (Right Panel/Modal)**: Clicking any record shows full details including personal info (Full Name, Email), financials (Equipment Amount, Status), and timing metadata (Created Date, Days Elapsed).

*Note: Screenshots would be provided from a configured Airtable base. The interface layout described above follows Airtable's Interface Designer with Summary, Grid, and Record Detail components.*

### 3. Formula Logic
The automation uses the same `Status Categorization` formula from Task 1 as the trigger condition. Additionally, the email validation check uses:
```
IF(OR(LEN({Cleaned Email}) = 0, FIND("@", {Cleaned Email}) = 0), TRUE(), FALSE())
```

### 4. Assumptions
- The `Tracking Table` exists as a separate table with a linked record field back to `New Hires`.
- Slack integration is pre-configured with the appropriate workspace and channel.
- The Airtable automation runs on record creation and on field update (for when `Amount Spent on Equipment` changes).
- The interface auto-refreshes or Airtable sync is enabled.

### 5. Optional Notes
- The interface could be extended with a chart showing spend distribution over time.
- A webhook could be added to notify an external system when High Value hires are detected.
