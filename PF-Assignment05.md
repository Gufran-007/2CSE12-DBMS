# PRACTICAL FILE ASSIGNMENT - 05

## DATE : 11/02/26

### 1. Display the total number of employee working in the company.

```sql
SELECT COUNT(*) AS Total_Employees
FROM EMPLOYEE_MASTER;
```

<pre>
+----------+
| COUNT(*) |
+----------+
|       14 |
+----------+
1 row in set (0.079 sec)
</pre>

### 2. Display the total salary being paid to all employees.

```sql
SELECT SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE_MASTER;
```

<pre>
+--------------+
| TOTAL_SALARY |
+--------------+
|        33946 |
+--------------+
1 row in set (0.033 sec)
</pre>

### 3. Display the maximum salary from employee table.

```sql
SELECT MAX(SAL)
FROM EMPLOYEE_MASTER;
```

<pre>
+----------+
| MAX(SAL) |
+----------+
|     6050 |
+----------+
1 row in set (0.034 sec)
</pre>

### 4. Display the minimum salary from employee table.

```sql
SELECT MIN(SAL)
FROM EMPLOYEE_MASTER;
```

<pre>
+----------+
| MIN(SAL) |
+----------+
|      968 |
+----------+
1 row in set (0.001 sec)
</pre>

### 5. Display the average salary from employee table.

```sql
SELECT AVG(SAL)
FROM EMPLOYEE_MASTER;
```

<pre>
+-----------+
| AVG(SAL)  |
+-----------+
| 2424.7143 |
+-----------+
1 row in set (0.001 sec)
</pre>

### 6. Display the maximum salary being paid to clerk.

```sql
SELECT MAX(SAL)
FROM EMPLOYEE_MASTER
WHERE JOB = 'CLERK';
```

<pre>
+----------+
| MAX(SAL) |
+----------+
|     1573 |
+----------+
1 row in set (0.035 sec)
</pre>

### 7. Display the maximum salary being paid in dept no 20.

```sql
SELECT MAX(SAL) AS MAXIMUM_SALARY
FROM EMPLOYEE_MASTER
WHERE DEPTNO = 20;
```

<pre>
+----------------+
| MAXIMUM_SALARY |
+----------------+
|           6050 |
+----------------+
1 row in set (0.037 sec)
</pre>

### 8. Display the minimum salary paid to any salesman.

```sql
SELECT MIN(SAL) AS MINIMUM_SALARY
FROM EMPLOYEE_MASTER
WHERE JOB = 'SALESMAN';
```

<pre>
+----------------+
| MINIMUM_SALARY |
+----------------+
|           1250 |
+----------------+
1 row in set (0.001 sec)
</pre>

### 9. Display the average salary drawn by managers.

```sql
SELECT AVG(SAL) AS AVERAGE_SALARY
FROM EMPLOYEE_MASTER
WHERE JOB = 'MANAGER';
```

<pre>
+----------------+
| AVERAGE_SALARY |
+----------------+
|      3338.0000 |
+----------------+
1 row in set (0.001 sec)
</pre>

### 10. Display the total salary drawn by analyst working in dept no 40.

```sql
SELECT SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE_MASTER
WHERE JOB = 'ANALYST'
AND DEPTNO = 40;
```

<pre>
+--------------+
| TOTAL_SALARY |
+--------------+
|         3630 |
+--------------+
1 row in set (0.034 sec)
</pre>

### 11. Display the names of the employee in Uppercase.

```sql
SELECT UPPER(ENAME)
FROM EMPLOYEE_MASTER;
```

<pre>
+--------------+
| UCASE(ENAME) |
+--------------+
| SMITH        |
| ALLEN        |
| WARD         |
| JONES        |
| MARTIN       |
| BLAKE        |
| CLARK        |
| SCOTT        |
| KING         |
| TURNER       |
| ADAMS        |
| JAMES        |
| FORD         |
| MILLER       |
+--------------+
14 rows in set (0.033 sec)
</pre>

### 12. Display the names of the employee in Lowercase.

```sql
SELECT LOWER(ENAME)
FROM EMPLOYEE_MASTER;
```

<pre>
+--------------+
| LCASE(ENAME) |
+--------------+
| smith        |
| allen        |
| ward         |
| jones        |
| martin       |
| blake        |
| clark        |
| scott        |
| king         |
| turner       |
| adams        |
| james        |
| ford         |
| miller       |
+--------------+
14 rows in set (0.001 sec)
</pre>

### 13. Display the names of the employee in Proper case.

```sql
SELECT CONCAT(
UCASE(SUBSTR(ENAME, 1, 1)),
LCASE(SUBSTR(ENAME, 2))
) AS EMP_NAME_ProperCase
FROM EMPLOYEE_MASTER;
```

<pre>
+---------------------+
| EMP_NAME_ProperCase |
+---------------------+
| Smith               |
| Allen               |
| Ward                |
| Jones               |
| Martin              |
| Blake               |
| Clark               |
| Scott               |
| King                |
| Turner              |
| Adams               |
| James               |
| Ford                |
| Miller              |
+---------------------+
14 rows in set (0.034 sec)
</pre>

### 14. Display the length of Your name using appropriate function.

```sql
SELECT LENGTH('GUFRAN');
```

<pre>
+------------------+
| LENGTH('GUFRAN') |
+------------------+
|                6 |
+------------------+
1 row in set (0.001 sec)
</pre>

### 15. Display the length of all the employee names.

```sql
SELECT LENGTH(ENAME) AS NAME_LENGTH
FROM EMPLOYEE_MASTER;
```

<pre>
+-------------+
| NAME_LENGTH |
+-------------+
|           5 |
|           5 |
|           4 |
|           5 |
|           6 |
|           5 |
|           5 |
|           5 |
|           4 |
|           6 |
|           5 |
|           5 |
|           4 |
|           6 |
+-------------+
14 rows in set (0.001 sec)
</pre>
