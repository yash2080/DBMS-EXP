# Experiment 12 – Advanced Subqueries and Correlated Queries

**Course:** UCS4001 – Database Management System

---

## Objective
Use correlated subqueries and advanced conditional queries for deep data analysis.

---

## Queries

**1. Display employees whose salary is less than their manager's but more than salary of any other manager.**
```sql
SELECT E.ENAME FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL < M.SAL
  AND E.SAL > ANY (SELECT SAL FROM EMPLOYEE WHERE JOB = 'MANAGER');
```

**2. Find the number of employees whose salary is greater than their manager's salary.**
```sql
SELECT COUNT(*) FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

**3. Display managers who are not working under the President but under another manager.**
```sql
SELECT E.ENAME FROM EMPLOYEE E
WHERE E.JOB = 'MANAGER'
  AND E.MGR NOT IN (SELECT EMPNO FROM EMPLOYEE WHERE JOB = 'PRESIDENT');
```

**4. Delete departments where no employee is working.**
```sql
DELETE FROM DEPARTMENT
WHERE DEPTNO NOT IN (SELECT DISTINCT DEPTNO FROM EMPLOYEE WHERE DEPTNO IS NOT NULL);
```

**5. Delete records from emp table whose deptno is not available in dept table.**
```sql
DELETE FROM EMPLOYEE
WHERE DEPTNO NOT IN (SELECT DEPTNO FROM DEPARTMENT);
```

**6. Display employees whose salary is outside the grade available in the salgrade table.**
```sql
SELECT * FROM EMPLOYEE
WHERE SAL NOT BETWEEN (SELECT MIN(LOSAL) FROM SALGRADE)
                  AND (SELECT MAX(HISAL) FROM SALGRADE);
```

**7. Display employee name, sal, comm and net pay where net pay is greater than any other employee in the company.**
```sql
SELECT ENAME, SAL, COMM, SAL + NVL(COMM, 0) AS NET_PAY
FROM EMPLOYEE
WHERE SAL + NVL(COMM, 0) > ANY (SELECT SAL + NVL(COMM, 0) FROM EMPLOYEE);
```

**8. Display employees working in SALES or RESEARCH.**
```sql
SELECT E.ENAME FROM EMPLOYEE E
WHERE E.DEPTNO IN (SELECT DEPTNO FROM DEPARTMENT WHERE DNAME IN ('SALES', 'RESEARCH'));
```

**9. Display the grade of JONES.**
```sql
SELECT S.GRADE FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.ENAME = 'JONES';
```

**10. Display department name whose number of characters equals the number of employees in any other department.**
```sql
SELECT DNAME FROM DEPARTMENT
WHERE LENGTH(DNAME) IN (SELECT COUNT(*) FROM EMPLOYEE GROUP BY DEPTNO);
```
