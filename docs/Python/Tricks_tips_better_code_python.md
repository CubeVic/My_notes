> This notes are base in the Medium post called ["five Python tricks you need to learn today"](https://towardsdatascience.com/five-python-tricks-you-need-to-learn-today-9dbe03c790ab)


## TIp 1: Clean - Powerful One-liners

### Conditional statements 

A normal If conditional will look like this:

```python
if alpha > 7 :
	beta = 999
elif alpha == 7:
	beta = 99
else:
	beta = 0
```

but this can be one line, can be simplify int his way:

```python
beta == 999 if alpha > 7 else 99 if alpha == 7 else 0
```

### `for` loops

for example, doubling a list of integers in four lines:

```python
lst = [1,3,5]
doubled = []
for num in lst:
	doubled.append(num*2)
```

and it can be simplify to just one line:

```python
double = [num * 2 for num in lst]
```

## Tip 2: String Manipulation

### Reverse a string 

we can use `::-1` to reverse a string, like this:

```python
a = "ilovemyjob"
print a[::-1]
#bojymevoli
```

### `join` strings 

we can print the result of join different strings, or item of a list together:

let say we have this:
```python
str1 = "Totally"
str2 = "Awesome"
lst3 = ["Omg", "You", "Are"]
```

so we can use `join()` method to create the outcome:

```python
print ' '.join(lst3)
#Omg You Are
print ' '.join(lst3)+' '+str1+' '+str2
#Omg You Are Totally Awesome
```


