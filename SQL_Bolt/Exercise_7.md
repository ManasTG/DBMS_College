# Exercise 06
**Date- 08-04-2026**

---

## 1. Find the domestic and international sales for each movie 

```sql
SELECT m.Title, b.Domestic_sales, b.International_sales
FROM Movies m
JOIN Boxoffice b ON m.id = b.Movie_id; 
```

---

## 2. Show the sales numbers for each movie that did better internationally rather than domestically

```sql
SELECT m.Title, b.International_sales
FROM Movies m
JOIN Boxoffice b ON m.id = b.Movie_id
WHERE International_sales > Domestic_sales;
```
---

## 3. List all the movies by their ratings in descending order

```sql
SELECT m.Title, b.Rating FROM Movies m
JOIN Boxoffice b ON m.id = b.Movie_id
ORDER BY Rating DESC
```

---
