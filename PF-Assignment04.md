# PRACTICAL FILE ASSIGNMENT - 02

## DATE : 09/02/26

### 1. Employees who joined before 30-Jun-1980 OR after 31-Dec-1981.

```sql
SELECT *
FROM EMPLOYEE_MASTER
WHERE HIREDATE < '1980-06-30'
   OR HIREDATE > '1981-12-31';
```

<pre>
+-------+--------+---------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+---------+------+------------+------+------+--------+
|  7788 | SCOTT  | ANALYST | 7566 | 1982-12-09 | 3300 | NULL |     40 |
|  7876 | ADAMS  | CLERK   | 7788 | 1983-01-12 | 1210 | NULL |     20 |
|  7934 | MILLER | CLERK   | 7782 | 1982-01-23 | 1430 | NULL |     10 |
+-------+--------+---------+------+------------+------+------+--------+
3 rows in set (0.001 sec)
</pre>

### 2. Employees whose second letter is ‘A’.

```sql
SELECT ENAME
FROM EMPLOYEE_MASTER
WHERE ENAME LIKE '_A%';
```

<pre>
+--------+
| ENAME  |
+--------+
| WARD   |
| MARTIN |
| JAMES  |
+--------+
3 rows in set (0.001 sec)
</pre>

### 3. Employees whose name is exactly 5 characters long.

```sql
SELECT ENAME
FROM EMPLOYEE_MASTER
WHERE ENAME LIKE '_____';
```

<pre>
+-------+
| ENAME |
+-------+
| SMITH |
| ALLEN |
| JONES |
| BLAKE |
| CLARK |
| SCOTT |
| ADAMS |
| JAMES |
+-------+
8 rows in set (0.001 sec)
</pre>

### 4. Employees whose second letter is ‘A’.

```sql
SELECT ENAME
FROM EMPLOYEE_MASTER
WHERE ENAME LIKE '_A%';
```

<pre>
+--------+
| ENAME  |
+--------+
| WARD   |
| MARTIN |
| JAMES  |
+--------+
3 rows in set (0.001 sec)
</pre>

### 5. Employees NOT working as salesman, clerk, or analyst.

```sql
SELECT ENAME
FROM EMPLOYEE_MASTER
WHERE JOB NOT IN ('SALESMAN', 'CLERK', 'ANALYST');
```

<pre>
+-------+
| ENAME |
+-------+
| JONES |
| BLAKE |
| CLARK |
| KING  |
+-------+
4 rows in set (0.001 sec)
</pre>

### 6. Employee name with annual salary (SAL \* 12), highest salary should appear first.

```sql
SELECT ENAME, SAL * 12 AS ANNUAL_SALARY
FROM EMPLOYEE_MASTER
ORDER BY SAL DESC;
```

<pre>
+--------+---------------+
| ENAME  | ANNUAL_SALARY |
+--------+---------------+
| KING   |         66000 |
| SCOTT  |         39600 |
| FORD   |         39600 |
| JONES  |         39276 |
| BLAKE  |         37620 |
| CLARK  |         32340 |
| ALLEN  |         19200 |
| TURNER |         18000 |
| MILLER |         17160 |
| MARTIN |         15000 |
| WARD   |         15000 |
| ADAMS  |         14520 |
| JAMES  |         12540 |
| SMITH  |         10560 |
+--------+---------------+
14 rows in set (0.001 sec)
</pre>

### 7. Display name, sal, hra, da, pf, totalsal for each employee. The output should be in the order of totalsal, hra - 15% of sal, da - 10% of sal, pf - 5% of sal. Total salary will be (sal* hra *da) - pf.

```sql
SELECT
  ENAME,
  SAL,
  SAL * 0.15 AS HRA,
  SAL * 0.10 AS DA,
  SAL * 0.05 AS PF,
  (SAL * (SAL * 0.15) * (SAL * 0.10) - (SAL * 0.05)) AS TOTALSAL
FROM EMPLOYEE_MASTER
ORDER BY TOTALSAL;
```

