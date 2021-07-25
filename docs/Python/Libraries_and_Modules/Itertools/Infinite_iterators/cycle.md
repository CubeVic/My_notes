# cycle()

Arg: p
Example: cycle('ABCD') ⇒ A B C D A B C D ...

It will return elements of the iterable and save a copy of each, when the iterator is exhausted it will rerun the elements of the iterable 

```python
for itertool import cycle

str_cycle = "victor"

n = cylce(str_cycle)

for _ in range(1,12):
	print(n.next())

>> v
>> i
>> c
>> t
>> o
>> r
>> v
>> i
>> c
>> t
```