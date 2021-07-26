# tee()

This iterator splits the container into a number of iterators mentioned in the argument.

**Syntax:**

```
tee(iterator, count)
```

**Parameter:** This method contains two arguments. 

- First argument is iterator
- Second argument is a integer

**Return Value:** This method returns the number of iterators mentioned in the argument.

```python
from itertools import tee

iterator1, iterator2 = tee([1,2,3,4,5,6], 2)

print (list(iterator1))  
print (list(iterator2))

#>>[1, 2, 3, 4, 5, 6]
#>>[1, 2, 3, 4, 5, 6]
```