# Itertools.combinations

This are use for combinatory construct, the usage of this methods is focus provide a series of tuples with all the sequence or set of numbers or letters used in the iterator.

```python
combinations(iterator, r)
```

Here `r` is an input, it represent the size of different combinations that are possible

```python
from itertools import combinations

letters ="victor"

# size of combination is set to 3
a = combinations(letters, 3)
comb = [' '.join(i) for i in a]

print(comb)

#['vic', 'vit', 'vio', 'vir', 'vct', 'vco', 'vcr', 'vto', 'vtr', 'vor', 'ict', 'ico', 'icr', 'ito', 'itr', 'ior', 'cto', 'ctr', 'cor', 'tor']
```

# Itertools.combinations

[itertools.combinations() | HackerRank](https://www.hackerrank.com/challenges/itertools-combinations/problem)

### Problem definition

**Task**

You are given a string.Your task is to print all possible combinations, up to size, of the string in lexicographic sorted order.

**Input Format**

A single line containing the string and integer value separated by a space.

**Output Format**

Print the different combinations of string on separate lines.

**Sample Input**

`HACK 2`

## Implementation

```python
from itertools import combinations

s , n  = input().split()

for i in range(1, int(n)+1):
    for j in combinations(sorted(s), i):
        print(''.join(j))
```

- `s` is the string
- `n` the length of the combination
- `for` loop, using a range that will be from `1` to the `n+1` , range upper limit not inclusive thus the `+1`
- Second `for` loop this time using the `combination` it is using `sorted()` to sort the string.
