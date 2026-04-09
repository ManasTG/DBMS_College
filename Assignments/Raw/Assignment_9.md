# Assingment 09
# 04-04-2026

## 1. Display the name of emp name who earns highest salary.
## 2.isplay the employee number and name of employee working as clerk and earning highest salary among clerks.
## 3. Display the names of the salesman who earns a salary more than the highest salary of any clerk.
## 4. Display the names of clerks who earn salary more than that of james of that of sal lesser than that of scott
## 5. Display the names of employees who earn a sal more than that of james or that of salary greater than that of scott.
## 6. Display the names of the employees who earn highest salary in their respective departments.
## 7. Display the names of employees who earn highest salaries in their respective job groups.
## 8. Display the employee names who are working in accounting dept.
## 9. Display the employee names who are working in mumbai.
## 10. Display the job groups having total salary greater than the maximum salary for managers.

---
# QUERIES

## 1. Display the name of emp name who earns highest salary.

MariaDB [manas_db]> SELECT ename FROM emp
    -> WHERE sal =(SELECT MAX(sal) FROM emp);
+-------+
| ename |
+-------+
| KING  |
+-------+
1 row in set (0.015 sec)



## 2. Display the employee number and name of employee working as clerk and earning highest salary among clerks.

MariaDB [manas_db]> SELECT ename, empno FROM emp WHERE job = 'CLERK' AND sal=(SELECT MAX(sal) FROM emp WHERE job = 'CLERK');
+--------+-------+
| ename  | empno |
+--------+-------+
| MILLER |  7934 |
+--------+-------+
1 row in set (0.001 sec)


## 3. Display the names of the salesman who earns a salary more than the highest salary of any clerk.

MariaDB [manas_db]> SELECT ename, empno FROM emp
    -> WHERE job = 'SALESMAN' AND sal > (SELECT MAX(sal) FROM emp WHERE job = 'CLERK');
+--------+-------+
| ename  | empno |
+--------+-------+
| ALLEN  |  7499 |
| TURNER |  7844 |
+--------+-------+
2 rows in set (0.001 sec)



## 4. Display the names of clerks who earn salary more than that of james of that of sal lesser than that of scott

MariaDB [manas_db]> SELECT ename FROM emp
    -> WHERE Job = 'CLERK'
    -> AND sal > (SELECT sal FROM emp WHERE ename = 'JAMES')
    -> AND sal < (SELECT sal FROM emp WHERE ename = 'SCOTT');
+--------+
| ename  |
+--------+
| ADAMS  |
| MILLER |
+--------+
2 rows in set (0.002 sec)


## 5. Display the names of employees who earn a sal more than that of james or that of salary greater than that of scott.

MariaDB [manas_db]> SELECT ename FROM emp
    -> WHERE sal > (SELECT sal FROM emp WHERE ename = 'JAMES')
    -> OR sal < (SELECT sal FROM emp WHERE ename = 'SCOTT'
    -> );
+--------+
| ename  |
+--------+
| SMITH  |
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
| JAMES  |
| FORD   |
| MILLER |
+--------+
14 rows in set (0.002 sec)



## 6. Display the names of the employees who earn highest salary in their respective departments.

MariaDB [manas_db]> SELECT ename, deptno FROM emp e
    -> WHERE sal = (SELECT MAX(sal) FROM emp e2
    -> WHERE e.deptno = e2.deptno);
+--------+--------+
| ename  | deptno |
+--------+--------+
| BLAKE  |     30 |
| SCOTT  |     40 |
| KING   |     20 |
| MILLER |     10 |
+--------+--------+
4 rows in set (0.004 sec)



## 7. Display the names of employees who earn highest salaries in their respective job groups.

MariaDB [manas_db]> SELECT ename, job FROM emp e
    -> WHERE sal = (SELECT MAX(SAL) FROM emp
    -> WHERE e.job = job);
+--------+-----------+
| ename  | job       |
+--------+-----------+
| ALLEN  | SALESMAN  |
| JONES  | MANAGER   |
| SCOTT  | ANALYST   |
| KING   | PRESIDENT |
| FORD   | ANALYST   |
| MILLER | CLERK     |
+--------+-----------+
6 rows in set (0.002 sec)



## 8. Display the employee names who are working in accounting dept.

MariaDB [manas_db]> SELECT ENAME FROM emp 
    -> WHERE deptno = (SELECT deptno FROM dept 
    -> WHERE dname = 'ACCOUNTING');
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
6 rows in set (0.003 sec)



## 9. Display the employee names who are working in mumbai.

MariaDB [manas_db]> SELECT ename
    -> FROM emp
    -> WHERE deptno IN (
    -> SELECT deptno
    -> FROM dept
    -> WHERE location = 'mumbai'
    -> );
+--------+
| ename  |
+--------+
| MILLER |
+--------+
1 row in set (0.002 sec)



## 10. Display the job groups having total salary greater than the maximum salary for managers.

MariaDB [manas_db]> SELECT job FROM emp
    -> GROUP BY Job
    -> HAVING SUM(sal) > (SELECT MAX(sal) FROM emp 
    -> WHERE job = 'MANAGER');
+-----------+
| job       |
+-----------+
| ANALYST   |
| CLERK     |
| MANAGER   |
| PRESIDENT |
| SALESMAN  |
+-----------+
5 rows in set (0.002 sec)



