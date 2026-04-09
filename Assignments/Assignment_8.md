# Assingment 07
**Date- 02-04-2026**

## 1. Display all employees with their dept name.
## 2. Display those employees whose manager names is jones, and also display their manager name.
## 3. Display employee name, his job, his dept name, his manager name, his grade and make out of an under department wise.
## 4. List out all the employees name, job, and salary grade and department name for everyone in the company except ‘clerk’. Sort on salary display the highest salary.
## 5. Display employee name, his job and his manager. Display also employees who are without manager.
## 6. List the employee name, job, annual salary, deptno, dept name and grade who earn 36000 a year or who are not clerks.
## 7. List ename, job, annual sal, deptno, dname and grade who earn 30000 per year and who are not clerks.
## 8. List out all employees by name and number along with their manager’s name and number also display ‘no manager’ who has no manager.
## 9. Select dept name, dept no and sum of sal
## 10. Display employee number, name and location of the department in which he is working
## 11. Display employee name and department name for each employee.

---
### Update Table

### Add location column in the dept table
```sql
ALTER TABLE dept ADD location char(50);
```

```sql
SELECT * FROM dept;
```

```
+--------+------------+----------+
| deptno | dname      | location |
+--------+------------+----------+
|     10 | RESEARCH   | NULL     |
|     20 | ACCOUNTING | NULL     |
|     30 | SALES      | NULL     |
|     40 | OPERATIONS | NULL     |
+--------+------------+----------+
```
---

### Add cities name in the location column of dept table

```sql
UPDATE dept
SET location = 'Mumbai' WHERE deptno = 10;
```

```sql
UPDATE dept SET location = 'Chennai' WHERE deptno = 20;
```

```sql
UPDATE dept SET location = 'Hyderabad' WHERE deptno = 30;
```

```sql
UPDATE dept SET location = 'Delhi' WHERE deptno = 40;
```

```sql
SELECT * FROM dept;
```

```
+--------+------------+-----------+
| deptno | dname      | location  |
+--------+------------+-----------+
|     10 | RESEARCH   | Mumbai    |
|     20 | ACCOUNTING | Chennai   |
|     30 | SALES      | Hyderabad |
|     40 | OPERATIONS | Delhi     |
+--------+------------+-----------+
```
---
## Create and add input in the new table of salgrade

```sql
CREATE TABLE salgrade
(grade VAR(1)),
(losal INT),
(Hisal INST);
```


```sql
Insert INTO salgrade VALUES
('A', 700, 1200),
('B', 1201, 1400),
('C', 1401, 2000),
('D', 2001, 3000),
('E', 3001, 9999);

SELECT * FROM salgrade;
```


```
+-------+-------+-------+
| grade | losal | hisal |
+-------+-------+-------+
| A     |   700 |  1200 |
| B     |  1201 |  1400 |
| C     |  1401 |  2000 |
| D     |  2001 |  3000 |
| E     |  3001 |  9999 |
+-------+-------+-------+
```




---
### table

## department table
```
+--------+------------+-----------+
| deptno | dname      | location  |
+--------+------------+-----------+
|     10 | RESEARCH   | Mumbai    |
|     20 | ACCOUNTING | Chennai   |
|     30 | SALES      | Hyderabad |
|     40 | OPERATIONS | Delhi     |
+--------+------------+-----------+
```
---

## employee table
```
+-------+--------+-----------+------+------------+------+------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal  | comm | deptno |
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
```
---

## salgrade table
```
+-------+-------+-------+
| grade | losal | hisal |
+-------+-------+-------+
| A     |   700 |  1200 |
| B     |  1201 |  1400 |
| C     |  1401 |  2000 |
| D     |  2001 |  3000 |
| E     |  3001 |  9999 |
+-------+-------+-------+
5 rows in set (0.002 sec)
```
---

# Queries

## 1. Display all employees with their dept name.
```sql
SELECT e.ename, d.dname
FROM emp e
JOIN dept d
ON e.deptno = d.deptno;
```

```
+--------+------------+
| ename  | dname      |
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
```
---



## 2. Display those employees whose manager names is jones, and also display their manager name.
```sql
SELECT e.ename AS emp, m.ename AS manager
FROM  emp e
JOIN emp m
ON e.mgr = m.empno
WHERE m.ename = 'JONES';
```

```
+-------+---------+
| emp   | manager |
+-------+---------+
| SCOTT | JONES   |
| FORD  | JONES   |
+-------+---------+
```
---



