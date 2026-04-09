# Exercise 05
**Date- 26-03-2026**

---

## 1. List all the Canadian cities and their populations 

```sql
SELECT City, Population FROM north_american_cities
WHERE Country = "Canada":
```

---

## 2. Order all the cities in the United States by their latitude from north to south

```sql
SELECT City FROM north_american_cities
WHERE Country = "United States"
ORDER BY LATITUDE desc;

```

---

## 3. List all the cities west of Chicago, ordered from west to east

```sql
SELECT city, longitude FROM north_american_cities
WHERE longitude < -87.629798
ORDER BY longitude ASC;
```

---

## 4. List the two largest cities in Mexico (by population)

```sql
SELECT city, population FROM north_american_cities
WHERE country = "Mexico"
ORDER BY population DESC
LIMIT 2;
```

---

## 5. List the third and fourth largest cities (by population) in the United States and their population

```sql
SELECT city, population FROM north_american_cities
WHERE country = "United States"
ORDER BY population DESC
LIMIT 2 OFFSET 2;
```

---
