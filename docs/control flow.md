## Iterating through Dictionaries with `For` loops

The iteration through Dictionaries in pyhton is a different than Swift, in this case to iterate and get back both *key* and *value* you need to use a built-in method `item`.

For example: 

```python

cast = {
           "Jerry Seinfeld": "Jerry Seinfeld",
           "Julia Louis-Dreyfus": "Elaine Benes",
           "Jason Alexander": "George Costanza",
           "Michael Richards": "Cosmo Kramer"
       }

for key,value in cast.items():
	print("Actor: {}   Role: {}".format(key,value))

```

which will result in something like: 

```
Actor: Jerry Seinfeld    Role: Jerry Seinfeld
Actor: Julia Louis-Dreyfus    Role: Elaine Benes
Actor: Jason Alexander    Role: George Costanza
Actor: Michael Richards    Role: Cosmo Kramer
```

## `for` Loops vs. `while` Loops

`for` loops are idea when the *number of iteration* are _known_ or _finite_.  

Examples:  

* When you have an iterable collection (list, string, set, tuple, dictionary):  
```python
for name in names:
```

* When you want to iterate through a loop for a definite number of times, using `range()`
```python
for i in range(5):
```

`while` loop are ideal when the *iterations* are to _continue until a condition is met_  

Examples:

* When you want to use comparison operations:
``` python
while count <= 100:
```

* When you want to loop base on receiving specific user input
```python
while user_input == 'y'
```

the following are required to build a correct `while` loop: 

* The condition for existing the while loop should be included.  
* Check if the iteration conditions is met.  
* Body of the loop should change the value of condition variables.  
##Break and continue.  

* `break` terminates a loop.  
* `continue` skips one iteration of a loop.  

## Zip and Enumerate
`zip` and `enumerate` are build-in functions that can come handy when dealing with loops.

**Zip**

`zip` will return  an iterator that combine multiples iterables into one sequence of tuples, this will be more clear with an example:

```python
list(zip(['a','b','c'], [1,2,3]))
```

which out put will be:

```python
[('a',1),('b',2),('c',3)]
```

In this case we can see that `zip` create a iterator that combine the two provided iterables and each iterator is a tuple with items in the position of the original iterable.

the reverse or Unzip process can be done using the *

```python
letters = ['a','b','c']
nums = [1,2,3]

for letter, num in zip(letters,nums):
	print("{}:{}".format(letter,num))

some_list = [('a',1),('b',2),('c',3)]
letters, nums = zip(*some_list)
```

**Enumerate**  
`enumerate` is a built in function that return an iterator of tuples containing indexes and values of a list, example:

```python
letters = ['a','b','c','d','e']

for i, letter in enumerate(letters):
	print(i, letter)
```

this will be the output:

```
0 a
1 b
2 c
3 d
4 e
```

an example of `enumerate`, here:

```python
cast = ["Barney Stinson", "Robin Scherbatsky", "Ted Mosby", "Lily Aldrin", "Marshall Eriksen"]
heights = [72, 68, 72, 66, 76]

for i, character in enumerate(cast):
    cast[i] = character + " " + str(heights[i])

print(cast)
```

It will take 2 list and it will out put a single list of items that include a both original list as a single string

```
['Barney Stinson 72', 'Robin Scherbatsky 68', 'Ted Mosby 72', 'Lily Aldrin 66', 'Marshall Eriksen 76']
```

## List Comprehensions  

List comprehensions are just present in python and not in other languages, this are normally use to create a list in a quickly and concisely way, for example:

```python
capitalized_cities = []
for city in cities:
    capitalized_cities.append(city.title())
```

can be reduce to:

```python
capitalized_cities = [city.title() for city in cities]
```

Conditional can be added to this list comprehensions (listcomps).
be aware that if the conditional has a `else` statement the syntax will be a bit different.

Lets start with a simply conditional.

```python
squares = [x**2 for x in range(9) if x % 2 == 0]
```

this will create a list with the power of the even numbers 

if you want to add a `else`, you will get a syntax error 

```python
squares = [x**2 for x in range(9) if x % 2 == 0 else x + 3] # this will produce a syntax error
```

in this case, it is necessary move all the block to the beginning.

```python
squares = [x**2 if x % 2 == 0 else x + 3 for x in range(9)]
```

## Exercise using the dictionaries and for loops

Provide a list with the name(s) of the director(s) with the most Oscar wins. We are asking for a list because there could be more than 1 director tied for the most Oscar wins.

