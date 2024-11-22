### Tutorial Questions with SQL Answers and Simple Explanations

---

#### **Question 1:**  
Display department names alongside the cities and countries where these departments are located, for all departments in Cambridge.

**SQL Answer:**
```sql
SELECT d.department_name, l.city, l.country
FROM locations l 
JOIN departments d ON l.location_id = d.location_id 
WHERE l.city = 'Cambridge';
```

**Explanation:**  
- Combines `locations` and `departments` tables using a `JOIN` based on `location_id`.  
- Filters to only include rows where the city is Cambridge (`WHERE l.city = 'Cambridge'`).
- The result shows department names, cities, and countries for Cambridge.

---

#### **Question 2:**  
List department names, full names, and salaries of employees earning over 45K in departments starting with "M".

**SQL Answer:**
```sql
SELECT e.first_name, e.last_name, e.salary, d.department_name
FROM employees e 
JOIN departments d ON e.department_id = d.department_id
WHERE e.salary >= 45000 
AND UPPER(d.department_name) LIKE UPPER('M%');
```

**Explanation:**  
- Combines `employees` and `departments` tables based on `department_id`.  
- Filters employees with salaries over 45K and departments starting with "M".  
- `UPPER` ensures the search is case-insensitive.

---

#### **Question 3:**  
Display countries, cities, department names, staff full names, and salaries for employees hired after 2 March 2015 or earning less than £46,000.

**SQL Answer:**
```sql
SELECT l.country, l.city, d.department_name, e.first_name, e.last_name, e.salary
FROM employees e
JOIN departments d ON e.department_id = d.department_id
JOIN locations l ON d.location_id = l.location_id
WHERE e.hire_date >= '2015-03-02' OR e.salary < 46000
ORDER BY l.country, l.city, d.department_name;
```

**Explanation:**  
- Combines `employees`, `departments`, and `locations` tables using `JOIN`.  
- Filters staff hired after 2 March 2015 or earning less than £46K.  
- Orders results by country, city, and department name.

---

#### **Question 4:**  
List departments, full names, hire dates, and salaries of employees whose surnames start with "P" or "S".

**SQL Answer:**
```sql
SELECT e.first_name, e.last_name, e.hire_date, e.salary, d.department_name
FROM departments d
JOIN employees e ON d.department_id = e.department_id
WHERE e.last_name LIKE 'P%' OR e.last_name LIKE 'S%';
```

**Explanation:**  
- Combines `employees` and `departments` tables.  
- Filters employees whose last names start with "P" or "S".  
- Shows their department, full name, hire date, and salary.

---

#### **Question 5:**  
List IDs, names of managers, and their employees with column headers distinguishing managers and employees.

**SQL Answer:**
```sql
SELECT m.employee_id AS "Mgr ID", m.first_name AS "Mgr F Name", m.last_name AS "Mgr L Name",
       e.employee_id AS "Emp ID", e.first_name AS "Emp F Name", e.last_name AS "Emp L Name"
FROM employees m
JOIN employees e ON m.employee_id = e.manager_id;
```

**Explanation:**  
- Joins the `employees` table to itself (`self-join`) using `manager_id`.  
- Displays managers and their corresponding employees with clear column headers.

---

#### **Question 6:**  
Create a management report showing relationships like “Jenny Bloggs (ID: 1234) manages John Smith (ID: 5678)”.

**SQL Answer:**
```sql
SELECT CONCAT(m.first_name, ' ', m.last_name, ' (ID: ', m.employee_id, ') manages ', 
              e.first_name, ' ', e.last_name, ' (ID: ', e.employee_id, ')') AS "Management Report"
FROM employees m
JOIN employees e ON m.employee_id = e.manager_id;
```

**Explanation:**  
- Uses `CONCAT` to combine text with employee and manager details into a single column.  
- Self-join links managers to employees.

---

#### **Question 7:**  
Display surnames, salaries, and job roles of employees in the IT department.

**SQL Answer:**
```sql
SELECT e.last_name, e.salary, j.job_title, d.department_name
FROM departments d
JOIN employees e ON d.department_id = e.department_id
JOIN jobs j ON e.job_id = j.job_id
WHERE d.department_name = 'IT';
```

**Explanation:**  
- Combines `departments`, `employees`, and `jobs` tables to fetch data.  
- Filters to include only employees in the IT department.

---

#### **Question 8:**  
List employee names, salaries, job roles, department names, and their locations.

**SQL Answer:**
```sql
SELECT e.last_name, e.first_name, e.salary, j.job_title, d.department_name, l.city, l.country
FROM locations l
JOIN departments d ON l.location_id = d.location_id
JOIN employees e ON d.department_id = e.department_id
JOIN jobs j ON e.job_id = j.job_id;
```

**Explanation:**  
- Combines `locations`, `departments`, `employees`, and `jobs` tables.  
- Displays full employee details, including department and location.

---

#### **Question 9:**  
List employee surnames, salaries, hire dates, and job roles for employees in London hired before 25 April 2019 and not earning between £40K and £50K.

**SQL Answer:**
```sql
SELECT e.last_name, e.salary, e.hire_date, j.job_title, d.department_name, l.city
FROM locations l
JOIN departments d ON l.location_id = d.location_id
JOIN employees e ON d.department_id = e.department_id
JOIN jobs j ON e.job_id = j.job_id
WHERE l.city = 'London' AND e.hire_date < '2019-04-25' 
AND (e.salary < 40000 OR e.salary > 50000);
```

**Explanation:**  
- Filters employees based on location, hire date, and salary range.  
- Combines necessary tables for comprehensive details.

---

#### **Question 10:**  
Show surnames, salaries, and job roles of employees and their managers.

**SQL Answer:**
```sql
SELECT e.last_name, e.salary, je.job_title, de.department_name,
       m.last_name, m.salary, jm.job_title, dm.department_name
FROM employees e
JOIN jobs je ON e.job_id = je.job_id
JOIN departments de ON e.department_id = de.department_id
JOIN employees m ON e.manager_id = m.employee_id
JOIN jobs jm ON m.job_id = jm.job_id
JOIN departments dm ON m.department_id = dm.department_id;
```

**Explanation:**  
- Displays both employee and manager details by joining relevant tables.  
- Highlights relationships and roles between employees and their managers.

---
