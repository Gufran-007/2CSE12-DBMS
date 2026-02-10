# PRACTICAL FILE ASSIGNMENT - 02

## DATE : 04/02/26

### 1. List all employees and jobs in Department 30 in descending order by salary.

```sql
SELECT ENAME, JOB, SAL
FROM Employee_master
WHERE DEPTNO = 30
ORDER BY SAL DESC;
```

<pre>
+--------+----------+------+
| ENAME  | JOB      | SAL  |
+--------+----------+------+
| BLAKE  | MANAGER  | 3135 |
| ALLEN  | SALESMAN | 1600 |
| TURNER | SALESMAN | 1500 |
| WARD   | SALESMAN | 1250 |
| MARTIN | SALESMAN | 1250 |
| JAMES  | CLERK    | 1045 |
+--------+----------+------+
6 rows in set (0.001 sec)
</pre>

### 2. List job and department number of employees.

```sql
SELECT JOB, DEPTNO
FROM Employee_master
WHERE ENAME LIKE 'A___N';
```

<pre>
+----------+--------+
| JOB      | DEPTNO |
+----------+--------+
| SALESMAN |     30 |
+----------+--------+
1 row in set (0.001 sec)
</pre>

### 3. Display names of employees whose name starts with S.

```sql
SELECT ENAME
FROM Employee_master
WHERE ENAME LIKE 'S%';
```

<pre>
+-------+
| ENAME |
+-------+
| SMITH |
| SCOTT |
+-------+
2 rows in set (0.001 sec)
</pre>

### 4. Display names of employees whose name ends with S.

```sql
SELECT ENAME
FROM Employee_master
WHERE ENAME LIKE '%S';
```

<pre>
+-------+
| ENAME |
+-------+
| JONES |
| ADAMS |
| JAMES |
+-------+
3 rows in set (0.001 sec)
</pre>

### 5. Display names of employees working in department 10 or 20 or 40 or working as CLERK, SALESMAN or ANALYST.

```sql
SELECT ENAME
FROM Employee_master
WHERE DEPTNO IN (10, 20, 40)
   OR JOB IN ('CLERK', 'SALESMAN', 'ANALYST');
```

<pre>
+--------+
| ENAME  |
+--------+
| SMITH  |
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| CLARK  |
| SCOTT  |
| KING   |
| TURNER |
| ADAMS  |
| JAMES  |
| FORD   |
| MILLER |
+--------+
13 rows in set (0.001 sec)
</pre>

### 6. Display employee number and names of employees who earn commission.

```sql
SELECT EMPNO, ENAME
FROM Employee_master
WHERE COMM IS NOT NULL
  AND COMM > 0;
```

<pre>
+-------+--------+
| EMPNO | ENAME  |
+-------+--------+
|  7499 | ALLEN  |
|  7521 | WARD   |
|  7654 | MARTIN |
+-------+--------+
3 rows in set (0.001 sec)
</pre>

### 7. Display employee number and total salary for each employee, (total salary = salary + commission).

```sql
SELECT EMPNO, SAL + IFNULL(COMM, 0) AS TOTAL_SALARY
FROM Employee_master;
```

<pre>
+-------+--------------+
| EMPNO | TOTAL_SALARY |
+-------+--------------+
|  7369 |          880 |
|  7499 |         1900 |
|  7521 |         1550 |
|  7566 |         3273 |
|  7654 |         2650 |
|  7698 |         3135 |
|  7782 |         2695 |
|  7788 |         3300 |
|  7839 |         5500 |
|  7844 |         1500 |
|  7876 |         1210 |
|  7900 |         1045 |
|  7902 |         3300 |
|  7934 |         1430 |
+-------+--------------+
14 rows in set (0.001 sec)
</pre>

### 8. Display employee number and annual salary for each employee.

```sql
SELECT EMPNO, SAL * 12 AS ANNUAL_SALARY
FROM Employee_master;
```

<pre>
+-------+---------------+
| EMPNO | ANNUAL_SALARY |
+-------+---------------+
|  7369 |         10560 |
|  7499 |         19200 |
|  7521 |         15000 |
|  7566 |         39276 |
|  7654 |         15000 |
|  7698 |         37620 |
|  7782 |         32340 |
|  7788 |         39600 |
|  7839 |         66000 |
|  7844 |         18000 |
|  7876 |         14520 |
|  7900 |         12540 |
|  7902 |         39600 |
|  7934 |         17160 |
+-------+---------------+
14 rows in set (0.001 sec)
</pre>

### 9. Display names of employees working as clerks.

```sql
SELECT ENAME
FROM Employee_master
WHERE JOB = 'CLERK'
  AND SAL > 3000;
```

<pre>
Empty set (0.001 sec)
</pre>

### 10. Display names of employees working as clerk, salesman or analyst and drawing salary more than 3000.

```sql
SELECT ENAME
FROM Employee_master
WHERE JOB IN ('CLERK', 'SALESMAN', 'ANALYST')
  AND SAL > 3000;
```

<pre>
+-------+
| ENAME |
+-------+
| SCOTT |
| FORD  |
+-------+
</pre>
