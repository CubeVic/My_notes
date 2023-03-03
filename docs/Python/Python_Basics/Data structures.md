Related with data structures

## Data Structures

Data structures are containers that organize and group data types together in different ways.

## Mutability and Order

**Mutability** is about whether or not we can change an object once it has been created. If an object (like a list or string) can be changed (like a list can), then it is called mutable. However, if an object cannot be changed with creating a completely new object (like strings), then the object is considered
**immutable**.

**Order** is about whether the position of an element in the object can be used to access the element. Both strings and lists are ordered. We can use the order to access parts of a list and string.

## List
A list is one of the most common and basic data structures in Python.
List are Mutable and ordinated data structures

``` python
list_of_random_things = [1, 3.4, 'a string', True]
```

## Tuples
**Tuples** are a data type for _immutable_ _ordered_ sequences of elements. They are often used to store related pieces of information, **tuples** are immutable - you can't add and remove items from tuples, or sort them in place

``` python
location = (13.4125, 103.866667)
```
Tuples can also be used to assign multiple variables in a compact way. In the example bellow, a tuple called dimensions is created, next, the content of this tuple is unpack, in three different variables, this is called **tuple unpacking.**

``` python
dimensions = 52, 40, 100
length, width, height = dimensions
```
The parentheses are optional when defining tuples, and programmers frequently omit them if parentheses don't clarify the code.

## Set

A **set** is a data type for mutable unordered collections of unique elements. One application of a set is to quickly remove duplicates from a list, it is an unordered data type, there fore if the method `.pop()` is use there is no way to know exactly with element will be eliminated.

``` python
numbers = [1, 2, 6, 3, 1, 1, 6]
unique_nums = set(numbers)
print(unique_nums)
```
It will output:

```
{1, 2, 3, 6}
```

## Dictionaries

A **dictionary** is a mutable data type that stores mappings of unique keys to values.

```python
elements = {"hydrogen": 1, "helium": 2, "carbon": 6}
```

Dictionaries can have keys of any immutable type, like integers or tuples, not just strings. It's not even necessary for every key to have the same type.

If you expect lookups to sometimes fail, `get` might be a better tool than normal square bracket lookups because errors can crash your program.

```python
print("carbon" in elements)
print(elements.get("dilithium"))
```
this would output:

```
True
None
```

So, to recap

Data Structure | Ordered | Mutable | Constructor     | Example             |
:--------------|:-------:|:-------:|:----------------|:--------------------|
List           | Yes     | Yes     |`[]` or `list()` | `[5.7,4,'yesy',5.7]`|
Tuple          | Yes     | No      |`()` or `tuple()`|`(5.7,4,'yes',5.7)`  |
Set            | No      | Yes     |`{}`[^1] or `set()` |`{5.7,4,'yes'}`      |
Dictionary     | No      | No[^2]  |`{}` or `dict()` |`{'jun':75.'jul':89}`|

[^1]: You can use curly braces to define a set like this: `{1, 2, 3}`. However, if you leave the curly braces empty like this: `{}` Python will instead create an empty dictionary. So to create an empty set, use `set()`.
[^2]: A dictionary itself is mutable, but each of its individual keys must be immutable.
