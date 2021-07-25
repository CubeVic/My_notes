# repeat()

Arg: elem [,n]
Example: repeat(10,3) ⇒ 10 10 10

Make iterable that will return objects over and over again, it will run infinitely at less the time is specify, that time will be the value of `n`.

```python
from itertools import repeat

r = repeat(10,4)

while True:
	try:
		print(m.next())
	except:
		break

>> 10
>> 10
>> 10
>> 10
```