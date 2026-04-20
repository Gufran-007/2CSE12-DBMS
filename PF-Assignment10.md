# PRACTICAL FILE ASSIGNMENT - 10

# DATE : 13/04/2026

### 1. Display the names of employees from department number 10 with salary greater than that of any employee working in other departments.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE DEPTNO = 10
    -> AND SAL > ANY (
    ->     SELECT SAL
    ->     FROM EMPLOYEE_MASTER
    ->     WHERE DEPTNO <> 10
    -> );
```

<pre>
+--------+
| ENAME  |
+--------+
| MILLER |
+--------+
1 row in set (0.049 sec)
</pre>

### 2. Display the names of employee from department number 10 with salary greater than that of all employee working in other departments.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE DEPTNO = 10
    -> AND SAL > ALL (
    ->     SELECT SAL
    ->     FROM EMPLOYEE_MASTER
    ->     WHERE DEPTNO <> 10
    -> );
```

<pre>
Empty set (0.001 sec)
</pre>

### 3. Display the details of employees who are in sales dept and grade is C.

```sql
MariaDB [iilm]> SELECT E.*
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE D.DNAME = 'SALES'
    -> AND S.GRADE = 'C';
```

<pre>
+-------+--------+----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+----------+------+------------+------+------+--------+
|  7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500 |    0 |     30 |
+-------+--------+----------+------+------------+------+------+--------+
2 rows in set (0.008 sec)
</pre>

### 4. Display those who are not managers and who manages anyone.

```sql
MariaDB [iilm]> SELECT *
    -> FROM EMPLOYEE_MASTER
    -> WHERE JOB <> 'MANAGER'
    -> AND EMPNO IN (
    ->     SELECT MGR FROM EMPLOYEE_MASTER WHERE MGR IS NOT NULL
    -> );
```

<pre>
+-------+-------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+-------+-----------+------+------------+------+------+--------+
|  7788 | SCOTT | ANALYST   | 7566 | 1982-12-09 | 3000 | NULL |     40 |
|  7839 | KING  | PRESIDENT | NULL | 1981-11-17 | 5000 | NULL |     20 |
|  7902 | FORD  | ANALYST   | 7566 | 1981-12-03 | 3000 | NULL |     20 |
+-------+-------+-----------+------+------------+------+------+--------+
3 rows in set (0.001 sec)
</pre>

### 5. Display those employees whose manager name is jones.

```sql
MariaDB [iilm]> SELECT E.ENAME
    -> FROM EMPLOYEE_MASTER E
    -> JOIN EMPLOYEE_MASTER M
    -> ON E.MGR = M.EMPNO
    -> WHERE M.ENAME = 'JONES';
```

<pre>
+-------+
| ENAME |
+-------+
| SCOTT |
| FORD  |
+-------+
2 rows in set (0.001 sec)
</pre>

### 6. Display ename who are working in sales dept.

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER
    -> WHERE DEPTNO = (
    ->     SELECT DEPTNO
    ->     FROM DEPARTMENT
    ->     WHERE DNAME = 'SALES'
    -> );
```

<pre>
+--------+
| ENAME  |
+--------+
| ALLEN  |
| WARD   |
| MARTIN |
| BLAKE  |
| TURNER |
| JAMES  |
+--------+
6 rows in set (0.001 sec)
</pre>

### 7. Display employee name, deptname, salary and comm. For those sal in between 2000 to 5000 while location is Chennai.

```sql
MariaDB [iilm]> SELECT E.ENAME, D.DNAME, E.SAL, E.COMM
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> WHERE E.SAL BETWEEN 2000 AND 5000
    -> AND D.LOCATION = 'CHENNAI';
```

<pre>
+-------+------------+------+------+
| ENAME | DNAME      | SAL  | COMM |
+-------+------------+------+------+
| JONES | ACCOUNTING | 2975 | NULL |
| CLARK | ACCOUNTING | 2450 | NULL |
| KING  | ACCOUNTING | 5000 | NULL |
| FORD  | ACCOUNTING | 3000 | NULL |
+-------+------------+------+------+
4 rows in set (0.001 sec)
</pre>

### 8. Display those employees whose salary greater than his manager salary.

```sql
MariaDB [iilm]> SELECT E.ENAME
    -> FROM EMPLOYEE_MASTER E
    -> JOIN EMPLOYEE_MASTER M
    -> ON E.MGR = M.EMPNO
    -> WHERE E.SAL > M.SAL;
```

<pre>
+-------+
| ENAME |
+-------+
| SCOTT |
| FORD  |
+-------+
2 rows in set (0.001 sec)
</pre>

### 9. Display those employees who are working in the same dept where his manager is working.

```sql
MariaDB [iilm]> SELECT E.ENAME
    -> FROM EMPLOYEE_MASTER E
    -> JOIN EMPLOYEE_MASTER M
    -> ON E.MGR = M.EMPNO
    -> WHERE E.DEPTNO = M.DEPTNO;
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
| TURNER |
| JAMES  |
| FORD   |
+--------+
9 rows in set (0.001 sec)
</pre>

### 10. Display grade and employees name for the dept no 10 or 30 but grade is not D, while joined the company before 31-dec-82.

```sql
MariaDB [iilm]> SELECT E.ENAME, S.GRADE
    -> FROM EMPLOYEE_MASTER E
    -> JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE E.DEPTNO IN (10, 30)
    -> AND S.GRADE <> 'D'
    -> AND E.HIREDATE < '1982-12-31';
```

<pre>
+--------+-------+
| ENAME  | GRADE |
+--------+-------+
| ALLEN  | C     |
| WARD   | B     |
| MARTIN | B     |
| TURNER | C     |
| JAMES  | A     |
| MILLER | B     |
+--------+-------+
6 rows in set (0.001 sec)
</pre>