<pre>
+--------+------+--------+--------+--------+-----------------+
| ENAME  | SAL  | HRA    | DA     | PF     | TOTALSAL        |
+--------+------+--------+--------+--------+-----------------+
| SMITH  |  880 | 132.00 |  88.00 |  44.00 |   10222036.0000 |
| JAMES  | 1045 | 156.75 | 104.50 |  52.25 |   17117439.6250 |
| ADAMS  | 1210 | 181.50 | 121.00 |  60.50 |   26573354.5000 |
| WARD   | 1250 | 187.50 | 125.00 |  62.50 |   29296812.5000 |
| MARTIN | 1250 | 187.50 | 125.00 |  62.50 |   29296812.5000 |
| MILLER | 1430 | 214.50 | 143.00 |  71.50 |   43863033.5000 |
| TURNER | 1500 | 225.00 | 150.00 |  75.00 |   50624925.0000 |
| ALLEN  | 1600 | 240.00 | 160.00 |  80.00 |   61439920.0000 |
| CLARK  | 2695 | 404.25 | 269.50 | 134.75 |  293607650.8750 |
| BLAKE  | 3135 | 470.25 | 313.50 | 156.75 |  462172123.8750 |
| JONES  | 3273 | 490.95 | 327.30 | 163.65 |  525931447.6050 |
| FORD   | 3300 | 495.00 | 330.00 | 165.00 |  539054835.0000 |
| SCOTT  | 3300 | 495.00 | 330.00 | 165.00 |  539054835.0000 |
| KING   | 5500 | 825.00 | 550.00 | 275.00 | 2495624725.0000 |
+--------+------+--------+--------+--------+-----------------+
14 rows in set (0.001 sec)
</pre>

### 8. Increase salary by 10% for employees not eligible for commission.

```sql
UPDATE EMPLOYEE_MASTER
SET SAL = SAL * 1.10
WHERE COMM IS NULL;
```

<pre>
Query OK, 10 rows affected (0.005 sec)
Rows matched: 10  Changed: 10  Warnings: 0
</pre>

```sql
SELECT ENAME, SAL FROM EMPLOYEE_MASTER;
```

<pre>
+--------+------+
| ENAME  | SAL  |
+--------+------+
| SMITH  |  968 |
| ALLEN  | 1600 |
| WARD   | 1250 |
| JONES  | 3600 |
| MARTIN | 1250 |
| BLAKE  | 3449 |
| CLARK  | 2965 |
| SCOTT  | 3630 |
| KING   | 6050 |
| TURNER | 1500 |
| ADAMS  | 1331 |
| JAMES  | 1150 |
| FORD   | 3630 |
| MILLER | 1573 |
+--------+------+
14 rows in set (0.001 sec)
</pre>

### 9. Employees whose salary is more than 3000 after 20% increment.

```sql
SELECT ENAME, SAL * 1.20 AS INCREMENTED_SAL
FROM EMPLOYEE_MASTER
WHERE SAL * 1.20 > 3000;
```

<pre>
+-------+-----------------+
| ENAME | INCREMENTED_SAL |
+-------+-----------------+
| JONES |         4320.00 |
| BLAKE |         4138.80 |
| CLARK |         3558.00 |
| SCOTT |         4356.00 |
| KING  |         7260.00 |
| FORD  |         4356.00 |
+-------+-----------------+
6 rows in set (0.001 sec)
</pre>

### 10. Employees whose salary contains at least 3 digits.

```sql
SELECT ENAME, SAL
FROM EMPLOYEE_MASTER
WHERE SAL >= 100;
```

<pre>
+--------+------+
| ENAME  | SAL  |
+--------+------+
| SMITH  |  968 |
| ALLEN  | 1600 |
| WARD   | 1250 |
| JONES  | 3600 |
| MARTIN | 1250 |
| BLAKE  | 3449 |
| CLARK  | 2965 |
| SCOTT  | 3630 |
| KING   | 6050 |
| TURNER | 1500 |
| ADAMS  | 1331 |
| JAMES  | 1150 |
| FORD   | 3630 |
| MILLER | 1573 |
+--------+------+
14 rows in set (0.001 sec)
</pre>