```python
winners = {1931: ['Norman Taurog'], 1932: ['Frank Borzage'], 1933: ['Frank Lloyd'], 1934: ['Frank Capra'], 1935: ['John Ford'], 1936: ['Frank Capra'], 1937: ['Leo McCarey'], 1938: ['Frank Capra'], 1939: ['Victor Fleming'], 1940: ['John Ford'], 1941: ['John Ford'], 1942: ['William Wyler'], 1943: ['Michael Curtiz'], 1944: ['Leo McCarey'], 1945: ['Billy Wilder'], 1946: ['William Wyler'], 1947: ['Elia Kazan'], 1948: ['John Huston'], 1949: ['Joseph L. Mankiewicz'], 1950: ['Joseph L. Mankiewicz'], 1951: ['George Stevens'], 1952: ['John Ford'], 1953: ['Fred Zinnemann'], 1954: ['Elia Kazan'], 1955: ['Delbert Mann'], 1956: ['George Stevens'], 1957: ['David Lean'], 1958: ['Vincente Minnelli'], 1959: ['William Wyler'], 1960: ['Billy Wilder'], 1961: ['Jerome Robbins', 'Robert Wise'], 1962: ['David Lean'], 1963: ['Tony Richardson'], 1964: ['George Cukor'], 1965: ['Robert Wise'], 1966: ['Fred Zinnemann'], 1967: ['Mike Nichols'], 1968: ['Carol Reed'], 1969: ['John Schlesinger'], 1970: ['Franklin J. Schaffner'], 1971: ['William Friedkin'], 1972: ['Bob Fosse'], 1973: ['George Roy Hill'], 1974: ['Francis Ford Coppola'], 1975: ['Milos Forman'], 1976: ['John G. Avildsen'], 1977: ['Woody Allen'], 1978: ['Michael Cimino'], 1979: ['Robert Benton'], 1980: ['Robert Redford'], 1981: ['Warren Beatty'], 1982: ['Richard Attenborough'], 1983: ['James L. Brooks'], 1984: ['Milos Forman'], 1985: ['Sydney Pollack'], 1986: ['Oliver Stone'], 1987: ['Bernardo Bertolucci'], 1988: ['Barry Levinson'], 1989: ['Oliver Stone'], 1990: ['Kevin Costner'], 1991: ['Jonathan Demme'], 1992: ['Clint Eastwood'], 1993: ['Steven Spielberg'], 1994: ['Robert Zemeckis'], 1995: ['Mel Gibson'], 1996: ['Anthony Minghella'], 1997: ['James Cameron'], 1998: ['Steven Spielberg'], 1999: ['Sam Mendes'], 2000: ['Steven Soderbergh'], 2001: ['Ron Howard'], 2002: ['Roman Polanski'], 2003: ['Peter Jackson'], 2004: ['Clint Eastwood'], 2005: ['Ang Lee'], 2006: ['Martin Scorsese'], 2007: ['Ethan Coen', 'Joel Coen'], 2008: ['Danny Boyle'], 2009: ['Kathryn Bigelow'], 2010: ['Tom Hooper']}
```

first step, is "open the dictionary", i will need to list the directors as a key and the number of wins as a value, for that i can use the for loops and the `get` method of dictionaries

```python
most_win_director = [] # i will use this list later to print the results

win_dict = {} # this Dictionary will hold the directors and the values ( number of wins)

for year, winner_name in winner.item():
	for winner in winner_name:
		win_dict[winner] = win_dict.get(winner,0) + 1
```

so in this step i get a dictionary that holds the name and the number of wins

```
{'Peter Jackson': 1, 'Anthony Minghella': 1, 'Robert Redford': 1, 'Clint Eastwood': 2, 'Ron Howard': 1, 'Billy Wilder': 2, 'Steven Spielberg': 2, 'Richard Attenborough': 1, 'Mel Gibson': 1, 'Leo McCarey': 2, 'William Friedkin': 1, 'Barry Levinson': 1, 'Oliver Stone': 2, 'Warren Beatty': 1, 'Ang Lee': 1, 'Joseph L. Mankiewicz': 2, 'Sydney Pollack': 1, 'Robert Wise': 2, 'Woody Allen': 1, 'John Ford': 4, 'Bob Fosse': 1, 'Jerome Robbins': 1, 'Robert Benton': 1, 'Elia Kazan': 2, 'Frank Lloyd': 1, 'John G. Avildsen': 1, 'Tom Hooper': 1, 'Frank Borzage': 1, 'Sam Mendes': 1, 'John Huston': 1, 'Carol Reed': 1, 'Francis Ford Coppola': 1, 'Joel Coen': 1, 'Fred Zinnemann': 2, 'William Wyler': 3, 'Jonathan Demme': 1, 'Kathryn Bigelow': 1, 'Delbert Mann': 1, 'Danny Boyle': 1, 'George Cukor': 1, 'Norman Taurog': 1, 'Tony Richardson': 1, 'George Roy Hill': 1, 'James L. Brooks': 1, 'Martin Scorsese': 1, 'David Lean': 2, 'Franklin J. Schaffner': 1, 'Bernardo Bertolucci': 1, 'John Schlesinger': 1, 'Ethan Coen': 1, 'Michael Cimino': 1, 'Milos Forman': 2, 'Mike Nichols': 1, 'Michael Curtiz': 1, 'Steven Soderbergh': 1, 'Robert Zemeckis': 1, 'Kevin Costner': 1, 'Frank Capra': 3, 'Vincente Minnelli': 1, 'James Cameron': 1, 'George Stevens': 2, 'Roman Polanski': 1, 'Victor Fleming': 1}
```  

now I will need to create a variable `highest_wins` I will change the value of this variable every time I encounter a director with a higher number of wins, and I will clean the `most_win_director` and append the a new name.  

```python
highest_wins = 0
 
for director, wins in win_dict.items():  
    if wins > highest_wins:  
        highest_wins = wins  
        most_win_director.clear()  
        most_win_director.append(director)  
    elif wins == highest_wins:  
        most_win_director.append(director)  
    else:  
        continue 
```
 finally print the solution:  

```python 
 print("most_win_director = {}".format(most_win_director))
```


and here a more compact solution using `max` and _list comprehension_:

```python 
highest_count = max(win_count_dict.values())

most_win_director = [key for key, value in win_count_dict.items() if value == highest_count]
```