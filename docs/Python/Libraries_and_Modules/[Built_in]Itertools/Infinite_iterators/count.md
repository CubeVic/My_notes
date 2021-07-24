# count()

[Documentation](https://docs.python.org/3/library/itertools.html#itertools.count)

Return an iterator with evenly spaced starting from the start, space by the step, default step is 1.

```python
from itertools import count

n = count(start=10)

for i in range(1,7):
	print(n.next())
	
>> 10
>> 11
>> 12
>> 13
>> 14
>> 15
```