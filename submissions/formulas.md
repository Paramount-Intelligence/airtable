* **Full Name Formula**: `{First Name} & " " & {Last Name}`
* **Cleaned Email Formula**: `TRIM({Email Input})`
* **Status Categorization Formula**: 
    `IF({Amount Spent on Equipment} > 1000, "High Value", IF({Amount Spent on Equipment} >= 500, "Medium Value", "Low Value"))`
* **Days Since Created Formula**: `DATETIME_DIFF(NOW(), {Created Date}, 'days')`

