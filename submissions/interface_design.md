# HR Dashboard Interface Design

## 1. Summary Tiles (Top Row)
- **High Value Hires**: Displays the count of records where `Status Categorization` = "High Value".
- **Medium Value Hires**: Displays the count of records where `Status Categorization` = "Medium Value".
- **Low Value Hires**: Displays the count of records where `Status Categorization` = "Low Value".

## 2. Filtered Grid (Center)
- **View Name**: "Priority Onboarding Queue"
- **Filter**: Only show records where `Status Categorization` = "High Value".
- **Columns**: Full Name, Email, Amount Spent, Created Date, Days Since Created.

## 3. Detail View (Side/Modal)
- Allows HR to click any record to see full details including:
  - Personal Info (Full Name, Cleaned Email)
  - Financials (Equipment Amount)
  - Metadata (Created Date, Days Elapsed)

## 4. Visual Elements
- Use color-coded labels for different value categories (e.g., Red for High, Yellow for Medium, Green for Low).
- Include a "Refresh" button or ensure real-time sync is enabled for the dashboard.
