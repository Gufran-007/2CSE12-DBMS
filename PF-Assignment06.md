# PRACTICAL FILE ASSIGNMENT - 06

## DATE : 16/02/2026

### 1. Display empno, ename, deptno from employee table. Instead of displaying department numbers, display the related department name (Use CASE function).

```sql
MariaDB [gufran]> SELECT EMPNO, ENAME,
    -> CASE DEPTNO
    -> WHEN 10 THEN 'RESEARCH'
    -> WHEN 20 THEN 'ACCOUNTING'
    -> WHEN 30 THEN 'SALES'
    -> WHEN 40 THEN 'OPERATIONS'
    -> END AS DEPT_NAME
    -> FROM EMPLOYEE_MASTER;
```

<pre>
+-------+--------+------------+
| EMPNO | ENAME  | DEPT_NAME  |
+-------+--------+------------+
|  7369 | SMITH  | ACCOUNTING |
|  7499 | ALLEN  | SALES      |
|  7521 | WARD   | SALES      |
|  7566 | JONES  | ACCOUNTING |
|  7654 | MARTIN | SALES      |
|  7698 | BLAKE  | SALES      |
|  7782 | CLARK  | ACCOUNTING |
|  7788 | SCOTT  | OPERATIONS |
|  7839 | KING   | ACCOUNTING |
|  7844 | TURNER | SALES      |
|  7876 | ADAMS  | ACCOUNTING |
|  7900 | JAMES  | SALES      |
|  7902 | FORD   | ACCOUNTING |
|  7934 | MILLER | RESEARCH   |
+-------+--------+------------+
14 rows in set (0.037 sec)
</pre>

### 2. Display your age in days.

```sql
MariaDB [gufran]> SELECT DATEDIFF(
    -> CURDATE(),
    -> '2004-08-24')
    -> AS AGE_IN_DAYS;
```

<pre>
+-------------+
| AGE_IN_DAYS |
+-------------+
|        7846 |
+-------------+
1 row in set (0.001 sec)
</pre>

### 3. Display your age in months.

```sql
MariaDB [gufran]> SELECT TIMESTAMPDIFF(
    -> MONTH,
    -> '2004-08-24',
    -> CURDATE())
    -> AS AGE_IN_MONTHS;
```

<pre>
+---------------+
| AGE_IN_MONTHS |
+---------------+
|           257 |
+---------------+
1 row in set (0.001 sec)
</pre>

### 4. Display the current date as 15th August Friday Nineteen Ninety-Seven(in sql year format).

```sql
MariaDB [gufran]> SELECT DATE_FORMAT(
    -> CURDATE(),
    -> '%D %M %W %Y')
    -> AS FORMATTED_DATE;
```

<pre>
+---------------------------+
| FORMATTED_DATE            |
+---------------------------+
| 16th February Monday 2026 |
+---------------------------+
1 row in set (0.001 sec)
</pre>

### 5&6. Display the following output for each row from employee table. Like "Scott has joined the company on Wednesday 13th August Nineteen Ninety".

```sql
MariaDB [gufran]> SELECT CONCAT(
    -> ENAME,
    -> ' has joined the company on ',
    -> DATE_FORMAT(HIREDATE, '%W %D %M %Y')
    -> ) AS REQUIRED_FORMAT
    -> FROM EMPLOYEE_MASTER;
```

<pre>
+--------------------------------------------------------------+
| REQUIRED_FORMAT                                              |
+--------------------------------------------------------------+
| SMITH has joined the company on Wednesday 17th December 1980 |
| ALLEN has joined the company on Friday 20th February 1981    |
| WARD has joined the company on Sunday 22nd February 1981     |
| JONES has joined the company on Thursday 2nd April 1981      |
| MARTIN has joined the company on Monday 28th September 1981  |
| BLAKE has joined the company on Friday 1st May 1981          |
| CLARK has joined the company on Tuesday 9th June 1981        |
| SCOTT has joined the company on Thursday 9th December 1982   |
| KING has joined the company on Tuesday 17th November 1981    |
| TURNER has joined the company on Tuesday 8th September 1981  |
| ADAMS has joined the company on Wednesday 12th January 1983  |
| JAMES has joined the company on Thursday 3rd December 1981   |
| FORD has joined the company on Thursday 3rd December 1981    |
| MILLER has joined the company on Saturday 23rd January 1982  |
+--------------------------------------------------------------+
14 rows in set (0.005 sec)
</pre>

