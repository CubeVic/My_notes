# Random notes about SQL ( mostly MySQL)

## How to get different (unique) results 

```SQL
SELECT DISTINCT column-name
  FROM table-name
```

## How to count different (unique) results 

```SQL
SELECT COUNT (DISTINCT column-name)
  FROM table-name
```

## How to display different (unique) in alphabetical order

```SQL
SELECT DISTINCT Country
  FROM Supplier
ORDER BY COUNTRY
```

## How to find the difference between unique values and all values

```SQL
SELECT (COUNT(CITY) - COUNT(DISTINCT CITY)) FROM STATION;
```



[some reference](https://www.dofactory.com/sql/select-distinct)