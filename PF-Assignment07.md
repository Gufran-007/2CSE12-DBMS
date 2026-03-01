# PRACTICAL FILE ASSIGNMENT - 07

## DATE : 25/02/2026

### 1. Compute the no. of days remaining in this year.

```sql
MariaDB [gufran]> SELECT DATEDIFF(
    -> MAKEDATE(YEAR(CURDATE()), '365'),
    -> CURDATE())
    -> AS REMAINING_DAYS;
```

<pre>
Output:
+----------------+
| REMAINING_DAYS |
+----------------+
|            305 |
+----------------+
1 row in set (0.009 sec)
</pre>

### 2. Find the highest and lowest salaries and the difference between of them.

```sql
MariaDB [gufran]> SELECT
    -> MAX(SAL) AS HIGHEST_SALARY,
    -> MIN(SAL) AS LOWEST_SALARY,
    -> (MAX(SAL)-MIN(SAL)) AS DIFFERENCE
    -> FROM EMPLOYEE_MASTER;
```

<pre>
Output:
+----------------+---------------+------------+
| HIGHEST_SALARY | LOWEST_SALARY | DIFFERENCE |
+----------------+---------------+------------+
|           6050 |           968 |       5082 |
+----------------+---------------+------------+
1 row in set (0.048 sec)
</pre>

### 3. List employee whose commission is greater than 25 % of their salaries.

```sql
MariaDB [gufran]> SELECT *
    -> FROM EMPLOYEE_MASTER
    -> WHERE COMM > (0.25*SAL);
```

<pre>
Output:
+-------+--------+----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+----------+------+------------+------+------+--------+
|  7654 | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
+-------+--------+----------+------+------------+------+------+--------+
1 row in set (0.001 sec)
</pre>

### 4. Make a query that displays salary in dollar format.

```sql
 MariaDB [gufran]> SELECT
    -> CONCAT('$', FORMAT(SAL,2)) AS SALARY_IN_DOLLARS
    -> FROM EMPLOYEE_MASTER;
```

<pre>
Output:
+-------------------+
| SALARY_IN_DOLLARS |
+-------------------+
| $968.00           |
| $1,600.00         |
| $1,250.00         |
| $3,600.00         |
| $1,250.00         |
| $3,449.00         |
| $2,965.00         |
| $3,630.00         |
| $6,050.00         |
| $1,500.00         |
| $1,331.00         |
| $1,150.00         |
| $3,630.00         |
| $1,573.00         |
+-------------------+
14 rows in set (0.001 sec)
</pre>

### 5. Create a matrix query to display the job, the salary for that job based on department number, and the total salary for that job for all departments, giving each column an appropriate heading.

```sql
MariaDB [gufran]> SELECT JOB,
    -> SUM(CASE WHEN DEPTNO=10 THEN SAL ELSE 0 END) AS SALARY_FOR_DEPT10,
    -> SUM(CASE WHEN DEPTNO=20 THEN SAL ELSE 0 END) AS SALARY_FOR_DEPT20,
    -> SUM(CASE WHEN DEPTNO=30 THEN SAL ELSE 0 END) AS SALARY_FOR_DEPT30,
    -> SUM(CASE WHEN DEPTNO=40 THEN SAL ELSE 0 END) AS SALARY_FOR_DEPT40,
    -> SUM(SAL) AS TOTAL_SALARY
    -> FROM EMPLOYEE_MASTER
    -> GROUP BY JOB;
```

<pre>
Output:
+-----------+-------------------+-------------------+-------------------+-------------------+--------------+
| JOB       | SALARY_FOR_DEPT10 | SALARY_FOR_DEPT20 | SALARY_FOR_DEPT30 | SALARY_FOR_DEPT40 | TOTAL_SALARY |
+-----------+-------------------+-------------------+-------------------+-------------------+--------------+
| ANALYST   |                 0 |              3630 |                 0 |              3630 |         7260 |
| CLERK     |              1573 |              2299 |              1150 |                 0 |         5022 |
| MANAGER   |                 0 |              6565 |              3449 |                 0 |        10014 |
| PRESIDENT |                 0 |              6050 |                 0 |                 0 |         6050 |
| SALESMAN  |                 0 |                 0 |              5600 |                 0 |         5600 |
+-----------+-------------------+-------------------+-------------------+-------------------+--------------+
5 rows in set (0.001 sec)
</pre>

