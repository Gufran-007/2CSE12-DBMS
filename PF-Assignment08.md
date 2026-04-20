# PRACTICAL FILE ASSIGNMENT - 08

# DATE : 30/03/2026

### 1. Display all employees with their dept name.

```sql
MariaDB [iilm]> SELECT E.ENAME, D.DNAME
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> ORDER BY D.DEPTNO;
```

<pre>
Output:
+--------+------------+
| ENAME  | DNAME      |
+--------+------------+
| MILLER | RESEARCH   |
| SMITH  | ACCOUNTING |
| JONES  | ACCOUNTING |
| CLARK  | ACCOUNTING |
| KING   | ACCOUNTING |
| ADAMS  | ACCOUNTING |
| FORD   | ACCOUNTING |
| ALLEN  | SALES      |
| WARD   | SALES      |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| TURNER | SALES      |
| JAMES  | SALES      |
| SCOTT  | OPERATIONS |
+--------+------------+
14 rows in set (0.127 sec)
</pre>

### 2. Display those employees whose manager names is jones, and also display their manager name.

```sql
MariaDB [iilm]> SELECT E.ENAME, M.ENAME AS MANAGER
    -> FROM EMPLOYEE_MASTER E
    -> JOIN EMPLOYEE_MASTER M
    -> ON E.MGR = M.EMPNO
    -> WHERE M.ENAME = 'JONES';
```

<pre>
Output:
+-------+---------+
| ENAME | MANAGER |
+-------+---------+
| SCOTT | JONES   |
| FORD  | JONES   |
+-------+---------+
2 rows in set (0.039 sec)
</pre>

### 3. Display employee name, his job, his dept name, his manager name, his grade and make out of an under department wise.

```sql
MariaDB [iilm]> SELECT E.ENAME, E.JOB, D.DNAME,
    -> M.ENAME AS MANAGER,
    -> S.GRADE
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> LEFT JOIN EMPLOYEE_MASTER M ON E.MGR = M.EMPNO
    -> JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> ORDER BY D.DNAME;
```

<pre>
Output:
+--------+-----------+------------+---------+-------+
| ENAME  | JOB       | DNAME      | MANAGER | GRADE |
+--------+-----------+------------+---------+-------+
| FORD   | ANALYST   | ACCOUNTING | JONES   | D     |
| ADAMS  | CLERK     | ACCOUNTING | SCOTT   | A     |
| JONES  | MANAGER   | ACCOUNTING | KING    | D     |
| KING   | PRESIDENT | ACCOUNTING | NULL    | E     |
| CLARK  | MANAGER   | ACCOUNTING | KING    | D     |
| SMITH  | CLERK     | ACCOUNTING | FORD    | A     |
| SCOTT  | ANALYST   | OPERATIONS | JONES   | D     |
| MILLER | CLERK     | RESEARCH   | CLARK   | B     |
| MARTIN | SALESMAN  | SALES      | BLAKE   | B     |
| ALLEN  | SALESMAN  | SALES      | BLAKE   | C     |
| BLAKE  | MANAGER   | SALES      | KING    | D     |
| JAMES  | CLERK     | SALES      | BLAKE   | A     |
| TURNER | SALESMAN  | SALES      | BLAKE   | C     |
| WARD   | SALESMAN  | SALES      | BLAKE   | B     |
+--------+-----------+------------+---------+-------+
14 rows in set (0.021 sec)
</pre>

### 4. List out all the employees name, job, and salary grade and department name for everyone in the company except ‘clerk’. Sort on salary display the highest salary.

```sql
MariaDB [iilm]> SELECT E.ENAME, E.JOB, E.SAL, S.GRADE, D.DEPTNO
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE E.JOB <> 'CLERK'
    -> ORDER BY E.SAL DESC;
```

<pre>
Output:
+--------+-----------+------+-------+--------+
| ENAME  | JOB       | SAL  | GRADE | DEPTNO |
+--------+-----------+------+-------+--------+
| KING   | PRESIDENT | 5000 | E     |     20 |
| SCOTT  | ANALYST   | 3000 | D     |     40 |
| FORD   | ANALYST   | 3000 | D     |     20 |
| JONES  | MANAGER   | 2975 | D     |     20 |
| BLAKE  | MANAGER   | 2850 | D     |     30 |
| CLARK  | MANAGER   | 2450 | D     |     20 |
| ALLEN  | SALESMAN  | 1600 | C     |     30 |
| TURNER | SALESMAN  | 1500 | C     |     30 |
| WARD   | SALESMAN  | 1250 | B     |     30 |
| MARTIN | SALESMAN  | 1250 | B     |     30 |
+--------+-----------+------+-------+--------+
10 rows in set (0.001 sec)
</pre>