## 3. Display employee name, his job, his dept name, his manager name, his grade and make out of an under department wise.
```sql
SELECT e.ename, e.job, d.dname, m.ename AS manager_name, s.grade
FROM emp e
JOIN dept d ON e.deptno = d.deptno
LEFT JOIN emp m ON e.mgr = m.empno
JOIN salgrade s ON e.sal BETWEEN s.losal AND s.hisal
ORDER BY d.dname;
```

```
+--------+-----------+------------+--------------+-------+
| ename  | job       | dname      | manager_name | grade |
+--------+-----------+------------+--------------+-------+
| JONES  | MANAGER   | ACCOUNTING | KING         | D     |
| KING   | PRESIDENT | ACCOUNTING | NULL         | E     |
| CLARK  | MANAGER   | ACCOUNTING | KING         | D     |
| SMITH  | CLERK     | ACCOUNTING | FORD         | A     |
| FORD   | ANALYST   | ACCOUNTING | JONES        | D     |
| ADAMS  | CLERK     | ACCOUNTING | SCOTT        | A     |
| SCOTT  | ANALYST   | OPERATIONS | JONES        | D     |
| MILLER | CLERK     | RESEARCH   | CLARK        | B     |
| WARD   | SALESMAN  | SALES      | BLAKE        | B     |
| MARTIN | SALESMAN  | SALES      | BLAKE        | B     |
| ALLEN  | SALESMAN  | SALES      | BLAKE        | C     |
| BLAKE  | MANAGER   | SALES      | KING         | D     |
| JAMES  | CLERK     | SALES      | BLAKE        | A     |
| TURNER | SALESMAN  | SALES      | BLAKE        | C     |
+--------+-----------+------------+--------------+-------+
```
---


## 4. List out all the employees name, job, and salary grade and department name for everyone in the company except ‘clerk’. Sort on salary display the highest salary.

```sql
SELECT e.ename, e.job, s.grade, d.dname, e.sal
FROM emp e
JOIN dept d ON e.deptno = d.deptno
JOIN salgrade s ON e.sal BETWEEN s.losal AND s.hisal
WHERE e.job <> 'CLERK'
ORDER BY e.sal DESC;
```

```
+--------+-----------+-------+------------+------+
| ename  | job       | grade | dname      | sal  |
+--------+-----------+-------+------------+------+
| KING   | PRESIDENT | E     | ACCOUNTING | 5000 |
| SCOTT  | ANALYST   | D     | OPERATIONS | 3000 |
| FORD   | ANALYST   | D     | ACCOUNTING | 3000 |
| JONES  | MANAGER   | D     | ACCOUNTING | 2975 |
| BLAKE  | MANAGER   | D     | SALES      | 2850 |
| CLARK  | MANAGER   | D     | ACCOUNTING | 2450 |
| ALLEN  | SALESMAN  | C     | SALES      | 1600 |
| TURNER | SALESMAN  | C     | SALES      | 1500 |
| MARTIN | SALESMAN  | B     | SALES      | 1250 |
| WARD   | SALESMAN  | B     | SALES      | 1250 |
+--------+-----------+-------+------------+------+
```
---


## 5. Display employee name, his job and his manager. Display also employees who are without manager.
```sql
SELECT e.ename, e.job, m.ename AS manager
FROM emp e
LEFT JOIN emp m ON e.mgr = m.empno;
```

```
+--------+-----------+---------+
| ename  | job       | manager |
+--------+-----------+---------+
| SMITH  | CLERK     | FORD    |
| ALLEN  | SALESMAN  | BLAKE   |
| WARD   | SALESMAN  | BLAKE   |
| JONES  | MANAGER   | KING    |
| MARTIN | SALESMAN  | BLAKE   |
| BLAKE  | MANAGER   | KING    |
| CLARK  | MANAGER   | KING    |
| SCOTT  | ANALYST   | JONES   |
| KING   | PRESIDENT | NULL    |
| TURNER | SALESMAN  | BLAKE   |
| ADAMS  | CLERK     | SCOTT   |
| JAMES  | CLERK     | BLAKE   |
| FORD   | ANALYST   | JONES   |
| MILLER | CLERK     | CLARK   |
+--------+-----------+---------+
```
---


## 6. List the employee name, job, annual salary, deptno, dept name and grade who earn 36000 a year or who are not clerks.
```sql
SELECT e.ename, e.job, e.sal*12 AS annual_salary,
e.deptno, d.dname, s.grade
FROM emp e
JOIN dept d ON e.deptno = d.deptno
JOIN salgrade s ON e.sal BETWEEN s.losal AND s.hisal
WHERE e.sal*12 >= 36000 OR e.job <> 'CLERK';
```

