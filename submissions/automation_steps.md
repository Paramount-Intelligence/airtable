# Automation Steps

### 1. Trigger
- **Condition**: When a record in the `New Hires` table matches conditions.
- **Filter**: `Status Categorization` (formula field) is equal to `High Value`.

### 2. Action: Notify HR
- **Method**: Slack or Email.
- **Message**: 
  "A new High Value hire HAS BEEN IDENTIFIED: **{Full Name}** ({Cleaned Email}). 
  Equipment Spend: ${Amount Spent on Equipment}. 
  Please prioritize their onboarding setup."

### 3. Action: Log to Tracking Table
- **Method**: Create Record.
- **Target Table**: `Tracking Table`.
- **Fields**: 
  - `Hire Name`: {Full Name}
  - `Priority Level`: "Urgent"
  - `Logged At`: Created Time

### 4. Conditional Branching (Advanced)
- **Condition**: If `Cleaned Email` is empty or does not contain "@".
- **Action**: Create a Task in Airtable for HR to "Manually verify email for {Full Name}".
- **Else**: Proceed with standard notification.

## Assumptions
- The `Tracking Table` already exists with a link to the `New Hires` table.
- Slack integration is configured with appropriate channel permissions.
