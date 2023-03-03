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

## `SET @var_name` User-defined Variables

You can store a value in a user-defined variable in one statement and refer to it later in another statement. This enables you to pass values from one statement to another.

User variables are written as @var_name, where the variable name var_name consists of alphanumeric characters, ., _ , and $.

User variable names are not case-sensitive. Names have a maximum length of 64 characters.

One way to set a user-defined variable is by issuing a `SET` statement:

```SQL
SET @var_name = expr [, @var_name = expr] ...
```

For `SET`, either `=` or `:=` can be used as the assignment operator.

When making an assignment in this way, you must use `:=` as the assignment operator; `=` is treated as the comparison operator in statements other than `SET`.


Here ans example of the usage of this "user-defined variables", this is the solution to the challenge [Occupations](https://www.hackerrank.com/challenges/occupations/problem) of [Hacker Ranks](https://www.hackerrank.com)

```SQL
SET @dRow = 0, @pRow = 0, @sRow = 0, @aRow = 0;

SELECT MIN(Doctor), MIN(Professor), MIN(Singer), MIN(Actor)
FROM (
    SELECT  CASE Occupation
                WHEN 'Doctor'       THEN @dRow := @dRow + 1
                WHEN 'Professor'    THEN @pRow := @pRow + 1
                WHEN 'Singer'       THEN @sRow := @sRow + 1
                WHEN 'Actor'        THEN @aRow := @aRow + 1
            END AS row,
            IF (Occupation = 'Doctor', Name, NULL) AS Doctor,
            IF (Occupation = 'Professor', Name, NULL) AS Professor,
            IF (Occupation = 'Singer', Name, NULL) AS Singer,
            IF (Occupation = 'Actor', Name, NULL) AS Actor
    FROM    OCCUPATIONS
    ORDER BY Name
) a
GROUP BY row;
```
