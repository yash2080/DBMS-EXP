# Experiment 10 – Subqueries (Part 2)

**Course:** UCS4001 – Database Management System

---

## Objective
Use advanced subqueries with ANY, ALL, and correlated subqueries for complex data retrieval.

---

## Queries

**1. Display names of employees from department 10 with salary greater than ANY employee in other departments.**
```sql
SELECT ENAME FROM EMPLOYEE
WHERE DEPTNO = 10 AND SAL > ANY (SELECT SAL FROM EMPLOYEE WHERE DEPTNO != 10);
```

**2. Display names of employees from department 10 with salary greater than ALL employees in other departments.**
```sql
SELECT ENAME FROM EMPLOYEE
WHERE DEPTNO = 10 AND SAL > ALL (SELECT SAL FROM EMPLOYEE WHERE DEPTNO != 10);
```

**3. Display details of employees in the SALES department with grade 3.**
```sql
SELECT E.* FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.DEPTNO = (SELECT DEPTNO FROM DEPARTMENT WHERE DNAME = 'SALES')
  AND S.GRADE = 3;
```

**4. Display those who are not managers and who are managed by someone.**
```sql
SELECT ENAME FROM EMPLOYEE
WHERE EMPNO NOT IN (SELECT DISTINCT MGR FROM EMPLOYEE WHERE MGR IS NOT NULL)
  AND MGR IN (SELECT EMPNO FROM EMPLOYEE);
```

**5. Display employees whose manager's name is JONES.**
```sql
SELECT E.ENAME FROM EMPLOYEE E
WHERE E.MGR = (SELECT EMPNO FROM EMPLOYEE WHERE ENAME = 'JONES');
```

**6. Display employee names working in the SALES department.**
```sql
SELECT ENAME FROM EMPLOYEE
WHERE DEPTNO = (SELECT DEPTNO FROM DEPARTMENT WHERE DNAME = 'SALES');
```

**7. Display employee name, dept name, salary and comm where salary is between 2000–5000 and location is CHICAGO.**
```sql
SELECT E.ENAME, D.DNAME, E.SAL, E.COMM
FROM EMPLOYEE E JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.SAL BETWEEN 2000 AND 5000 AND D.LOC = 'CHICAGO';
```

**8. Display employees whose salary is greater than their manager's salary.**
```sql
SELECT E.ENAME FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

**9. Display employees working in the same department as their manager.**
```sql
SELECT E.ENAME FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.DEPTNO = M.DEPTNO;
```

**10. Display grade and employee name for dept 10 or 30 where grade is not 4, joined before 31-Dec-82.**
```sql
SELECT S.GRADE, E.ENAME
FROM EMPLOYEE E JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.DEPTNO IN (10, 30) AND S.GRADE != 4 AND E.HIREDATE < '31-DEC-82';
```
