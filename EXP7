# Employee Table Queries – Experiment 7 (Group By & Reports)

-- Question 1: Compute number of days remaining in this year
SELECT DATEDIFF(CONCAT(YEAR(CURDATE()), '-12-31'), CURDATE()) AS days_remaining;

-- Question 2: Find highest and lowest salaries and the difference between them
SELECT MAX(sal) AS highest_salary,
       MIN(sal) AS lowest_salary,
       (MAX(sal) - MIN(sal)) AS difference
FROM Employee;

-- Question 3: List employees whose commission is greater than 25% of their salary
SELECT ename, sal, comm
FROM Employee
WHERE comm > (sal * 0.25);

-- Question 4: Display salary in dollar format
SELECT ename, CONCAT('$', FORMAT(sal,2)) AS salary_dollar
FROM Employee;

-- Question 5: Display job-wise salary matrix by department and total salary
SELECT job,
       SUM(CASE WHEN DeptNo = 10 THEN sal ELSE 0 END) AS dept10,
       SUM(CASE WHEN DeptNo = 20 THEN sal ELSE 0 END) AS dept20,
       SUM(CASE WHEN DeptNo = 30 THEN sal ELSE 0 END) AS dept30,
       SUM(CASE WHEN DeptNo = 40 THEN sal ELSE 0 END) AS dept40,
       SUM(sal) AS total_salary
FROM Employee
GROUP BY job;

-- Question 6: Display total employees and count hired in each year (1980–1983)
SELECT COUNT(*) AS total_employees,
       SUM(CASE WHEN YEAR(hiredate)=1980 THEN 1 ELSE 0 END) AS y1980,
       SUM(CASE WHEN YEAR(hiredate)=1981 THEN 1 ELSE 0 END) AS y1981,
       SUM(CASE WHEN YEAR(hiredate)=1982 THEN 1 ELSE 0 END) AS y1982,
       SUM(CASE WHEN YEAR(hiredate)=1983 THEN 1 ELSE 0 END) AS y1983
FROM Employee;

-- Question 7: Find last Sunday of current month
SELECT DATE_SUB(
         LAST_DAY(CURDATE()), 
         INTERVAL (DAYOFWEEK(LAST_DAY(CURDATE())) - 1) DAY
       ) AS last_sunday;

-- Question 8: Display department numbers and total employees in each department
SELECT DeptNo, COUNT(*) AS total_employees
FROM Employee
GROUP BY DeptNo;

-- Question 9: Display jobs and total number of employees in each job group
SELECT job, COUNT(*) AS total_employees
FROM Employee
GROUP BY job;

-- Question 10: Display department numbers and total salary for each department
SELECT DeptNo, SUM(sal) AS total_salary
FROM Employee
GROUP BY DeptNo;
