# Assingment 09
**Date- 04-04-2026**

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
```sql
SELECT ename FROM emp
WHERE sal =(SELECT MAX(sal) FROM emp);
```
```
+-------+
| ename |
+-------+
| KING  |
+-------+
```
---



## 2. Display the employee number and name of employee working as clerk and earning highest salary among clerks.
```sql
SELECT ename, empno FROM emp WHERE job = 'CLERK' AND sal=(SELECT MAX(sal) FROM emp WHERE job = 'CLERK');
```

```
+--------+-------+
| ename  | empno |
+--------+-------+
| MILLER |  7934 |
+--------+-------+
```
---

## 3. Display the names of the salesman who earns a salary more than the highest salary of any clerk.
```sql
SELECT ename, empno FROM emp
WHERE job = 'SALESMAN' AND sal > (SELECT MAX(sal) FROM emp WHERE job = 'CLERK');
```

```
+--------+-------+
| ename  | empno |
+--------+-------+
| ALLEN  |  7499 |
| TURNER |  7844 |
+--------+-------+
```
---



## 4. Display the names of clerks who earn salary more than that of james of that of sal lesser than that of scott
```sql
SELECT ename FROM emp
WHERE Job = 'CLERK'
AND sal > (SELECT sal FROM emp WHERE ename = 'JAMES')
AND sal < (SELECT sal FROM emp WHERE ename = 'SCOTT');
```

```
+--------+
| ename  |
+--------+
| ADAMS  |
| MILLER |
+--------+
```
---


## 5. Display the names of employees who earn a sal more than that of james or that of salary greater than that of scott.
```sql
SELECT ename FROM emp
WHERE sal > (SELECT sal FROM emp WHERE ename = 'JAMES')
OR sal < (SELECT sal FROM emp WHERE ename = 'SCOTT');
```

```
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
```
---


## 6. Display the names of the employees who earn highest salary in their respective departments.
```sql
SELECT ename, deptno FROM emp e
WHERE sal = (SELECT MAX(sal) FROM emp e2
WHERE e.deptno = e2.deptno);
```

```
+--------+--------+
| ename  | deptno |
+--------+--------+
| BLAKE  |     30 |
| SCOTT  |     40 |
| KING   |     20 |
| MILLER |     10 |
+--------+--------+
```
---



## 7. Display the names of employees who earn highest salaries in their respective job groups.
```sql
SELECT ename, job FROM emp e
WHERE sal = (SELECT MAX(SAL) FROM emp
WHERE e.job = job);
```

```
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
```
---



## 8. Display the employee names who are working in accounting dept.
```sql
SELECT ENAME FROM emp 
WHERE deptno = (SELECT deptno FROM dept 
WHERE dname = 'ACCOUNTING');
```

```
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
```
---



## 9. Display the employee names who are working in mumbai.
```sql
SELECT ename
FROM emp
WHERE deptno IN (
SELECT deptno
FROM dept
WHERE location = 'mumbai');
```

```
+--------+
| ename  |
+--------+
| MILLER |
+--------+
```
---



## 10. Display the job groups having total salary greater than the maximum salary for managers.
```sql
SELECT job FROM emp
GROUP BY Job
HAVING SUM(sal) > (SELECT MAX(sal) FROM emp 
WHERE job = 'MANAGER');
```

```
+-----------+
| job       |
+-----------+
| ANALYST   |
| CLERK     |
| MANAGER   |
| PRESIDENT |
| SALESMAN  |
+-----------+
```
---



