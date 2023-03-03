## Reading and Writing Files

Python has the ability to open, create, write and "modify" files, write and modify has some point to take in count that we will address later.

## Reading a File

To read a file you will need to:

1. Open the file with the built-in function `open`, for this we will need a string with the location or path to this file, this will return an object file, this object is what Python use to interact with the document.
2. There are optional parameters you can specify in the `open` function. One is the mode in which we open the file. if we use `r` ( which is the value by default) the mode will be read only.
3. Use the `read` method to access the contents from the file object. this `read` method takes the text content in the file and puts into a string.
4. (**IMPORTANT**) when finished with the file, use the `close` method to free up any system resources taken up by the file.

the code will be something like:

```python
f = open('my_path/my_file.txt', 'r')
file_data = f.read()
f.close()
```

## Writing to File

Now, to write we need to the open the file in write mode, but it is important to know that this will remove any previous content in the document.

1. Open the file in writing ('w') mode. if the file does not exist, Python will create it for you, if the file exist all the content will be delete, if the intention is to add information to this document we will need to open it in append mode ('a').
2. Use the write method to add text to the file.
3. Close the file when finished.

so the code will look like:

```python
f = open('my_path/my_file.txt', 'w')
f.write("Hello there!")
f.close()
```

Now it is important to close the files after use them, but in some case can be easy to forget to close the files, in that case we can use the block `with`, we will be able to access the file within this block and after we finish the file will be close automatically, example:

```python
with open('my_path/my_file.txt','r') as f:
	file_data = f.data()
```

so in this case the `as f`  is equal to `f = open('my_path/my_file.txt','r')` we can access the file using f within the indented `with`block and we don't need to use `f.close()`.

## About Reading the Files

By default the `read()` method has no argument and it gives back the content of the file, but, we can use integer argument, this will give back the number of characters pass as argument and leave the window open, this will be easy to understand in a example:

let assume the document `camelot.txt` contain:

```
We're the knights of the round table
We dance whenever we're able
```

and we have the following code:

```python
with open("camelot.txt") as song:
    print(song.read(2))
    print(song.read(8))
    print(song.read())
```

the output will be:

```
We
're the
knights of the round table
We dance whenever we're able
```

this will be really difficult to know in which position are we after each `read()` statement.

Now, python is smart enough to understand that `\n` which is a character that means newline means that the sentences finish and there is a new line. For this cases we can use `readline()`.

although there is a way to loop over the lines of the file, this can be done with the syntax `for line in file` and using the `.strip()` we can remove the `\n`.

```python
camelot_lines = []
with open("camelot.txt") as f:
    for line in f:
        camelot_lines.append(line.strip())

print(camelot_lines)
```
the output will be:

```
["We're the knights of the round table", "We dance whenever we're able"]
```
