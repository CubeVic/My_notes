# Itertools

![Itertools](images/itertools.png){: .center}

This is a built-in library so there ir is not necessary to installed with PIP

### Why I make notes about it

I'm making note about this , since I found that many of the challenges in the website can be solved using these iterators,
so I think it is a good idea.

##Description
Itertools is a module which is implementing of the iterator building blocks of other well known programing languages, 
this is the implementation on python.

[Itertools documentation](https://docs.python.org/3/library/itertools.html)

These are memory-efficient tools that are useful either using them alone or in combination.

They are divided in  three big main categories:

1. Infinite iterators
2. Iterators on the shortest input sequence 
3. combinatorics iterators 

## Infinite Iterators

These are apparently 3 different iterators to get **N** repetitions of the same number, Count from an N number a define number of steps in a direction, and cycle over a string.

|Name |Arg      |Example      |
|:---:|:--------|:------------|
|count()|"start, [step]"|count(10) ⇒ 10 11 12 13 14|
|cycle()|p|cycle('ABCD') ⇒ A B C D A B C D ...|
|repeat()|"elem [,n]"|"repeat(10,3) ⇒ 10 10 10"|

## Iterators terminating on the shortest input sequence

These are more difficult to understand by the title





> Icons made by [Freepik](https://www.flaticon.com/)