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
