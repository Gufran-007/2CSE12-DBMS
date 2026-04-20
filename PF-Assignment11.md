# PRACTICAL FILE ASSIGNMENT - 11

# DATE : 17/04/2026

### 1. Delete those employees who joined the company before 31-dec-82 while their dept location is ‘Mumbai’ or ‘Delhi’.

```sql
MariaDB [iilm]> DELETE FROM EMPLOYEE_MASTER
    -> WHERE HIREDATE < '1982-12-31'
    -> AND DEPTNO IN (
    ->     SELECT DEPTNO
    ->     FROM DEPARTMENT
    ->     WHERE LOCATION IN ('MUMBAI', 'DELHI')
    -> );
```

<pre>
Query OK, 2 rows affected (0.003 sec)

MariaDB [iilm]> SELECT * FROM EMPLOYEE_MASTER;
+-------+--------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+-----------+------+------------+------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975 | NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450 | NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000 | NULL |     20 |
+-------+--------+-----------+------+------------+------+------+--------+
12 rows in set (0.001 sec)
</pre>

### 2. Display employee name, job, deptname, location for all who are working as managers.

```sql
MariaDB [iilm]> SELECT E.ENAME, E.JOB, D.DNAME, D.LOCATION
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> WHERE E.JOB = 'MANAGER';
```

<pre>
+-------+---------+------------+-----------+
| ENAME | JOB     | DNAME      | LOCATION  |
+-------+---------+------------+-----------+
| JONES | MANAGER | ACCOUNTING | CHENNAI   |
| CLARK | MANAGER | ACCOUNTING | CHENNAI   |
| BLAKE | MANAGER | SALES      | HYDERABAD |
+-------+---------+------------+-----------+
3 rows in set (0.001 sec)
</pre>

### 3. Display name and salary of ford if his sal is equal to high sal of his grade.

```sql
MariaDB [iilm]> SELECT E.ENAME, E.SAL
    -> FROM EMPLOYEE_MASTER E
    -> JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE E.ENAME = 'FORD'
    -> AND E.SAL = S.HISAL;
```

<pre>
+-------+------+
| ENAME | SAL  |
+-------+------+
| FORD  | 3000 |
+-------+------+
1 row in set (0.001 sec)
</pre>

### 4. Find out the top 5 earners of company.

```sql
MariaDB [iilm]> SELECT ENAME, SAL
    -> FROM EMPLOYEE_MASTER
    -> ORDER BY SAL DESC
    -> LIMIT 5;
```

<pre>
+-------+------+
| ENAME | SAL  |
+-------+------+
| KING  | 5000 |
| FORD  | 3000 |
| JONES | 2975 |
| BLAKE | 2850 |
| CLARK | 2450 |
+-------+------+
5 rows in set (0.001 sec)
</pre>

### 5. Display the name of those employees who are getting highest salary.

```sql
MariaDB [iilm]>  SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE_MASTER);
```

<pre>
+-------+
| ENAME |
+-------+
| KING  |
+-------+
1 row in set (0.001 sec)
</pre>

### 6. Display those employees whose salary is equal to average of maximum and minimum.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE SAL = (
    ->     (SELECT MAX(SAL) FROM EMPLOYEE_MASTER) +
    ->     (SELECT MIN(SAL) FROM EMPLOYEE_MASTER)
    -> ) / 2;
```

<pre>
Empty set (0.001 sec)
</pre>

### 7. Display dname where at least 3 are working and display only dname.

```sql
MariaDB [iilm]> SELECT D.DNAME
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> GROUP BY D.DNAME
    -> HAVING COUNT(*) >= 3;
```

<pre>
+------------+
| DNAME      |
+------------+
| ACCOUNTING |
| SALES      |
+------------+
2 rows in set (0.001 sec)
</pre>

### 8. Display name of those managers whose salary is more than average salary of company.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE JOB = 'MANAGER'
    -> AND SAL > (SELECT AVG(SAL) FROM EMPLOYEE_MASTER);
```

<pre>
+-------+
| ENAME |
+-------+
| JONES |
| BLAKE |
| CLARK |
+-------+
3 rows in set (0.001 sec)
</pre>

### 9. Display those managers name whose salary is more than average salary of his employees.

```sql
MariaDB [iilm]> SELECT M.ENAME
    -> FROM EMPLOYEE_MASTER M
    -> JOIN EMPLOYEE_MASTER E
    -> ON M.EMPNO = E.MGR
    -> GROUP BY M.ENAME, M.SAL
    -> HAVING M.SAL > AVG(E.SAL);
```

<pre>
+-------+
| ENAME |
+-------+
| BLAKE |
| FORD  |
| KING  |
+-------+
3 rows in set (0.001 sec)
</pre>

### 10. Display employee name, sal, comm and net pay for those employees whose net pay are greater than or equal to any other employee salary of the company.

```sql
MariaDB [iilm]> SELECT ENAME, SAL, COMM, (SAL + IFNULL(COMM,0)) AS NET_PAY
    -> FROM EMPLOYEE_MASTER
    -> WHERE (SAL + IFNULL(COMM,0)) >= ANY (
    ->     SELECT SAL FROM EMPLOYEE_MASTER
    -> );
```

<pre>
+--------+------+------+---------+
| ENAME  | SAL  | COMM | NET_PAY |
+--------+------+------+---------+
| SMITH  |  800 | NULL |     800 |
| ALLEN  | 1600 |  300 |    1900 |
| WARD   | 1250 |  300 |    1550 |
| JONES  | 2975 | NULL |    2975 |
| MARTIN | 1250 | 1400 |    2650 |
| BLAKE  | 2850 | NULL |    2850 |
| CLARK  | 2450 | NULL |    2450 |
| KING   | 5000 | NULL |    5000 |
| TURNER | 1500 |    0 |    1500 |
| ADAMS  | 1100 | NULL |    1100 |
| JAMES  |  950 | NULL |     950 |
| FORD   | 3000 | NULL |    3000 |
+--------+------+------+---------+
12 rows in set (0.001 sec)
</pre>
