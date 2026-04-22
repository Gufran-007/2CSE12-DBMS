# PRACTICAL FILE ASSIGNMENT - 11

# DATE : 20/04/2026

### 1. Display those employees whose salary is less than his manager but more than salary of any other managers.

```sql
MariaDB [iilm]> SELECT E.ENAME
    -> FROM EMPLOYEE_MASTER E
    -> JOIN EMPLOYEE_MASTER M
    -> ON E.MGR = M.EMPNO
    -> WHERE E.SAL < M.SAL
    -> AND E.SAL > ANY (
    ->  SELECT SAL FROM EMPLOYEE_MASTER
    -> );
```
<pre>
+--------+
| ENAME  |
+--------+
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| BLAKE  |
| CLARK  |
| TURNER |
| JAMES  |
+--------+
8 rows in set (0.068 sec)
</pre>

### 2. Find out the number of employees whose salary is greater than their manager salary?

```sql
MariaDB [iilm]> SELECT COUNT(*) AS COUNT
    -> FROM EMPLOYEE_MASTER E
    -> JOIN EMPLOYEE_MASTER M
    -> ON E.MGR = M.EMPNO
    -> WHERE E.SAL > M.SAL;
```
<pre>
+-------+
| COUNT |
+-------+
|     1 |
+-------+
1 row in set (0.001 sec)
</pre>

### 3. Display those managers who are not working under president but they are working under any other manager?

```sql
MariaDB [iilm]> SELECT E.ENAME
    -> FROM EMPLOYEE_MASTER E
    -> JOIN EMPLOYEE_MASTER M
    -> ON E.MGR = M.EMPNO
    -> WHERE E.JOB = 'MANAGER'
    -> OR M.JOB <> 'PRESIDENT';
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
| BLAKE  |
| CLARK  |
| TURNER |
| JAMES  |
| FORD   |
+--------+
10 rows in set (0.001 sec)
</pre>

### 4. Delete those department where no employee working?

```sql
MariaDB [iilm]> DELETE FROM DEPARTMENT
    -> WHERE DEPTNO NOT IN (SELECT DISTINCT(DEPTNO) FROM EMPLOYEE_MASTER);
```
<pre>

</pre>

### 5. Delete those records from emp table whose deptno not available in dept table?

```sql
MariaDB [iilm]> DELETE FROM DEPARTMENT
    -> WHERE DEPTNO NOT IN (SELECT (DEPTNO) FROM DEPARTMENT);
```
<pre>
Query OK, 0 rows affected (0.001 sec)
</pre>

### 6. Display those earners whose salary is out of the grade available in sal grade table?

```sql
MariaDB [iilm]> SELECT ENAME, SAL
    -> FROM EMPLOYEE_MASTER
    -> WHERE SAL NOT BETWEEN
    -> (SELECT MIN(LOSAL) FROM SALGRADE)
    -> AND
    -> (SELECT MAX(HISAL) FROM SALGRADE);
```
<pre>
Empty set (0.002 sec)
</pre>

### 7. Display employee name, sal, comm. And whose net pay is greater than any other in the company?

```sql
MariaDB [iilm]> SELECT ENAME, SAL, COMM,
    -> (SAL + IFNULL(COMM, 0)) AS NET_PAY
    -> FROM EMPLOYEE_MASTER
    -> WHERE (SAL + IFNULL(COMM, 0)) > ANY (SELECT SAL FROM EMPLOYEE_MASTER);
```
<pre>
+--------+------+------+---------+
| ENAME  | SAL  | COMM | NET_PAY |
+--------+------+------+---------+
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
11 rows in set (0.001 sec)
</pre>

### 8. Display those employees who are working in sales or research?

```sql
MariaDB [iilm]> SELECT ENAME
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D
    -> ON E.DEPTNO = D.DEPTNO
    -> WHERE DNAME IN("SALES", "RESEARCH");
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
6 rows in set (0.007 sec)
</pre>

### 9. Display the grade of jones?

```sql
MariaDB [iilm]> SELECT E.ENAME, S.GRADE
    -> FROM EMPLOYEE_MASTER E
    -> JOIN SALGRADE S
    -> ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE E.ENAME = 'JONES';
```
<pre>
+-------+-------+
| ENAME | GRADE |
+-------+-------+
| JONES | D     |
+-------+-------+
1 row in set (0.001 sec)
</pre>

### 10. Display the department name the no of characters of which is equal to no of employees in any other department?

```sql
MariaDB [iilm]> SELECT DNAME
    -> FROM DEPARTMENT
    -> WHERE LENGTH(DNAME) IN
    -> (SELECT COUNT(*)
    -> FROM EMPLOYEE_MASTER
    -> ORDER BY DEPTNO);
```
<pre>
Empty set (0.001 sec)
</pre>

