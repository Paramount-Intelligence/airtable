* **Full Name Formula**: `{First Name} & " " & {Last Name}`
* **Cleaned Email Formula**: `TRIM({Email Input})`
* **Status Categorization Formula**: 
    `IF({Amount Spent on Equipment} > 1000, "High Value", IF({Amount Spent on Equipment} >= 500, "Medium Value", "Low Value"))`
* **Days Since Created Formula**: `DATETIME_DIFF(NOW(), {Created Date}, 'days')`
<img width="1391" height="918" alt="image" src="https://github.com/user-attachments/assets/ad22533b-908f-4b77-a15f-1a3117a837e8" />
