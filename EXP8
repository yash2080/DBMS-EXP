# Alter Department Table & Create Salgrade Table

## Alter Department Table (Add Location Column)

```sql
ALTER TABLE Department
ADD COLUMN location VARCHAR(20);

UPDATE Department SET location = 'MUMBAI' WHERE DeptNo = 10;
UPDATE Department SET location = 'CHENNAI' WHERE DeptNo = 20;
UPDATE Department SET location = 'HYDERABAD' WHERE DeptNo = 30;
UPDATE Department SET location = 'DELHI' WHERE DeptNo = 40;

CREATE TABLE Salgrade (
    grade CHAR(1) PRIMARY KEY,
    losal INT,
    hisal INT
);

INSERT INTO Salgrade VALUES ('A',700,1200);
INSERT INTO Salgrade VALUES ('B',1201,1400);
INSERT INTO Salgrade VALUES ('C',1401,2000);
INSERT INTO Salgrade VALUES ('D',2001,3000);
INSERT INTO Salgrade VALUES ('E',3001,9999);


# Employee Table Queries – Experiment 8 (Joins & Advanced Queries)

-- Question 1: Display all employees with their department name
SELECT e.ename, d.dname
FROM Employee e
JOIN Department d ON e.DeptNo = d.DeptNo;

-- Question 2: Display employees whose manager name is JONES (also show manager name)
SELECT e.ename, m.ename AS manager
FROM Employee e
JOIN Employee m ON e.mgr = m.empno
WHERE m.ename = 'JONES';

-- Question 3: Display employee name, job, dept name, manager name and grade (department wise)
SELECT e.ename, e.job, d.dname,
       m.ename AS manager,
       s.grade
FROM Employee e
JOIN Department d ON e.DeptNo = d.DeptNo
LEFT JOIN Employee m ON e.mgr = m.empno
JOIN Salgrade s ON e.sal BETWEEN s.losal AND s.hisal
ORDER BY d.dname;

-- Question 4: List employee name, job, salary grade and department name except 'CLERK', sorted by highest salary
SELECT e.ename, e.job, s.grade, d.dname, e.sal
FROM Employee e
JOIN Department d ON e.DeptNo = d.DeptNo
JOIN Salgrade s ON e.sal BETWEEN s.losal AND s.hisal
WHERE e.job <> 'CLERK'
ORDER BY e.sal DESC;

-- Question 5: Display employee name, job and manager (include employees without manager)
SELECT e.ename, e.job,
       IFNULL(m.ename,'NO MANAGER') AS manager
FROM Employee e
LEFT JOIN Employee m ON e.mgr = m.empno;

-- Question 6: List employee name, job, annual salary, deptno, dept name and grade who earn 36000 per year or are not clerks
SELECT e.ename, e.job, (e.sal*12) AS annual_salary,
       d.deptno, d.dname, s.grade
FROM Employee e
JOIN Department d ON e.DeptNo = d.DeptNo
JOIN Salgrade s ON e.sal BETWEEN s.losal AND s.hisal
WHERE (e.sal*12 = 36000) OR e.job <> 'CLERK';

-- Question 7: List employee name, job, annual salary, deptno, dept name and grade who earn 30000 per year and are not clerks
SELECT e.ename, e.job, (e.sal*12) AS annual_salary,
       d.deptno, d.dname, s.grade
FROM Employee e
JOIN Department d ON e.DeptNo = d.DeptNo
JOIN Salgrade s ON e.sal BETWEEN s.losal AND s.hisal
WHERE (e.sal*12 = 30000) AND e.job <> 'CLERK';

-- Question 8: List all employees with their manager name and number (display 'NO MANAGER' if none)
SELECT e.empno, e.ename,
       IFNULL(m.ename,'NO MANAGER') AS manager_name,
       IFNULL(m.empno,0) AS manager_no
FROM Employee e
LEFT JOIN Employee m ON e.mgr = m.empno;

-- Question 9: Display department name, department number and total salary
SELECT d.deptno, d.dname, SUM(e.sal) AS total_salary
FROM Employee e
JOIN Department d ON e.DeptNo = d.DeptNo
GROUP BY d.deptno, d.dname;

-- Question 10: Display employee number, name and department location
SELECT e.empno, e.ename, d.location
FROM Employee e
JOIN Department d ON e.DeptNo = d.DeptNo;

-- Question 11: Display employee name and department name for each employee
SELECT e.ename, d.dname
FROM Employee e
JOIN Department d ON e.DeptNo = d.DeptNo;
