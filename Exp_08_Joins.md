# Experiment 8 – Joins

**Course:** UCS4001 – Database Management System

---

## Objective
Perform JOIN operations between EMPLOYEE, DEPARTMENT, and SALGRADE tables.

---

## Queries

**1. Display all employees with their department name.**
```sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```

**2. Display employees whose manager's name is JONES, and also display their manager name.**
```sql
SELECT E.ENAME AS EMPLOYEE, M.ENAME AS MANAGER
FROM EMPLOYEE E JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
```

**3. Display employee name, job, dept name, manager name, grade; sort department-wise.**
```sql
SELECT E.ENAME, E.JOB, D.DNAME, M.ENAME AS MANAGER, S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
ORDER BY D.DNAME;
```

**4. List employee name, job, salary grade and department name for everyone except clerks, sorted by highest salary.**
```sql
SELECT E.ENAME, E.JOB, S.GRADE, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.JOB != 'CLERK'
ORDER BY E.SAL DESC;
```

**5. Display employee name, job, and manager. Also display employees without a manager.**
```sql
SELECT E.ENAME, E.JOB, M.ENAME AS MANAGER
FROM EMPLOYEE E LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
```

**6. List ename, job, annual salary, deptno, dept name and grade who earn 36000/year or are not clerks.**
```sql
SELECT E.ENAME, E.JOB, E.SAL * 12 AS ANNUAL_SAL, E.DEPTNO, D.DNAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.SAL * 12 = 36000 OR E.JOB != 'CLERK';
```

**7. List ename, job, annual salary, deptno, dname and grade who earn 30000/year and are not clerks.**
```sql
SELECT E.ENAME, E.JOB, E.SAL * 12 AS ANNUAL_SAL, E.DEPTNO, D.DNAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.SAL * 12 = 30000 AND E.JOB != 'CLERK';
```

**8. List all employees by name and number along with their manager's name and number; display 'NO MANAGER' if no manager exists.**
```sql
SELECT E.EMPNO, E.ENAME,
  NVL(TO_CHAR(M.EMPNO), 'NO MANAGER') AS MGR_NO,
  NVL(M.ENAME, 'NO MANAGER') AS MANAGER
FROM EMPLOYEE E LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
```

**9. Select department name, department number and sum of salary.**
```sql
SELECT D.DNAME, D.DEPTNO, SUM(E.SAL) AS TOTAL_SAL
FROM DEPARTMENT D JOIN EMPLOYEE E ON D.DEPTNO = E.DEPTNO
GROUP BY D.DNAME, D.DEPTNO;
```

**10. Display employee number, name and location of the department in which they work.**
```sql
SELECT E.EMPNO, E.ENAME, D.LOC
FROM EMPLOYEE E JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```

**11. Display employee name and department name for each employee.**
```sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```
