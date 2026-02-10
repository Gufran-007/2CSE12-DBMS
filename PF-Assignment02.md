# PRACTICAL FILE ASSIGNMENT - 02

## DATE : 02/02/26

### 1. List all distinct jobs in Employee.

```sql
SELECT DISTINCT JOB
FROM EMPLOYEE_MASTER;
```

<pre>
+-----------+
| JOB       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
5 rows in set (0.034 sec)
</pre>

### 2. List all information about employee in Department Number 30.

```sql
SELECT *
FROM EMPLOYEE_MASTER
WHERE DEPTNO = 30;
```

<pre>
+-------+--------+----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+----------+------+------------+------+------+--------+
|  7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7654 | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 3135 | NULL |     30 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 | 1045 | NULL |     30 |
+-------+--------+----------+------+------------+------+------+--------+
6 rows in set (0.001 sec)
</pre>

### 3. Find all department number with department names greater than 20.

```sql
SELECT DEPTNO, DNAME
FROM DEPARTMENT
WHERE DEPTNO > 20;
```

<pre>
+--------+------------+
| DEPTNO | DNAME      |
+--------+------------+
|     30 | SALES      |
|     40 | OPERATIONS |
+--------+------------+
2 rows in set (0.034 sec)
</pre>

### 4. Find all information about all the managers as well as the clerks in department 30.

```sql
SELECT *
FROM EMPLOYEE_MASTER
WHERE DEPTNO = 30
AND (JOB = 'MANAGER' OR JOB = 'CLERK');
```

<pre>
+-------+-------+---------+------+------------+------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+-------+---------+------+------------+------+------+--------+
|  7698 | BLAKE | MANAGER | 7839 | 1981-05-01 | 3135 | NULL |     30 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 | 1045 | NULL |     30 |
+-------+-------+---------+------+------------+------+------+--------+
2 rows in set (0.001 sec)
</pre>

### 5. List the Employee name, Employee numbers and department of all clerks.

```sql
SELECT ENAME, EMPNO, DEPTNO
FROM EMPLOYEE_MASTER
WHERE JOB = 'CLERK';
```

<pre>
+--------+-------+--------+
| ENAME  | EMPNO | DEPTNO |
+--------+-------+--------+
| SMITH  |  7369 |     20 |
| ADAMS  |  7876 |     20 |
| JAMES  |  7900 |     30 |
| MILLER |  7934 |     10 |
+--------+-------+--------+
4 rows in set (0.001 sec)
</pre>

### 6. Find all managers not in department 30.

```sql
SELECT *
FROM EMPLOYEE_MASTER
WHERE JOB = 'MANAGER'
AND DEPTNO <> 30;
```

<pre>
+-------+-------+---------+------+------------+------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+-------+---------+------+------------+------+------+--------+
|  7566 | JONES | MANAGER | 7839 | 1981-04-02 | 3273 | NULL |     20 |
|  7782 | CLARK | MANAGER | 7839 | 1981-06-09 | 2695 | NULL |     20 |
+-------+-------+---------+------+------------+------+------+--------+
2 rows in set (0.001 sec)
</pre>

### 7. List information about all Employees in department 10 who are not manager or clerks.

```sql
SELECT *
FROM EMPLOYEE_MASTER
WHERE DEPTNO = 10
AND JOB NOT IN ('MANAGER', 'CLERK');
```

<pre>
Empty set (0.001 sec)
</pre>

### 8. Find Employees and jobs earning between 1200 and 1400.

```sql
SELECT ENAME, JOB
FROM EMPLOYEE_MASTER
WHERE SAL BETWEEN 1200 AND 1400;
```

<pre>
+--------+----------+
| ENAME  | JOB      |
+--------+----------+
| WARD   | SALESMAN |
| MARTIN | SALESMAN |
| ADAMS  | CLERK    |
+--------+----------+
3 rows in set (0.001 sec)
</pre>

### 9. List Name and Department Number of employee who are clerks, analyst or salesman.

```sql
SELECT ENAME, DEPTNO
FROM EMPLOYEE_MASTER
WHERE JOB IN ('CLERK', 'ANALYST', 'SALESMAN');
```

<pre>
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| SMITH  |     20 |
| ALLEN  |     30 |
| WARD   |     30 |
| MARTIN |     30 |
| SCOTT  |     40 |
| TURNER |     30 |
| ADAMS  |     20 |
| JAMES  |     30 |
| FORD   |     20 |
| MILLER |     10 |
+--------+--------+
10 rows in set (0.001 sec)
</pre>

### 10. List Name and Department Number of employee whose names begin with M.

```sql
SELECT ENAME, DEPTNO
FROM EMPLOYEE_MASTER
WHERE ENAME LIKE 'M%';
```

<pre>
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| MARTIN |     30 |
| MILLER |     10 |
+--------+--------+
2 rows in set (0.001 sec)
</pre>
