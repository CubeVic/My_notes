## How to find the length of a string 

In this case, let say that we want to print the size or length of a string.

```SQL
SELECT CITY, LENGTH(CITY) FROM STATION ORDER BY LENGTH(CITY)
```

## `LEFT()` and `RIGHT()` functions useful to make substrigns 

The `LEFT()` function extracts a number of characters from a string (starting from left.

### **Syntax LEFT()**
```SQL
LEFT(string, number_of_chars)
```

**Example:**
Extract 5 characters from the text in the *"CustomerName"* column (starting from left):

```SQL
SELECT LEFT(CustomerName, 5) AS ExtractString
FROM Customers;
```

now, The `RIGHT()` function extracts a number of characters from a string (starting from right).

### **Syntax RIGHT()**
```SQL
RIGHT(string, number_of_chars)
```
**Example**
Extract 5 characters from the text in the "CustomerName" column (starting from right):

```SQL
SELECT RIGHT(CustomerName, 5) AS ExtractString
FROM Customers;
```

## `CONCAT()` function

The CONCAT() function adds two or more expressions together.

###**Syntax CONCAT()** 
```SQL
CONCAT(expression1, expression2, expression3,...)
```

**Example:**
```SQL
SELECT CONCAT(Address, " ", PostalCode, " ", City) AS Address
FROM Customers;
```

##`CONCAT_WS()` function 

The `CONCAT_WS()` function adds two or more expressions together with a separator.

##**Syntax CONCAT_WS()**
```SQL
CONCAT_WS(separator, expression1, expression2, expression3,...)
```

**Example**
```SQL
SELECT CONCAT_WS(" ", Address, PostalCode, City) AS Address
FROM Customers;
```
