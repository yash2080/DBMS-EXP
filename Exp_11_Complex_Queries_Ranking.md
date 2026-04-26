# Experiment 11 – Complex Queries and Ranking

**Course:** UCS4001 – Database Management System

---

## Objective
Use advanced queries, TOP-N analysis, and manager-based comparisons.

---

## Queries

**1. Delete employees who joined before 31-Dec-82 and whose dept location is 'NEW YORK' or 'CHICAGO'.**
```sql
DELETE FROM EMPLOYEE
WHERE HIREDATE < '31-DEC-82'
  AND DEPTNO IN (SELECT DEPTNO FROM DEPARTMENT WHERE LOC IN ('NEW YORK', 'CHICAGO'));
```

**2. Display employee name, job, dept name, location for all managers.**
```sql
SELECT E.ENAME, E.JOB, D.DNAME, D.LOC
FROM EMPLOYEE E JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.JOB = 'MANAGER';
```

**3. Display name and salary of FORD if his salary equals the highest salary of his grade.**
```sql
SELECT E.ENAME, E.SAL
FROM EMPLOYEE E JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.ENAME = 'FORD' AND E.SAL = S.HISAL;
```

**4. Find the top 5 earners of the company.**
```sql
SELECT ENAME, SAL FROM EMPLOYEE ORDER BY SAL DESC FETCH FIRST 5 ROWS ONLY;
-- Oracle (older versions):
-- SELECT ENAME, SAL FROM (SELECT ENAME, SAL FROM EMPLOYEE ORDER BY SAL DESC) WHERE ROWNUM <= 5;
```

**5. Display the name of employees getting the highest salary.**
```sql
SELECT ENAME FROM EMPLOYEE WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```

**6. Display employees whose salary equals the average of the maximum and minimum salary.**
```sql
SELECT * FROM EMPLOYEE
WHERE SAL = (SELECT (MAX(SAL) + MIN(SAL)) / 2 FROM EMPLOYEE);
```

**7. Display department names where at least 3 employees are working.**
```sql
SELECT D.DNAME FROM DEPARTMENT D
JOIN EMPLOYEE E ON D.DEPTNO = E.DEPTNO
GROUP BY D.DNAME
HAVING COUNT(*) >= 3;
```

**8. Display names of managers whose salary is more than the average salary of the company.**
```sql
SELECT ENAME FROM EMPLOYEE
WHERE JOB = 'MANAGER' AND SAL > (SELECT AVG(SAL) FROM EMPLOYEE);
```

**9. Display managers whose salary is more than the average salary of their employees.**
```sql
SELECT M.ENAME FROM EMPLOYEE M
WHERE M.EMPNO IN (SELECT MGR FROM EMPLOYEE WHERE MGR IS NOT NULL)
  AND M.SAL > (SELECT AVG(SAL) FROM EMPLOYEE WHERE MGR = M.EMPNO);
```

**10. Display employee name, sal, comm and net pay for employees whose net pay >= any other employee's salary.**
```sql
SELECT ENAME, SAL, COMM, SAL + NVL(COMM, 0) AS NET_PAY
FROM EMPLOYEE
WHERE SAL + NVL(COMM, 0) >= ANY (SELECT SAL FROM EMPLOYEE);
```
