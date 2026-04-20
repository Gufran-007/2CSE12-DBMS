# PRACTICAL FILE ASSIGNMENT - 09

# DATE : 10/04/2026

### 1. Display the name of emp name who earns highest salary.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE_MASTER);
```

<pre>
Output:
+-------+
| ENAME |
+-------+
| KING  |
+-------+
1 row in set (0.010 sec)
</pre>

### 2. Display the employee number and name of employee working as clerk and earning highest salary among clerks.

```sql
MariaDB [iilm]> SELECT EMPNO, ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE JOB = 'CLERK'
    -> AND SAL = (
    ->     SELECT MAX(SAL)
    ->     FROM EMPLOYEE_MASTER
    ->     WHERE JOB = 'CLERK'
    -> );
```

<pre>
Output:
+-------+--------+
| EMPNO | ENAME  |
+-------+--------+
|  7934 | MILLER |
+-------+--------+
1 row in set (0.001 sec)
</pre>

### 3. Display the names of the salesman who earns a salary more than the highest salary of any clerk.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE JOB = 'SALESMAN'
    -> AND SAL > (
    ->     SELECT MAX(SAL)
    ->     FROM EMPLOYEE_MASTER
    ->     WHERE JOB = 'CLERK'
    -> );
```

<pre>
Output:
+--------+
| ENAME  |
+--------+
| ALLEN  |
| TURNER |
+--------+
2 rows in set (0.006 sec)
</pre>

### 4. Display the names of clerks who earn salary more than that of james of that of sal lesser than that of scott.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE JOB = 'CLERK'
    -> AND SAL > (
    ->     SELECT SAL FROM EMPLOYEE_MASTER WHERE ENAME = 'JAMES'
    -> )
    -> AND SAL < (
    ->     SELECT SAL FROM EMPLOYEE_MASTER WHERE ENAME = 'SCOTT'
    -> );
```

<pre>
Output:
+--------+
| ENAME  |
+--------+
| ADAMS  |
| MILLER |
+--------+
2 rows in set (0.001 sec)
</pre>

### 5. Display the names of employees who earn a sal more than that of james or that of salary greater than that of scott.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE SAL > (
    ->     SELECT SAL FROM EMPLOYEE_MASTER WHERE ENAME = 'JAMES'
    -> )
    -> OR SAL > (
    ->     SELECT SAL FROM EMPLOYEE_MASTER WHERE ENAME = 'SCOTT'
    -> );
```

<pre>
Output:
+--------+
| ENAME  |
+--------+
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| BLAKE  |
| CLARK  |
| SCOTT  |
| KING   |
| TURNER |
| ADAMS  |
| FORD   |
| MILLER |
+--------+
12 rows in set (0.001 sec)
</pre>

### 6. Display the names of the employees who earn highest salary in their respective departments.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER E
    -> WHERE SAL = (
    ->     SELECT MAX(SAL)
    ->     FROM EMPLOYEE_MASTER
    ->     WHERE DEPTNO = E.DEPTNO
    -> );
```

<pre>
Output:
+--------+
| ENAME  |
+--------+
| BLAKE  |
| SCOTT  |
| KING   |
| MILLER |
+--------+
4 rows in set (0.008 sec)
</pre>

### 7. Display the names of employees who earn highest salaries in their respective job groups.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER E
    -> WHERE SAL = (
    ->     SELECT MAX(SAL)
    ->     FROM EMPLOYEE_MASTER
    ->     WHERE JOB = E.JOB
    -> );
```

<pre>
Output:
+--------+
| ENAME  |
+--------+
| ALLEN  |
| JONES  |
| SCOTT  |
| KING   |
| FORD   |
| MILLER |
+--------+
6 rows in set (0.001 sec)
</pre>

### 8. Display the employee names who are working in accounting dept.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE DEPTNO = (
    ->     SELECT DEPTNO
    ->     FROM DEPARTMENT
    ->     WHERE DNAME = 'ACCOUNTING'
    -> );
```

<pre>
Output:
+-------+
| ENAME |
+-------+
| SMITH |
| JONES |
| CLARK |
| KING  |
| ADAMS |
| FORD  |
+-------+
6 rows in set (0.033 sec)
</pre>

### 9. Display the employee names who are working in mumbai.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE DEPTNO IN (
    ->     SELECT DEPTNO
    ->     FROM DEPARTMENT
    ->     WHERE LOCATION = 'MUMBAI'
    -> );
```

<pre>
Output:
+--------+
| ENAME  |
+--------+
| MILLER |
+--------+
1 row in set (0.001 sec)
</pre>

### 10. Display the job groups having total salary greater than the maximum salary for managers.

```sql
MariaDB [iilm]> SELECT JOB
    -> FROM EMPLOYEE_MASTER
    -> GROUP BY JOB
    -> HAVING SUM(SAL) > (
    ->     SELECT MAX(SAL)
    ->     FROM EMPLOYEE_MASTER
    ->     WHERE JOB = 'MANAGER'
    -> );
```

<pre>
Output:
+-----------+
| JOB       |
+-----------+
| ANALYST   |
| CLERK     |
| MANAGER   |
| PRESIDENT |
| SALESMAN  |
+-----------+
5 rows in set (0.006 sec)
</pre>
