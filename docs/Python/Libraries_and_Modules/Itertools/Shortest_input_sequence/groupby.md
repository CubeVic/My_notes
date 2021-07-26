# groupby()

***Syntax:** itertools.groupby(iterable, key_func)*

***Parameters:***

- ***iterable:** Iterable can be of any kind (list, tuple, dictionary).*
- ***key:** A function that calculates keys for each element present in iterable.*

This method calculates the keys for each element present in iterable. It returns key and iterable of grouped items.

It is still not a good description of this method, in the following example we will use a lambda function as part of the key. 

```python
from iter import groupby
  
L = [("a", 1), ("a", 2), ("b", 3), ("b", 4)]
  
# Key function
key_func = lambda x: x[0]
  
for key, group in groupby(L, key_func):
    print(key + " :", list(group))

# output
#a : [('a', 1), ('a', 2)]
#b : [('b', 3), ('b', 4)]
```

In this case the Lambda function will extract the first element of the tuple inside the list ( the `a` and `b` ) and use them as Keys, later the same iterable will be group base on the key.