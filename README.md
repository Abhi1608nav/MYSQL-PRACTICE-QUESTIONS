# MYSQL-PRACTICE-QUESTIONS
THIS REPO IS BUILT FOR MY MYSQL JOURNEY  AND TO CHECK  MY PROGRESS IN MYSQL . 

# MEDIUM LEVEL QUESTION 

## Problem Statement
**Show first_name, last_name, and the total number of admissions attended for each doctor.**

Every admission has been attended by a doctor.

## Solution Approach
To solve this problem, we will perform the following steps:

1. **Join the Tables**: Use a `RIGHT JOIN` to combine data from the `admissions` and `doctors` tables. This ensures that we get all records from the `doctors` table, even if they haven't attended any admissions.
   
2. **Select Required Columns**: We will select `first_name`, `last_name`, and count the number of admissions each doctor has attended.
   
3. **Group the Results**: Group the results by the `attending_doctor_id` to calculate the total number of admissions for each doctor.

4. **SQL Query**: The SQL query used to achieve the above steps.

## SQL Query
```sql
SELECT docDATA.first_name, docDATA.last_name, COUNT(docDATA.attending_doctor_id) AS total_admissions
FROM (
    SELECT * 
    FROM admissions 
    RIGHT JOIN doctors 
    ON admissions.attending_doctor_id = doctors.doctor_id
) AS docDATA 
GROUP BY docDATA.attending_doctor_id;
