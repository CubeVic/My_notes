# Itertools

![Itertools](images/Itertools.png){: .center}

### Why I make notes about it

I found many of the challenges websites can be solved using these iterators.

##Description
Itertools is a module which is implementing of the iterator building blocks of other well known programing languages,
this is the implementation on python.

[Itertools documentation](https://docs.python.org/3/library/itertools.html)

These are memory-efficient tools that are useful either using them alone or in combination.

They are divided in  three big main categories:

1. Infinite iterators
2. Iterators on the shortest input sequence
3. combinatorics iterators

## 1. Infinite Iterators

These are apparently 3 different iterators to get **N** repetitions of the same number, Count from an N number a define number of steps in a direction, and cycle over a string.

|Name |Arg      |Example      |
|:---:|:--------|:------------|
|count()|"start, [step]"|count(10) ⇒ 10 11 12 13 14|
|cycle()|p|cycle('ABCD') ⇒ A B C D A B C D ...|
|repeat()|"elem [,n]"|"repeat(10,3) ⇒ 10 10 10"|

## 2. Iterators terminating on the shortest input sequence

These are more difficult to understand just by reading the title, but the example will help to make it clear

| Name                | arg             |Results | Example|
|:--------------------|:----------------|:--------------------------|:-------------------------------------|
|accumulate()         | p [, func]      | p0, p0+p1. p0+p1+p2       | accumulete([1,2,3,4,5]) ⇒ 1 3 6 10 15|
|chain()              | p, q, …         | p0, p1, … plast, q0, q1, …| chain('ABC', 'DEF') ⇒ A B C D E F|
|chain.from_iterable()| iterable        | p0, p1, … plast, q0, q1, …| chain.from_iterable(['ABC', 'DEF']) ⇒ A B C D E F|
|compress()           | data, selectors | "(d[0] if s[0]), (d[1] if s[1]), … | compress('ABCDEF', [1,0,1,0,1,1]) ⇒ A C E F|
|dropwhile()          | pred, seq       | seq[n], seq[n+1], starting when pred fails | dropwhile(lambda x: x<5, [1,4,6,4,1]) ⇒ 6 4 1|
|filterfalse()        | pred, seq       |elements of seq where pred(elem) is false | filterfalse(lambda x: x%2, range(10)) ⇒ 0 2 4 6 8|
|groupby()            |iterable [, key] |sub-iterators grouped by value of key(v)| |
|islice()             |seq, [start,] stop [, step]|elements from seq[start:stop:step] | islice('ABCDEFG', 2, None) ⇒ C D E F G|
|starmap()            |func, seq |func(*seq[0]) func(*seq[1]), … |starmap(pow, [(2,5), (3,2), (10,3)]) --> 32 9 1000|
|takewhile()          |pred, seq | seq[0], seq[1] until pred fails | takewhile(lambda x: x<5, [1,4,6,4,1]) --> 1 4"|
|tee()                | it, n |it1, it2, … itn | splits one iterator into n |
|zip_longest()        | p, q, … |  (p[0], q[0]), (p[1], q[1]), … | zip_longest('ABCD', 'xy', fillvalue='-') --> Ax By C- D-|

## 3. Combinatoric iterator

| Name | arg  | Result| Results|
|:-----|:-----|:------|:-------|
| product()      | p, q, … [repeat=1] | AA AB AC AD BA BB BC BD CA CB CC CD DA DB DC DD | cartesian product, equivalent to a nested for-loop|
| permutations() | p[, r] | AB AC AD BA BC BD CA CB CD DA DB DC | r-length tuples, all possible orderings, no repeated elements|
| combinations() | p, r | AB AC AD BC BD CD |r-length tuples, in sorted order, no repeated elements|
| combinations_with_replacement() | p, r | AA AB AC AD BB BC BD CC CD DD | r-length tuples, in sorted order, with repeated elements|

> Icons made by [Freepik](https://www.flaticon.com/)