```
+--------+-----------+---------------+--------+------------+-------+
| ename  | job       | annual_salary | deptno | dname      | grade |
+--------+-----------+---------------+--------+------------+-------+
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
```
---


## 7. List ename, job, annual sal, deptno, dname and grade who earn 30000 per year and who are not clerks.

```sql
SELECT e.ename, e.job, e.sal*12 AS annual_salary,
e.deptno, d.dname, s.grade
FROM emp e
JOIN dept d ON e.deptno = d.deptno
JOIN salgrade s ON e.sal BETWEEN s.losal AND s.hisal
WHERE e.sal*12 >= 30000
AND e.job <> 'CLERK';
```

```
+-------+-----------+---------------+--------+------------+-------+
| ename | job       | annual_salary | deptno | dname      | grade |
+-------+-----------+---------------+--------+------------+-------+
| JONES | MANAGER   |         35700 |     20 | ACCOUNTING | D     |
| FORD  | ANALYST   |         36000 |     20 | ACCOUNTING | D     |
| BLAKE | MANAGER   |         34200 |     30 | SALES      | D     |
| SCOTT | ANALYST   |         36000 |     40 | OPERATIONS | D     |
| KING  | PRESIDENT |         60000 |     20 | ACCOUNTING | E     |
+-------+-----------+---------------+--------+------------+-------+
```
---


## 8. List out all employees by name and number along with their manager’s name and number also display ‘no manager’ who has no manager.
```sql
SELECT e.ename, e.empno,
FNULL(m.ename, 'No Manager') AS manager_name,
m.empno AS manager_no
FROM emp e
LEFT JOIN emp m ON e.mgr = m.empno;
```

```
+--------+-------+--------------+------------+
| ename  | empno | manager_name | manager_no |
+--------+-------+--------------+------------+
| SMITH  |  7369 | FORD         |       7902 |
| ALLEN  |  7499 | BLAKE        |       7698 |
| WARD   |  7521 | BLAKE        |       7698 |
| JONES  |  7566 | KING         |       7839 |
| MARTIN |  7654 | BLAKE        |       7698 |
| BLAKE  |  7698 | KING         |       7839 |
| CLARK  |  7782 | KING         |       7839 |
| SCOTT  |  7788 | JONES        |       7566 |
| KING   |  7839 | No Manager   |       NULL |
| TURNER |  7844 | BLAKE        |       7698 |
| ADAMS  |  7876 | SCOTT        |       7788 |
| JAMES  |  7900 | BLAKE        |       7698 |
| FORD   |  7902 | JONES        |       7566 |
| MILLER |  7934 | CLARK        |       7782 |
+--------+-------+--------------+------------+
```
---



## 9. Select dept name, dept no and sum of sal
```sql
SELECT d.dname, d.deptno, SUM(e.sal) AS total_salary
FROM emp e
JOIN dept d ON e.deptno = d.deptno
GROUP BY d.deptno, d.dname;
```

```
+------------+--------+--------------+
| dname      | deptno | total_salary |
+------------+--------+--------------+
| RESEARCH   |     10 |         1300 |
| ACCOUNTING |     20 |        15325 |
| SALES      |     30 |         9400 |
| OPERATIONS |     40 |         3000 |
+------------+--------+--------------+
```
---


## 10. Display employee number, name and location of the department in which he is working
```sql
SELECT e.empno, e.ename, d.location
FROM emp e
JOIN dept d ON e.deptno = d.deptno;
```

```
+-------+--------+-----------+
| empno | ename  | location  |
+-------+--------+-----------+
|  7934 | MILLER | Mumbai    |
|  7369 | SMITH  | Chennai   |
|  7566 | JONES  | Chennai   |
|  7782 | CLARK  | Chennai   |
|  7839 | KING   | Chennai   |
|  7876 | ADAMS  | Chennai   |
|  7902 | FORD   | Chennai   |
|  7499 | ALLEN  | Hyderabad |
|  7521 | WARD   | Hyderabad |
|  7654 | MARTIN | Hyderabad |
|  7698 | BLAKE  | Hyderabad |
|  7844 | TURNER | Hyderabad |
|  7900 | JAMES  | Hyderabad |
|  7788 | SCOTT  | Delhi     |
+-------+--------+-----------+
```
---


## 11. Display employee name and department name for each employee.
```sql
SELECT e.ename, d.dname
FROM emp e
JOIN dept d ON e.deptno = d.deptno;
```

```
+--------+------------+
| ename  | dname      |
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
```
---
