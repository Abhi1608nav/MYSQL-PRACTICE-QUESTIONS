# MYSQL-PRACTICE-QUESTIONS
THIS REPO IS BUILT FOR MY MYSQL JOURNEY  AND TO CHECK  MY PROGRESS IN MYSQL . 

# MEDIUM LEVEL QUESTION 

## Problem Statement 1
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

## Problem Statement 2
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
## Problem Statement 3
Display the total number of patients for each province, ordered by the count in descending order.

## Solution Approach
To solve this problem, the following steps were taken:
1. **Join Tables**: Use an `INNER JOIN` to combine data from the `patients` and `province_names` tables.
2. **Select Columns**: Retrieve the `province_name` and count the number of patients for each province.
3. **Group and Order Results**: Group the results by `province_name` and order them by the patient count in descending order.

## SQL Query
```sql
SELECT 
    patientsProvinceData.province_name, 
    COUNT(patientsProvinceData.province_name) AS patientsCount 
FROM 
    (SELECT * 
     FROM patients 
     JOIN province_names 
     ON patients.province_id = province_names.province_id) AS patientsProvinceData 
GROUP BY 
    patientsProvinceData.province_name 
ORDER BY 
    patientsCount DESC;
```

## Problem Statement 4
For every admission, display the patient's full name, their admission diagnosis, and the full name of the doctor who diagnosed their problem.

## Solution Approach
To achieve this, we:
1. **Join Tables**: Use `JOIN` operations to combine data from the `patients`, `admissions`, and `doctors` tables.
2. **Select Columns**: Extract the patient's full name, the diagnosis for the admission, and the full name of the attending doctor.
3. **Concatenate Names**: Use the `CONCAT` function to combine `first_name` and `last_name` for both the patient and doctor.

## SQL Query
```sql
SELECT 
    CONCAT(wholePatientData.first_name, ' ', wholePatientData.last_name) AS fullname,
    wholePatientData.diagnosis AS admissionsDiagnosis, 
    CONCAT(wholePatientData.doctor_first_name, ' ', wholePatientData.doctor_last_name) AS doctorName 
FROM 
    (SELECT 
         patients.first_name, patients.last_name, 
         admissions.diagnosis, admissions.attending_doctor_id, 
         doctors.first_name AS doctor_first_name, doctors.last_name AS doctor_last_name
     FROM patients 
     JOIN admissions ON patients.patient_id = admissions.patient_id 
     JOIN doctors ON admissions.attending_doctor_id = doctors.doctor_id
    ) AS wholePatientData;