### 7. Find the date for nearest Saturday after current date.

```sql
MariaDB [gufran]> SELECT DATE_ADD(
    -> CURDATE(),
    -> INTERVAL (5-WEEKDAY(CURDATE())) DAY
    -> ) AS NEXT_SATURDAY;
```

<pre>
+---------------+
| NEXT_SATURDAY |
+---------------+
| 2026-02-21    |
+---------------+
1 row in set (0.001 sec)
</pre>

### 8. Display current time.

```sql
MariaDB [gufran]> SELECT CURTIME() AS CURR_TIME;
```

<pre>
+-----------+
| CURR_TIME |
+-----------+
| 19:01:55  |
+-----------+
1 row in set (0.001 sec)
</pre>

### 9. Display the date three months before the current date.

```sql
MariaDB [gufran]> SELECT DATE_SUB(
    -> CURDATE(),
    -> INTERVAL 3 MONTH)
    -> AS DATE_3_MONTH_BEFORE;
```

<pre>
+---------------------+
| DATE_3_MONTH_BEFORE |
+---------------------+
| 2025-11-16          |
+---------------------+
1 row in set (0.001 sec)
</pre>

### 10. Display those employees who joined in the company in the month of Dec.

```sql
MariaDB [gufran]> SELECT ENAME, HIREDATE
    -> FROM EMPLOYEE_MASTER
    -> WHERE MONTH(HIREDATE)=12;
```

<pre>
+-------+------------+
| ENAME | HIREDATE   |
+-------+------------+
| SMITH | 1980-12-17 |
| SCOTT | 1982-12-09 |
| JAMES | 1981-12-03 |
| FORD  | 1981-12-03 |
+-------+------------+
4 rows in set (0.042 sec)
</pre>

### 11. Display those employees whose first 2 characters from hire date = last 2 characters of salary.

```sql
MariaDB [gufran]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE DAY(HIREDATE)=RIGHT(SAL, 2);
```

<pre>
Empty set (0.001 sec)
</pre>

### 12. Display those employees whose 10% of salary is equal to the year of joining.

```sql
MariaDB [gufran]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE (SAL*0.10)=YEAR(HIREDATE);
```

<pre>
Empty set (0.001 sec)
</pre>

### 13. Display those employees who joined the company before 15th of the months.

```sql
MariaDB [gufran]> SELECT *
    -> FROM EMPLOYEE_MASTER
    -> WHERE DAY(HIREDATE) < 15;
```

<pre>
+-------+--------+----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+----------+------+------------+------+------+--------+
|  7566 | JONES  | MANAGER  | 7839 | 1981-04-02 | 3600 | NULL |     20 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 3449 | NULL |     30 |
|  7782 | CLARK  | MANAGER  | 7839 | 1981-06-09 | 2965 | NULL |     20 |
|  7788 | SCOTT  | ANALYST  | 7566 | 1982-12-09 | 3630 | NULL |     40 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK    | 7788 | 1983-01-12 | 1331 | NULL |     20 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 | 1150 | NULL |     30 |
|  7902 | FORD   | ANALYST  | 7566 | 1981-12-03 | 3630 | NULL |     20 |
+-------+--------+----------+------+------------+------+------+--------+
8 rows in set (0.001 sec)
</pre>

### 14. Display those employees who has joined after 15th of the month.

```sql
MariaDB [gufran]> SELECT *
    -> FROM EMPLOYEE_MASTER
    -> WHERE DAY(HIREDATE) > 15;
```

<pre>
+-------+--------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+-----------+------+------------+------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  968 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 6050 | NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1573 | NULL |     10 |
+-------+--------+-----------+------+------------+------+------+--------+
6 rows in set (0.001 sec)
</pre>

### 15. Display those employees whose joining DATE is available in deptno.

```sql
MariaDB [gufran]> SELECT *
    -> FROM EMPLOYEE_MASTER
    -> WHERE HIREDATE IS NOT NULL;
```

<pre>
+-------+--------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+-----------+------+------------+------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  968 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 3600 | NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 3449 | NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2965 | NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3630 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 6050 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1331 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 | 1150 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3630 | NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1573 | NULL |     10 |
+-------+--------+-----------+------+------------+------+------+--------+
14 rows in set (0.001 sec)
</pre>
