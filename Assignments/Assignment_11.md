# Assingment 11
# 16-04-2026

## 1. Delete those employees who joined the company before 31- dec-82 while there dept location is ‘Delhi or ‘Mumbai’.
## 2. Display employee name, job, deptname, location for all who are working as managers.
## 3. Display name and salary of ford if his sal is equal to high sal of his grade.
## 4. Find out the top 5 earner of company.
## 5. Display the name of those employees who are getting highest salary.
## 6. Display those employees whose salary is equal to average of maximum and minimum.
## 7. Display dname where at least 3 are working and display only dname
## 8. Display name of those managers names whose salary is more than average salary of company.
## 9. Display those managers name whose salary is more than an average salary of his employees.
## 10. Display employee name, sal, comm and net pay for those employees whose net pay are greater than or equal to any other employee salary of the company?
---

# Table Update 
```sql
CREATE TABLE emp_cp3 AS SELECT * FROM emp;
```
Query OK, 14 rows affected
Time: 0.038s
```sql
SELECT* FROM emp_cp3;
```
```
+-------+--------+-----------+--------+------------+------+--------+--------+
| empno | ename  | job       | mgr    | hiredate   | sal  | comm   | deptno |
+-------+--------+-----------+--------+------------+------+--------+--------+
| 7369  | SMITH  | CLERK     | 7902   | 1980-12-17 | 800  | <null> | 20     |
| 7499  | ALLEN  | SALESMAN  | 7698   | 1981-02-20 | 1600 | 300    | 30     |
| 7521  | WARD   | SALESMAN  | 7698   | 1981-02-22 | 1250 | 300    | 30     |
| 7566  | JONES  | MANAGER   | 7839   | 1981-04-02 | 2975 | <null> | 20     |
| 7654  | MARTIN | SALESMAN  | 7698   | 1981-09-28 | 1250 | 1400   | 30     |
| 7698  | BLAKE  | MANAGER   | 7839   | 1981-05-01 | 2850 | <null> | 30     |
| 7782  | CLARK  | MANAGER   | 7839   | 1981-06-09 | 2450 | <null> | 20     |
| 7788  | SCOTT  | ANALYST   | 7566   | 1982-12-09 | 3000 | <null> | 40     |
| 7839  | KING   | PRESIDENT | <null> | 1981-11-17 | 5000 | <null> | 20     |
| 7844  | TURNER | SALESMAN  | 7698   | 1981-09-08 | 1500 | 0      | 30     |
| 7876  | ADAMS  | CLERK     | 7788   | 1983-01-12 | 1100 | <null> | 20     |
| 7900  | JAMES  | CLERK     | 7698   | 1981-12-03 | 950  | <null> | 30     |
| 7902  | FORD   | ANALYST   | 7566   | 1981-12-03 | 3000 | <null> | 20     |
| 7934  | MILLER | CLERK     | 7782   | 1982-01-23 | 1300 | <null> | 10     |
+-------+--------+-----------+--------+------------+------+--------+--------+
14 rows in set
Time: 0.023s
```

---
# Queries

## 1. Delete those employees who joined the company before 31- dec-82 while there dept location is ‘Delhi’ or ‘Mumbai’. {in emp_cp3}
```sql
DELETE FROM emp_cp3 
WHERE hiredate < "1982-12-31"
AND deptno IN (SELECT deptno FROM dept WHERE location IN 
("DELHI" , "MUMBAI")); 
```
```
You're about to run a destructive command.
Do you want to proceed? (y/n): y
Your call!
Query OK, 2 rows affected
Time: 0.009s
```

```sql
SELECT * FROM emp_cp3;
```
```
+-------+--------+-----------+--------+------------+------+--------+--------+
| empno | ename  | job       | mgr    | hiredate   | sal  | comm   | deptno |
+-------+--------+-----------+--------+------------+------+--------+--------+
| 7369  | SMITH  | CLERK     | 7902   | 1980-12-17 | 800  | <null> | 20     |
| 7499  | ALLEN  | SALESMAN  | 7698   | 1981-02-20 | 1600 | 300    | 30     |
| 7521  | WARD   | SALESMAN  | 7698   | 1981-02-22 | 1250 | 300    | 30     |
| 7566  | JONES  | MANAGER   | 7839   | 1981-04-02 | 2975 | <null> | 20     |
| 7654  | MARTIN | SALESMAN  | 7698   | 1981-09-28 | 1250 | 1400   | 30     |
| 7698  | BLAKE  | MANAGER   | 7839   | 1981-05-01 | 2850 | <null> | 30     |
| 7782  | CLARK  | MANAGER   | 7839   | 1981-06-09 | 2450 | <null> | 20     |
| 7839  | KING   | PRESIDENT | <null> | 1981-11-17 | 5000 | <null> | 20     |
| 7844  | TURNER | SALESMAN  | 7698   | 1981-09-08 | 1500 | 0      | 30     |
| 7876  | ADAMS  | CLERK     | 7788   | 1983-01-12 | 1100 | <null> | 20     |
| 7900  | JAMES  | CLERK     | 7698   | 1981-12-03 | 950  | <null> | 30     |
| 7902  | FORD   | ANALYST   | 7566   | 1981-12-03 | 3000 | <null> | 20     |
+-------+--------+-----------+--------+------------+------+--------+--------+
12 rows in set
Time: 0.020s
(1065, 'Query was empty')
```
---

