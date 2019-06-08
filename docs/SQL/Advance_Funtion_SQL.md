## CASE Function

The CASE statement goes through conditions and return a value when the first condition is met (like an IF-THEN-ELSE statement). So, once a condition is true, it will stop reading and return the result.

If no conditions are true, it will return the value in the ELSE clause.

If there is no ELSE part and no conditions are true, it returns NULL.

### **Syntax** of CASE Function
```SQL
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;
```

### **Example** CASE Function

```SQL
SELECT CASE 
        WHEN A + B > C AND A + C > B AND B + C > A THEN CASE 
            WHEN A = B AND B = C THEN 'Equilateral' 
            WHEN A = B OR B = C OR A = C THEN 'Isosceles' 
            ELSE 'Scalene' END 
        ELSE 'Not A Triangle' END 
FROM TRIANGLES;
```
