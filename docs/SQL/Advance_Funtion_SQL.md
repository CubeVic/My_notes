##`CASE` function

The CASE statement goes through conditions and return a value when the first condition is met (like an IF-THEN-ELSE statement). So, once a condition is true, it will stop reading and return the result.

If no conditions are true, it will return the value in the ELSE clause.

If there is no ELSE part and no conditions are true, it returns NULL.

### **Syntax CASE** 

```SQL
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;
```

**Example** 

```SQL
SELECT CASE 
        WHEN A + B > C AND A + C > B AND B + C > A THEN CASE 
            WHEN A = B AND B = C THEN 'Equilateral' 
            WHEN A = B OR B = C OR A = C THEN 'Isosceles' 
            ELSE 'Scalene' END 
        ELSE 'Not A Triangle' END 
FROM TRIANGLES;
```

##`IF()` function

The `IF()` function returns a value if a condition is TRUE, or another value if a condition is FALSE.

### **Syntax IF()**

```SQL
IF(condition, value_if_true, value_if_false)
```

**Example**
```SQL
SELECT IF(500<1000, 5, 10);
```

```SQL
SELECT OrderID, Quantity, IF(Quantity>10, "MORE", "LESS")
FROM OrderDetails;
```