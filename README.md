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
```
# SQL Question Solution

## Problem Statement
**For each doctor, display their ID, full name, and the first and last admission date they attended.**

The goal is to retrieve each doctor's ID, full name (concatenation of first and last name), and the earliest and latest admission dates they have attended.

## Solution Approach
To solve this problem, we will:

1. **Join Tables**: Use a `RIGHT JOIN` to combine the `admissions` and `doctors` tables, ensuring that all doctors are included, even if they haven't attended any admissions.

2. **Select Required Columns**: Extract the `doctor_id`, concatenate `first_name` and `last_name` to form the `fullname`, and use `MIN()` and `MAX()` to determine the first and last admission dates.

3. **Group the Results**: Group the results by `doctor_id` to calculate the first and last admission dates for each doctor.

4. **SQL Query**: The SQL query to implement this logic.

## SQL Query
```sql
SELECT 
    docDATA.doctor_id, 
    CONCAT(docDATA.first_name, ' ', docDATA.last_name) AS fullname, 
    MIN(docDATA.admission_date) AS firstAdmission, 
    MAX(docDATA.admission_date) AS lastAdmission   
FROM 
    (SELECT * 
     FROM admissions 
     RIGHT JOIN doctors 
     ON admissions.attending_doctor_id = doctors.doctor_id) AS docDATA
GROUP BY 
    docDATA.doctor_id;
```