### 5. Display employee name, his job and his manager. Display also employees who are without manager.

```sql
MariaDB [iilm]> SELECT E.ENAME, E.JOB, M.MGR
    -> FROM EMPLOYEE_MASTER E
    -> LEFT JOIN EMPLOYEE_MASTER M
    -> ON M.MGR = E.EMPNO;
```

<pre>
Output:
+--------+-----------+------+
| ENAME  | JOB       | MGR  |
+--------+-----------+------+
| FORD   | ANALYST   | 7902 |
| BLAKE  | MANAGER   | 7698 |
| BLAKE  | MANAGER   | 7698 |
| KING   | PRESIDENT | 7839 |
| BLAKE  | MANAGER   | 7698 |
| KING   | PRESIDENT | 7839 |
| KING   | PRESIDENT | 7839 |
| JONES  | MANAGER   | 7566 |
| BLAKE  | MANAGER   | 7698 |
| SCOTT  | ANALYST   | 7788 |
| BLAKE  | MANAGER   | 7698 |
| JONES  | MANAGER   | 7566 |
| CLARK  | MANAGER   | 7782 |
| SMITH  | CLERK     | NULL |
| ALLEN  | SALESMAN  | NULL |
| WARD   | SALESMAN  | NULL |
| MARTIN | SALESMAN  | NULL |
| TURNER | SALESMAN  | NULL |
| ADAMS  | CLERK     | NULL |
| JAMES  | CLERK     | NULL |
| MILLER | CLERK     | NULL |
+--------+-----------+------+
21 rows in set (0.001 sec)
</pre>

### 6. List the employee name, job, annual salary, deptno, dept name and grade who earn 36000 a year or who are not clerks.

```sql
MariaDB [iilm]> SELECT E.ENAME, E.JOB, (E.SAL*12) AS ANNUAL_SALARY, E.DEPTNO, D.DNAME, S.GRADE
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE (E.SAL*12) >= 36000 OR E.SAL <> 'CLERK';
```

<pre>
Output:
+--------+-----------+---------------+--------+------------+-------+
| ENAME  | JOB       | ANNUAL_SALARY | DEPTNO | DNAME      | GRADE |
+--------+-----------+---------------+--------+------------+-------+
| SMITH  | CLERK     |          9600 |     20 | ACCOUNTING | A     |
| ADAMS  | CLERK     |         13200 |     20 | ACCOUNTING | A     |
| JAMES  | CLERK     |         11400 |     30 | SALES      | A     |
| MILLER | CLERK     |         15600 |     10 | RESEARCH   | B     |
| WARD   | SALESMAN  |         15000 |     30 | SALES      | B     |
| MARTIN | SALESMAN  |         15000 |     30 | SALES      | B     |
| ALLEN  | SALESMAN  |         19200 |     30 | SALES      | C     |
| TURNER | SALESMAN  |         18000 |     30 | SALES      | C     |
| JONES  | MANAGER   |         35700 |     20 | ACCOUNTING | D     |
| CLARK  | MANAGER   |         29400 |     20 | ACCOUNTING | D     |
| FORD   | ANALYST   |         36000 |     20 | ACCOUNTING | D     |
| BLAKE  | MANAGER   |         34200 |     30 | SALES      | D     |
| SCOTT  | ANALYST   |         36000 |     40 | OPERATIONS | D     |
| KING   | PRESIDENT |         60000 |     20 | ACCOUNTING | E     |
+--------+-----------+---------------+--------+------------+-------+
14 rows in set, 1 warning (0.034 sec)
</pre>

### 7. List ename, job, annual sal, deptno, dname and grade who earn 30000 per year and who are not clerks.

```sql
MariaDB [iilm]> SELECT E.ENAME, E.JOB, (E.SAL*12) AS ANNUAL_SALARY, E.DEPTNO, D.DNAME, S.GRADE
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE (E.SAL*12) >= 36000 AND E.SAL <> 'CLERK';
```

<pre>
Output:
+-------+-----------+---------------+--------+------------+-------+
| ENAME | JOB       | ANNUAL_SALARY | DEPTNO | DNAME      | GRADE |
+-------+-----------+---------------+--------+------------+-------+
| FORD  | ANALYST   |         36000 |     20 | ACCOUNTING | D     |
| SCOTT | ANALYST   |         36000 |     40 | OPERATIONS | D     |
| KING  | PRESIDENT |         60000 |     20 | ACCOUNTING | E     |
+-------+-----------+---------------+--------+------------+-------+
3 rows in set, 1 warning (0.002 sec)
</pre>

