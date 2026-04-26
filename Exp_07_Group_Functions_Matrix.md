# Experiment 7 – Group Functions and Matrix Queries

**Course:** UCS4001 – Database Management System

---

## Objective
Use GROUP BY, HAVING, and advanced aggregate queries including matrix-style reports.

---

## Queries

**1. Compute the number of days remaining in this year.**
```sql
SELECT TO_DATE('31-DEC-' || TO_CHAR(SYSDATE, 'YYYY')) - SYSDATE AS DAYS_LEFT FROM DUAL;
```

**2. Find the highest and lowest salaries and the difference between them.**
```sql
SELECT MAX(SAL), MIN(SAL), MAX(SAL) - MIN(SAL) AS DIFFERENCE FROM EMPLOYEE;
```

**3. List employees whose commission is greater than 25% of their salary.**
```sql
SELECT * FROM EMPLOYEE WHERE COMM > SAL * 0.25;
```

**4. Display salary in dollar format.**
```sql
SELECT ENAME, TO_CHAR(SAL, '$99,999') AS SALARY FROM EMPLOYEE;
```

**5. Create a matrix query: display job, salary by department number, and total salary for that job.**
```sql
SELECT JOB,
  SUM(CASE WHEN DEPTNO = 10 THEN SAL ELSE 0 END) AS DEPT10,
  SUM(CASE WHEN DEPTNO = 20 THEN SAL ELSE 0 END) AS DEPT20,
  SUM(CASE WHEN DEPTNO = 30 THEN SAL ELSE 0 END) AS DEPT30,
  SUM(SAL) AS TOTAL
FROM EMPLOYEE
GROUP BY JOB;
```

**6. Display total employees and how many were hired in 1980, 1981, 1982, and 1983.**
```sql
SELECT COUNT(*) AS TOTAL,
  SUM(CASE WHEN TO_CHAR(HIREDATE, 'YYYY') = '1980' THEN 1 ELSE 0 END) AS "1980",
  SUM(CASE WHEN TO_CHAR(HIREDATE, 'YYYY') = '1981' THEN 1 ELSE 0 END) AS "1981",
  SUM(CASE WHEN TO_CHAR(HIREDATE, 'YYYY') = '1982' THEN 1 ELSE 0 END) AS "1982",
  SUM(CASE WHEN TO_CHAR(HIREDATE, 'YYYY') = '1983' THEN 1 ELSE 0 END) AS "1983"
FROM EMPLOYEE;
```

**7. Get the last Sunday of any month.**
```sql
SELECT NEXT_DAY(LAST_DAY(SYSDATE) - 7, 'SUNDAY') AS LAST_SUNDAY FROM DUAL;
```

**8. Display department numbers and total number of employees in each department.**
```sql
SELECT DEPTNO, COUNT(*) AS TOTAL_EMP FROM EMPLOYEE GROUP BY DEPTNO;
```

**9. Display various jobs and total number of employees in each job group.**
```sql
SELECT JOB, COUNT(*) AS TOTAL_EMP FROM EMPLOYEE GROUP BY JOB;
```

**10. Display department numbers and total salary for each department.**
```sql
SELECT DEPTNO, SUM(SAL) AS TOTAL_SAL FROM EMPLOYEE GROUP BY DEPTNO;
```
