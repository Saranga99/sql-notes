### Tutorial Questions with SQL Answers and Simple Explanations

---

#### **Question 1 (a):**  
Display the average salary for employees with IDs 1022, 1023, 1024, and 1025.

**SQL Answer:**
```sql
SELECT AVG(salary) AS "Average Salary"
FROM employees
WHERE employee_id IN (1022, 1023, 1024, 1025);
```

**Explanation:**  
- **Purpose:** Calculate the average salary for specific employees.  
- **Key Concept:** The `AVG` function computes the mean value, while `IN` checks if the employee ID matches the given list.

---

#### **Question 1 (b):**  
Modify the query to treat missing salaries as zero.

**SQL Answer:**
```sql
SELECT AVG(IFNULL(salary, 0)) AS "Average Salary"
FROM employees
WHERE employee_id IN (1022, 1023, 1024, 1025);
```

**Explanation:**  
- **Key Change:** `IFNULL(salary, 0)` replaces `NULL` salaries with 0 for calculation.  
- **Result:** Ensures employees without a salary are included in the average as zero.

---

#### **Question 2:**  
Display the lowest, highest, and average salary for staff with job IDs 907, 908, or 909, hired in 2017.

**SQL Answer:**
```sql
SELECT MIN(salary) AS "Minimum", MAX(salary) AS "Maximum", AVG(salary) AS "Average"
FROM employees
WHERE job_id IN (907, 908, 909) AND hire_date LIKE '%2017%';
```

**Explanation:**  
- **Purpose:** Analyze salaries for specific job IDs.  
- **Key Concepts:**  
  - `MIN`, `MAX`, and `AVG` aggregate salary values.  
  - `LIKE '%2017%'` filters employees hired in 2017.

---

#### **Question 3:**  
List manager IDs and the lowest-paid employees they manage, excluding groups where the minimum salary is ≤ 47,000.

**SQL Answer:**
```sql
SELECT manager_id, MIN(salary)
FROM employees
WHERE manager_id IS NOT NULL
GROUP BY manager_id
HAVING MIN(salary) > 47000;
```

**Explanation:**  
- **Grouping:** `GROUP BY manager_id` groups employees by their manager.  
- **Filtering:** `HAVING MIN(salary) > 47000` excludes managers with employees earning ≤ 47,000.

---

#### **Question 4:**  
Display department IDs, lowest, highest, and average salaries for departments with maximum and average salaries > 50,000.

**SQL Answer:**
```sql
SELECT department_id, MIN(salary) AS "Minimum", MAX(salary) AS "Maximum", AVG(salary) AS "Average"
FROM employees
WHERE department_id IS NOT NULL
GROUP BY department_id
HAVING MAX(salary) > 50000 AND AVG(salary) > 50000;
```

**Explanation:**  
- **Purpose:** Analyze salary statistics for qualifying departments.  
- **Key Concepts:**  
  - `HAVING` ensures both conditions (`MAX` and `AVG` > 50,000) are met.  

---

#### **Question 5:**  
List department IDs and names alongside the average salary in each department, including departments without employees.

**SQL Answer:**
```sql
SELECT d.department_id, d.department_name, AVG(e.salary) AS "Average"
FROM departments d LEFT OUTER JOIN employees e ON d.department_id = e.department_id
GROUP BY d.department_id;
```

**Explanation:**  
- **Join Type:** `LEFT OUTER JOIN` ensures departments without employees are included.  
- **Key Concept:** `AVG` calculates salaries per department.

---

#### **Question 6:**  
List job IDs, job titles, and the count of employees for each job with at least two staff and exclude management roles.

**SQL Answer:**
```sql
SELECT e.job_id AS "Job Id", j.job_title AS "Job Title", COUNT(e.job_id) AS "Staff Count"
FROM jobs j JOIN employees e ON j.job_id = e.job_id
WHERE j.job_title NOT LIKE '%Manag%'
GROUP BY e.job_id
HAVING COUNT(e.job_id) >= 2
ORDER BY j.job_title;
```

**Explanation:**  
- **Filter:** Excludes management roles using `NOT LIKE '%Manag%'`.  
- **Grouping and Filtering:** Groups by job ID, and `HAVING` ensures at least two employees per job.

---

#### **Question 7:**  
Display department numbers, last names, and hire dates of employees in the same department as "Matos," excluding Matos.

**SQL Answer:**
```sql
SELECT department_id, last_name, hire_date
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM employees
    WHERE last_name = 'Matos'
) AND last_name <> 'Matos'
ORDER BY department_id;
```

**Explanation:**  
- **Subquery:** Finds the department ID of "Matos."  
- **Exclusion:** Filters out "Matos" using `last_name <> 'Matos'`.

---

#### **Question 8:**  
List last names and salaries of staff earning more than the highest salary in department 40.

**SQL Answer:**
```sql
SELECT last_name, salary
FROM employees
WHERE salary > (
    SELECT MAX(salary)
    FROM employees
    WHERE department_id = 40
);
```

**Explanation:**  
- **Subquery:** Finds the highest salary in department 40.  
- **Comparison:** Filters employees earning more than this value.

---

#### **Question 9:**  
Display last names, salaries, and department IDs for employees whose department location ID is 100.

**SQL Answer:**
```sql
SELECT last_name, salary, hire_date, department_id
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location_id = 100
);
```

**Explanation:**  
- **Subquery:** Retrieves department IDs with location ID 100.  
- **Filtering:** Includes employees in these departments.

---

#### **Question 10:**  
List department IDs and names for departments without employees in job code 904.

**SQL Answer:**
```sql
SELECT department_id, department_name
FROM departments
WHERE department_id NOT IN (
    SELECT department_id
    FROM employees
    WHERE job_id = 904 AND department_id IS NOT NULL
);
```

**Explanation:**  
- **Subquery:** Identifies departments with employees in job code 904.  
- **Exclusion:** `NOT IN` ensures these departments are excluded.

---