### 8. List out all employees by name and number along with their manager’s name and number also display ‘no manager’ who has no manager.

```sql
 SELECT E.ENAME, E.EMPNO, IFNULL(CAST(M.EMPNO AS CHAR), 'NO MANAGER') AS MGR_NO,
    -> IFNULL(M.ENAME, 'NO MANAGER') AS MGR_NAME
    -> FROM EMPLOYEE_MASTER E
    -> LEFT JOIN EMPLOYEE_MASTER M ON E.MGR = M.EMPNO;
```

<pre>
Output:
+--------+-------+------------+------------+
| ENAME  | EMPNO | MGR_NO     | MGR_NAME   |
+--------+-------+------------+------------+
| SMITH  |  7369 | 7902       | FORD       |
| ALLEN  |  7499 | 7698       | BLAKE      |
| WARD   |  7521 | 7698       | BLAKE      |
| JONES  |  7566 | 7839       | KING       |
| MARTIN |  7654 | 7698       | BLAKE      |
| BLAKE  |  7698 | 7839       | KING       |
| CLARK  |  7782 | 7839       | KING       |
| SCOTT  |  7788 | 7566       | JONES      |
| KING   |  7839 | NO MANAGER | NO MANAGER |
| TURNER |  7844 | 7698       | BLAKE      |
| ADAMS  |  7876 | 7788       | SCOTT      |
| JAMES  |  7900 | 7698       | BLAKE      |
| FORD   |  7902 | 7566       | JONES      |
| MILLER |  7934 | 7782       | CLARK      |
+--------+-------+------------+------------+
14 rows in set (0.007 sec)
</pre>

### 9. Select dept name, dept no and sum of sal.

```sql
MariaDB [iilm]> SELECT D.DEPTNO, D.DNAME, SUM(E.SAL) AS TOTAL_SAL
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> GROUP BY D.DEPTNO;
```

<pre>
Output:
+--------+------------+-----------+
| DEPTNO | DNAME      | TOTAL_SAL |
+--------+------------+-----------+
|     10 | RESEARCH   |      1300 |
|     20 | ACCOUNTING |     15325 |
|     30 | SALES      |      9400 |
|     40 | OPERATIONS |      3000 |
+--------+------------+-----------+
4 rows in set (0.035 sec)
</pre>

### 10. Display employee number, name and location of the department in which he is working.

```sql
MariaDB [iilm]> SELECT E.EMPNO, E.ENAME, D.LOCATION
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```

<pre>
Output:
+-------+--------+-----------+
| EMPNO | ENAME  | LOCATION  |
+-------+--------+-----------+
|  7934 | MILLER | MUMBAI    |
|  7369 | SMITH  | CHENNAI   |
|  7566 | JONES  | CHENNAI   |
|  7782 | CLARK  | CHENNAI   |
|  7839 | KING   | CHENNAI   |
|  7876 | ADAMS  | CHENNAI   |
|  7902 | FORD   | CHENNAI   |
|  7499 | ALLEN  | HYDERABAD |
|  7521 | WARD   | HYDERABAD |
|  7654 | MARTIN | HYDERABAD |
|  7698 | BLAKE  | HYDERABAD |
|  7844 | TURNER | HYDERABAD |
|  7900 | JAMES  | HYDERABAD |
|  7788 | SCOTT  | DELHI     |
+-------+--------+-----------+
14 rows in set (0.001 sec)
</pre>

### 11. Display employee name and department name for each employee.

```sql
MariaDB [iilm]> SELECT E.ENAME, D.DNAME
    -> FROM EMPLOYEE_MASTER E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> ORDER BY D.DEPTNO;
```

<pre>
Output:
+--------+------------+
| ENAME  | DNAME      |
+--------+------------+
| MILLER | RESEARCH   |
| SMITH  | ACCOUNTING |
| JONES  | ACCOUNTING |
| CLARK  | ACCOUNTING |
| KING   | ACCOUNTING |
| ADAMS  | ACCOUNTING |
| FORD   | ACCOUNTING |
| ALLEN  | SALES      |
| WARD   | SALES      |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| TURNER | SALES      |
| JAMES  | SALES      |
| SCOTT  | OPERATIONS |
+--------+------------+
14 rows in set (0.001 sec)
</pre>
