# Experiment 9 – Subqueries (Part 1)

**Course:** UCS4001 – Database Management System

---

## Objective
Use subqueries to retrieve complex information from the Employee and Department tables.

---

## Queries

**1. Display the name of the employee who earns the highest salary.**
```sql
SELECT ENAME FROM EMPLOYEE WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```

**2. Display the employee number and name of the clerk earning the highest salary among clerks.**
```sql
SELECT EMPNO, ENAME FROM EMPLOYEE
WHERE JOB = 'CLERK' AND SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
```

**3. Display the names of salesmen who earn more than the highest salary of any clerk.**
```sql
SELECT ENAME FROM EMPLOYEE
WHERE JOB = 'SALESMAN' AND SAL > (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
```

**4. Display names of clerks who earn more than JAMES or less than SCOTT.**
```sql
SELECT ENAME FROM EMPLOYEE
WHERE JOB = 'CLERK'
  AND (SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
    OR SAL < (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT'));
```

**5. Display names of employees who earn more than JAMES or more than SCOTT.**
```sql
SELECT ENAME FROM EMPLOYEE
WHERE SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
   OR SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
```

**6. Display names of employees who earn the highest salary in their respective departments.**
```sql
SELECT ENAME FROM EMPLOYEE E
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE DEPTNO = E.DEPTNO);
```

**7. Display names of employees who earn the highest salary in their respective job groups.**
```sql
SELECT ENAME FROM EMPLOYEE E
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = E.JOB);
```

**8. Display employee names working in the ACCOUNTING department.**
```sql
SELECT ENAME FROM EMPLOYEE
WHERE DEPTNO = (SELECT DEPTNO FROM DEPARTMENT WHERE DNAME = 'ACCOUNTING');
```

**9. Display employee names working in CHICAGO.**
```sql
SELECT ENAME FROM EMPLOYEE
WHERE DEPTNO = (SELECT DEPTNO FROM DEPARTMENT WHERE LOC = 'CHICAGO');
```

**10. Display job groups having total salary greater than the maximum salary for managers.**
```sql
SELECT JOB, SUM(SAL) FROM EMPLOYEE
GROUP BY JOB
HAVING SUM(SAL) > (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'MANAGER');
```
