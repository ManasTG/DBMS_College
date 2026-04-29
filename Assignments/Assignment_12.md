# Assingment 12
# 18-04-2026

## 1. Display those employees whose salary is less than his manager but more than salary of any other managers.
## 2. Find out the number of employees whose salary is greater than their manager salary?
## 3. Display those managers who are not working under president but they are working under any other manager?
## 4. Delete those department where no employee working?
## 5. Delete those records from emp table whose deptno not available in dept table?
## 6. Display those earners whose salary is out of the grade available in sal grade table?
## 7. Display employee name, sal, comm. And whose net pay is greater than any other in the company?
## 8. Display those employees who are working in sales or research?
## 9. Display the grade of jones?
## 10. Display the department name the no of characters of which is equal to no of employees in any other department?

---

# Queries

## 1. Display those employees whose salary is less than his manager but more than salary of any other managers.

-> SELECT e.ename, e.sal
-> FROM emp e
-> JOIN emp m ON e.mgr = m.empno
-> WHERE e.sal < m.sal
-> AND e.sal > ANY (
-> SELECT sal FROM emp WHERE job = 'MANAGER');
+-------+------+
| ename | sal  |
+-------+------+
| JONES | 2975 |
| BLAKE | 2850 |
+-------+------+

2 rows in set
Time: 0.065s


## 2. Find out the number of employees whose salary is greater than their manager salary?

-> SELECT COUNT(*)
-> FROM emp e
-> JOIN emp m ON e.mgr = m.empno
-> WHERE e.sal > m.sal;
+----------+
| COUNT(*) |
+----------+
| 2        |
+----------+

1 row in set
Time: 0.050s


## 3. Display those managers who are not working under president but they are working under any other manager?

-> SELECT e.ename
-> FROM emp e
-> JOIN emp m ON e.mgr = m.empno
-> WHERE e.job = 'MANAGER'
-> AND m.job <> 'PRESIDENT';
+-------+
| ename |
+-------+
+-------+

0 rows in set
Time: 0.011s


## 4. Delete those department where no employee working?

-> DELETE FROM dept
-> WHERE NOT EXISTS (
-> SELECT 1 FROM emp e WHERE e.deptno = dept.deptno);
You're about to run a destructive command.
Do you want to proceed? (y/n): y
Your call!
Query OK, 0 rows affected
Time: 0.005s



## 5. Delete those records from emp table whose deptno not available in dept table?

-> DELETE FROM emp_cp3
-> WHERE deptno NOT IN (
-> SELECT deptno FROM dept);
You're about to run a destructive command.
Do you want to proceed? (y/n): y
Your call!
Query OK, 0 rows affected
Time: 0.006s

## 6. Display those earners whose salary is out of the grade available in sal grade table?

-> SELECT e.ename, e.sal
-> FROM emp e
-> WHERE NOT EXISTS (
-> SELECT 1
-> FROM salgrade s
-> WHERE e.sal BETWEEN s.losal AND s.hisal);
+-------+-----+
| ename | sal |
+-------+-----+
+-------+-----+

0 rows in set
Time: 0.031s


## 7. Display employee name, sal, comm. And whose net pay is greater than any other in the company?

-> SELECT ename, sal, comm
-> FROM emp
-> WHERE (sal + NVL(comm,0)) >= ALL (
-> SELECT (sal + NVL(comm,0)) FROM emp);
+-------+------+--------+
| ename | sal  | comm   |
+-------+------+--------+
| KING  | 5000 | <null> |
+-------+------+--------+

1 row in set
Time: 0.020s


## 8. Display those employees who are working in sales or research?

-> SELECT e.ename
-> FROM emp e
-> JOIN dept d ON e.deptno = d.deptno
-> WHERE d.dname IN ('SALES', 'RESEARCH');
+--------+
| ename  |
+--------+
| MILLER |
| ALLEN  |
| WARD   |
| MARTIN |
| BLAKE  |
| TURNER |
| JAMES  |
+--------+

7 rows in set
Time: 0.023s


## 9. Display the grade of jones?

-> SELECT s.grade
-> FROM emp e
-> JOIN salgrade s
-> ON e.sal BETWEEN s.losal AND s.hisal
-> WHERE e.ename = 'JONES';
+-------+
| grade |
+-------+
| D     |
+-------+

1 row in set
Time: 0.028s


## 10. Display the department name the no of characters of which is equal to no of employees in any other department?

-> SELECT d.dname
-> FROM dept d
-> WHERE LENGTH(d.dname) IN (
-> SELECT COUNT(*) FROM emp GROUP BY deptno);
+-------+
| dname |
+-------+
+-------+

0 rows in set
Time: 0.035s

