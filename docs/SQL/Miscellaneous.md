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

## How to find the length of a string 

In this case let say that we want to print the size or length of a string

```SQL
SELECT CITY, LENGTH(CITY) FROM STATION ORDER BY LENGTH(CITY)
```

## `LEFT()` and `RIGHT()` functions useful to make substrigns 

The `LEFT()` function extracts a number of characters from a string (starting from left.

**Syntax**
```SQL
LEFT(string, number_of_chars)
```

**Example:**
Extract 5 characters from the text in the *"CustomerName"* column (starting from left):

```SQL
SELECT LEFT(CustomerName, 5) AS ExtractString
FROM Customers;
```

now, The `RIGHT()`function extracts a number of characters from a string (starting from right).

**Syntax**
```SQL
RIGHT(string, number_of_chars)
```
**Example**
Extract 5 characters from the text in the "CustomerName" column (starting from right):

```SQL
SELECT RIGHT(CustomerName, 5) AS ExtractString
FROM Customers;
```

[some reference](https://www.dofactory.com/sql/select-distinct)