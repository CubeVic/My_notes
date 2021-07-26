# Itertools permutations

`Itertool` is a module provided by Python for creating iterators for efficient looping. It also provides various features or functions that work with iterators to produce complex iterators and help us to solve problems easily and efficiently in terms of time as well as memory.

permutation will receive two values

`permutations(iterator,r)`

- **Iterator:** will be the string or list that will be using as base for the permutation
- **r:** will be the length of the permutation item results

```python
from itertools import permutations

a = "geEk"

p = permutatations(a,2)

for j in p:
	print(j)
```

Results: 

('g', 'e')
('g', 'E')
('g', 'k')
('e', 'g')
('e', 'E')
('e', 'k')
('E', 'g')
('E', 'e')
('E', 'k')
('k', 'g')
('k', 'e')
('k', 'E')