### 6. Query that will display the total no of employees, and of that total the number who were hired in 1980,1981,1982 and 1983. Give appropriate column heading.

```sql
MariaDB [gufran]> SELECT
    -> COUNT(*) AS TOTAL_EMPLOYEES,
    -> SUM(CASE WHEN YEAR(HIREDATE)=1980 THEN 1 ELSE 0 END) AS HIRED_IN_1980,
    -> SUM(CASE WHEN YEAR(HIREDATE)=1981 THEN 1 ELSE 0 END) AS HIRED_IN_1981,
    -> SUM(CASE WHEN YEAR(HIREDATE)=1982 THEN 1 ELSE 0 END) AS HIRED_IN_1982,
    -> SUM(CASE WHEN YEAR(HIREDATE)=1983 THEN 1 ELSE 0 END) AS HIRED_IN_1983
    -> FROM EMPLOYEE_MASTER;
```

<pre>
Output:
+-----------------+---------------+---------------+---------------+---------------+
| TOTAL_EMPLOYEES | HIRED_IN_1980 | HIRED_IN_1981 | HIRED_IN_1982 | HIRED_IN_1983 |
+-----------------+---------------+---------------+---------------+---------------+
|              14 |             1 |            10 |             2 |             1 |
+-----------------+---------------+---------------+---------------+---------------+
1 row in set (0.001 sec)
</pre>

### 7. Query to get the last Sunday of Any Month.

```sql
MariaDB [gufran]> SELECT DATE_SUB(
    -> LAST_DAY(CURDATE()),
    -> INTERVAL (DAYOFWEEK(LAST_DAY(CURDATE()))-1) DAY
    -> ) AS LAST_SUNDAY;
```

<pre>
Output:
+-------------+
| LAST_SUNDAY |
+-------------+
| 2026-03-29  |
+-------------+
1 row in set (0.001 sec)
</pre>

### 8. Display department numbers and total number of employees working in each department.

```sql
MariaDB [gufran]> SELECT DEPTNO,
    -> COUNT(*) AS TOTAL_EMPLOYEES
    -> FROM EMPLOYEE_MASTER
    -> GROUP BY DEPTNO;
```

<pre>
Output:
+--------+-----------------+
| DEPTNO | TOTAL_EMPLOYEES |
+--------+-----------------+
|     10 |               1 |
|     20 |               6 |
|     30 |               6 |
|     40 |               1 |
+--------+-----------------+
4 rows in set (0.001 sec)
</pre>

### 9. Display the various jobs and total number of employees within each job group.

```sql
MariaDB [gufran]> SELECT JOB,
    -> COUNT(*) AS TOTAL_EMPLOYEES
    -> FROM EMPLOYEE_MASTER
    -> GROUP BY JOB;
```

<pre>
Output:
+-----------+-----------------+
| JOB       | TOTAL_EMPLOYEES |
+-----------+-----------------+
| ANALYST   |               2 |
| CLERK     |               4 |
| MANAGER   |               3 |
| PRESIDENT |               1 |
| SALESMAN  |               4 |
+-----------+-----------------+
5 rows in set (0.001 sec)
</pre>

### 10. Display the depart numbers and total salary for each department.

```sql
MariaDB [gufran]> SELECT DEPTNO,
    -> SUM(SAL) AS TOTAL_SALARY
    -> FROM EMPLOYEE_MASTER
    -> GROUP BY DEPTNO;
```

<pre>
Output:
+--------+--------------+
| DEPTNO | TOTAL_SALARY |
+--------+--------------+
|     10 |         1573 |
|     20 |        18544 |
|     30 |        10199 |
|     40 |         3630 |
+--------+--------------+
4 rows in set (0.001 sec)
</pre>