## 2. Display employee name, job, deptname, location for all who are working as managers.
```sql
SELECT e.ename, e.job, d.dname, d.location
FROM emp e
JOIN dept d ON e.deptno = d.deptno
WHERE e.job = 'MANAGER';
```
```
+-------+---------+------------+-----------+
| ename | job     | dname      | location  |
+-------+---------+------------+-----------+
| JONES | MANAGER | ACCOUNTING | Chennai   |
| CLARK | MANAGER | ACCOUNTING | Chennai   |
| BLAKE | MANAGER | SALES      | Hyderabad |
+-------+---------+------------+-----------+
3 rows in set
Time: 0.048s
```
---

## 3. Display name and salary of ford if his sal is equal to high sal of his grade.
```sql
SELECT e.ename, e.job
FROM emp e
JOIN salgrade s ON e.sal BETWEEN s.losal AND s.hisal
WHERE e.ename = 'FORD'
and SAL = (SELECT MAX(e2.sal)
FROM emp e2
JOIN salgrade s2 ON e2.sal BETWEEN s2.losal AND s2.hisal
WHERE s2.grade = s.grade);
```
```
+-------+---------+
| ename | job     |
+-------+---------+
| FORD  | ANALYST |
+-------+---------+
1 row in set
Time: 0.006s
```
---

## 4. Find out the top 5 earner of company.
```sql
SELECT ename, sal 
FROM emp
ORDER BY sal DESC
LIMIT 5;
```
```
+-------+------+
| ename | sal  |
+-------+------+
| KING  | 5000 |
| FORD  | 3000 |
| SCOTT | 3000 |
| JONES | 2975 |
| BLAKE | 2850 |
+-------+------+
5 rows in set
Time: 0.041s
```
---

## 5. Display the name of those employee who is getting the highest salary.
```sql
SELECT ename,
MAX(sal) AS max_sal 
FROM emp;
```
```
+-------+---------+
| ename | max_sal |
+-------+---------+
| SMITH | 5000    |
+-------+---------+
1 row in set
Time: 0.021s
```
---

## 6. Display those employees whose salary is equal to average of maximum and minimum.
```sql
SELECT ename, sal
FROM emp
WHERE sal=(
SELECT (MAX(sal) + MIN(sal))/2
FROM emp);
```
```
+-------+-----+
| ename | sal |
+-------+-----+
+-------+-----+
0 rows in set
Time: 0.022s
```
---

## 7. Display dname where at least 3 are working and display only dname
```sql
SELECT d.dname
FROM dept d
JOIN emp e
ON d.deptno = e.deptno
GROUP BY d.dname
HAVING  COUNT(e.deptno) >2; 
```
```
+------------+
| dname      |
+------------+
| ACCOUNTING |
| SALES      |
+------------+
2 rows in set
Time: 0.018s
```
---

## 8. Display name of those managers names whose salary is more than average salary of company.
```sql
SELECT ename 
FROM emp 
WHERE job = 'MANAGER' 
AND sal > (SELECT AVG(sal)
FROM emp);
```
```
+-------+
| ename |
+-------+
| JONES |
| BLAKE |
| CLARK |
+-------+
3 rows in set
Time: 0.004s
```
---

## 9. Display those managers name whose salary is more than an average salary of his employees.(IMP)
```sql
SELECT ename 
FROM emp m
WHERE job = 'MANAGER' 
AND sal > (SELECT AVG(sal)
FROM emp e
WHERE  e.mgr = m.empno);
```
```
+-------+
| ename |
+-------+
| BLAKE |
| CLARK |
+-------+
2 rows in set
Time: 0.007s
```
---

## 10. Display employee name, sal, comm and net pay for those employees whose net pay are greater than or equal to any other employee salary of the company?
```sql
SELECT ename, sal, comm, (sal + comm) AS net_pay
FROM emp
WHERE (sal + comm) >= ANY (SELECT sal FROM emp);
```
```
+--------+------+------+---------+
| ename  | sal  | comm | net_pay |
+--------+------+------+---------+
| ALLEN  | 1600 | 300  | 1900    |
| WARD   | 1250 | 300  | 1550    |
| MARTIN | 1250 | 1400 | 2650    |
| TURNER | 1500 | 0    | 1500    |
+--------+------+------+---------+
4 rows in set
```
---
