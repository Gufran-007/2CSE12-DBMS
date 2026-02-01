# PRACTICAL FILE ASSIGNMENT - 01

## DATE : 28/01/26

### 1. Create Employee_master table with data using Employee table.

```sql
MariaDB [iilm]> CREATE TABLE Employee_master(
    -> EMPNO INT PRIMARY KEY,
    -> ENAME VARCHAR(20) NOT NULL,
    -> JOB VARCHAR(20),
    -> MGR INT,
    -> HIREDATE DATE,
    -> SAL INT(10),
    -> COMM INT(7),
    -> DEPTNO INT(2),
    -> FOREIGN KEY(DEPTNO) REFERENCES Department(DEPTNO));
Query OK, 0 rows affected (0.084 sec)
```

```sql
MariaDB [iilm]> DESC Employee_master;
```

<pre >
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| EMPNO    | int(11)     | NO   | PRI | NULL    |       |
| ENAME    | varchar(20) | NO   |     | NULL    |       |
| JOB      | varchar(20) | YES  |     | NULL    |       |
| MGR      | int(11)     | YES  |     | NULL    |       |
| HIREDATE | date        | YES  |     | NULL    |       |
| SAL      | int(10)     | YES  |     | NULL    |       |
| COMM     | int(7)      | YES  |     | NULL    |       |
| DEPTNO   | int(2)      | YES  | MUL | NULL    |       |
+----------+-------------+------+-----+---------+-------+
8 rows in set (0.065 sec)
</pre>

```sql
MariaDB [iilm]> DESC Department;
```

<pre>
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| DEPTNO | int(2)      | NO   | PRI | NULL    |       |
| DNAME  | varchar(15) | NO   |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
2 rows in set (0.064 sec)
</pre>

```sql
MariaDB [iilm]> INSERT INTO Department (DEPTNO, DNAME) VALUES
    -> (10, 'RESEARCH'),
    -> (20, 'ACCOUNTING'),
    -> (30, 'SALES'),
    -> (40, 'OPERATIONS');
Query OK, 4 rows affected (0.016 sec)
Records: 4  Duplicates: 0  Warnings: 0
```

```sql
MariaDB [iilm]> SELECT *FROM Department;
```

<pre>
+--------+------------+
| DEPTNO | DNAME      |
+--------+------------+
|     10 | RESEARCH   |
|     20 | ACCOUNTING |
|     30 | SALES      |
|     40 | OPERATIONS |
+--------+------------+
4 rows in set (0.001 sec)
</pre>

```sql
MariaDB [iilm]> INSERT INTO Employee_master
    -> (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
    -> VALUES
    -> (7369, 'SMITH', 'CLERK', 7902, '1980-12-17', 800, NULL, 20),
    -> (7499, 'ALLEN', 'SALESMAN', 7698, '1981-02-20', 1600, 300, 30),
    -> (7521, 'WARD', 'SALESMAN', 7698, '1981-02-22', 1250, 300, 30),
    -> (7566, 'JONES', 'MANAGER', 7839, '1981-04-02', 2975, NULL, 20),
    -> (7654, 'MARTIN', 'SALESMAN', 7698, '1981-09-28', 1250, 1400, 30),
    -> (7698, 'BLAKE', 'MANAGER', 7839, '1981-05-01', 2850, NULL, 30),
    -> (7782, 'CLARK', 'MANAGER', 7839, '1981-06-09', 2450, NULL, 20),
    -> (7788, 'SCOTT', 'ANALYST', 7566, '1982-12-09', 3000, NULL, 40),
    -> (7839, 'KING', 'PRESIDENT', NULL, '1981-11-17', 5000, NULL, 20),
    -> (7844, 'TURNER', 'SALESMAN', 7698, '1981-09-08', 1500, 0, 30),
    -> (7876, 'ADAMS', 'CLERK', 7788, '1983-01-12', 1100, NULL, 20),
    -> (7900, 'JAMES', 'CLERK', 7698, '1981-12-03', 950, NULL, 30),
    -> (7902, 'FORD', 'ANALYST', 7566, '1981-12-03', 3000, NULL, 20),
    -> (7934, 'MILLER', 'CLERK', 7782, '1982-01-23', 1300, NULL, 10);
Query OK, 14 rows affected (0.037 sec)
Records: 14  Duplicates: 0  Warnings: 0
```

```sql
MariaDB [iilm]> SELECT *FROM Employee_master;
```

<pre>
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
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000 | NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300 | NULL |     10 |
+-------+--------+-----------+------+------------+------+------+--------+
14 rows in set (0.001 sec)
</pre>

### 2. Delete all record from Employee_master where DEPTNO is 10.

```sql
MariaDB [iilm]> DELETE FROM Employee_master WHERE DEPTNO=10;
Query OK, 1 row affected (0.035 sec)

MariaDB [iilm]> SELECT *FROM Employee_master;
```

<pre>
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
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000 | NULL |     20 |
+-------+--------+-----------+------+------------+------+------+--------+
13 rows in set (0.001 sec)
</pre>

### 3. Update 10% in SAL where DEPTNO is 20 from Employee_master.

```sql
MariaDB [iilm]> UPDATE Employee_master
    -> SET SAL=SAL*1.10
    -> WHERE DEPTNO=20;
Query OK, 6 rows affected (0.037 sec)
Rows matched: 6  Changed: 6  Warnings: 0

MariaDB [iilm]> SELECT *FROM Employee_master;
```

<pre>
+-------+--------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+-----------+------+------------+------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  880 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 3273 | NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2695 | NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5500 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1210 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3300 | NULL |     20 |
+-------+--------+-----------+------+------------+------+------+--------+
13 rows in set (0.001 sec)
</pre>

### 4. Alter SAL with size (10,2) in Employee_master.

---

```sql
MariaDB [iilm]> ALTER TABLE Employee_master
    -> MODIFY SAL FLOAT(10,2);
Query OK, 13 rows affected (0.110 sec)
Records: 13  Duplicates: 0  Warnings: 0

MariaDB [iilm]> SELECT *FROM Employee_master;
```

<pre>
+-------+--------+-----------+------+------------+---------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+--------+-----------+------+------------+---------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  880.00 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  300 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 3273.00 | NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2695.00 | NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000.00 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5500.00 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1210.00 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3300.00 | NULL |     20 |
+-------+--------+-----------+------+------------+---------+------+--------+
13 rows in set (0.003 sec)
</pre>

### 5. Drop Employee_master Table.

---

```sql
MariaDB [iilm]> DROP TABLE Employee_master;
Query OK, 0 rows affected (0.050 sec)
```

<pre>
MariaDB [iilm]> show tables;
+-----------------+
| Tables_in_iilm  |
+-----------------+
| department      |
| employee_master |
+-----------------+
2 rows in set (0.001 sec)

MariaDB [iilm]> SHOW TABLES;
+----------------+
| Tables_in_iilm |
+----------------+
| department     |
+----------------+
1 row in set (0.002 sec)
</pre>
