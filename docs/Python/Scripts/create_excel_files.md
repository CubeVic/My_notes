First we are going to create a csv file using the build-in csv module, after that we will proceed to use a third party library to create a xlsx file.

## Creating a CSV file

To be able to work with this type of file we are going to import CSV in the following way

```python
import csv
```

### CVS Module

the CVS module includes all necessary methods built-in some of which are:

* csv.reader  
* csv.writer  
* csv.DictReader  
* csv.DictWriter  

with this method we can edit, modify and manipulate the stored data in a csv file.

### Initial preparation 

First we will need to prepare the file so it can be run with `python namefile.py` for that we  add the `if __name__ == "__main__"`

```python
import csv




if __name__ = "__main__":
	main()
```

#### Name of the file, header and data

Now, we proceed to define some variables, the name of the file with `filename`, later the headers ( or the name of the columns) with `header` and provide some data with `data`

```python
import csv

filename = "imdb_top_4.csv"
header = ("Rank", "Rating", "Title")
data = [
(1, 9.2, "The Shawshank Redemption(1994)"),
(2, 9.2, "The Godfather(1972)"),
(3, 9, "The Godfather: Part II(1974)"),
(4, 8.9, "Pulp Fiction(1994)")
]


if __name__ = "__main__":
	main()

```

### Function to write on the file

The next step will be create a function that write the data on the file,
this function will have 3 parameters, `header`,`data`, and `filename`.
Inside this function we will write the first line of the file with the content of header, this will give the name to the columns and later with a `for` loop we will write the data.


```python

def writer(header,data,filename):
	with open(filename,"w",newline = " ") as csvfile:
		movies = cvs.writer(csvfile)
		movies.writerow(header)
		for x in data:
			movies.writerow(x)
```

so the full, first version of the script will be, notice that there is a call to the function `writer` after the variable `data` is defined.

```python
import csv

filename = "imdb_top_4.csv"
header = ("Rank", "Rating", "Title")
data = [
(1, 9.2, "The Shawshank Redemption(1994)"),
(2, 9.2, "The Godfather(1972)"),
(3, 9, "The Godfather: Part II(1974)"),
(4, 8.9, "Pulp Fiction(1994)")
]

writer(header, data, filename, "write")

def writer(header,data,filename):
	with open(filename,"w",newline = " ") as csvfile:
		movies = cvs.writer(csvfile)
		movies.writerow(header)
		for x in data:
			movies.writerow(x)




if __name__ = "__main__":
	main()

```

And the result will be like:

![create_excel_files_001](../images/create_excel_files_001.png)

### Updating a CSV files

To update this type of file and in this case we will need to create a new function named '*updater*' that will just take the `filename` as a parameter.


```python
def updater(filename):
	with open(filename, newline= "") as file:
		readData = [row for row in csv.DictReader(file)]
		readData[0]['Rating'] = '9.4'

		readHeader = readData[0].keys()
		writer(readHeader,readData,filename,"update")
```

In this function:

1. We open the file define in `filename` and we are going to called it 'file'.
2. Save all the information from that file in a variable called `readData`,  [cvs.DictReader](https://docs.python.org/3/library/csv.html#csv.DictReader)
3. the next line `readData[0]['Rating'] = '9.4'` is hard-coding the value 9.4 in the 'Rating' column.
4. the last line will tell the function `writer` that we are executing an update ( this option is not yet define in the function `writer` that will be the next step)
5. finally we add a call to the function `uodater` after the call to the function `writer`

```python
import csv

filename = "imdb_top_4.csv"
header = ("Rank", "Rating", "Title")
data = [
(1, 9.2, "The Shawshank Redemption(1994)"),
(2, 9.2, "The Godfather(1972)"),
(3, 9, "The Godfather: Part II(1974)"),
(4, 8.9, "Pulp Fiction(1994)")
]

writer(header, data, filename, "write")
updater(filename)

def writer(header,data,filename):
	with open(filename,"w",newline = " ") as csvfile:
		movies = cvs.writer(csvfile)
		movies.writerow(header)
		for x in data:
			movies.writerow(x)
	# TODO option to update

def updater(filename):
	with open(filename, newline= "") as file:
		readData = [row for row in csv.DictReader(file)]
		readData[0]['Rating'] = '9.4'

		readHeader = readData[0].keys()
		writer(readHeader,readData,filename,"update")


if __name__ = "__main__":
	main()

```

#### Create the option for update

Now, we need to modify the function `writer` to be able to receive an extra parameter, and inside, some modifications to handle these options for "*write*"
and "*update*".

1. lets add the extra parameter, this will be called **option**

```python
def writer(header, data, filename, option):
	...
```

2. Inside we are going to create a decision loop to execute some part of the code depending of the the parameter **option** 

```python
def writer(header, data, filename, option):
	with open(filename, "w", newline = "") as csvfile:
		if option == "write":
			movies = csv.writer(csvfile)
			movies.writerow(headers)
			for x in data:
				movies.writerow(x)

		elif option == "update":
			writer = csv.DictWriter(csvfile, fieldnames = headers)
			writer.writeheader()
			write.writerow(data)
		else:
			print("option is not know")
```

More information about `DictWriter` [here](https://docs.python.org/3/library/csv.html#csv.DictWriter.writeheader) but basically here is use to write a row with the field names.

so with all this changes we will have a script that look like this: 

```python
import csv

filename = "imdb_top_4.csv"
header = ("Rank", "Rating", "Title")
data = [
(1, 9.2, "The Shawshank Redemption(1994)"),
(2, 9.2, "The Godfather(1972)"),
(3, 9, "The Godfather: Part II(1974)"),
(4, 8.9, "Pulp Fiction(1994)")
]


writer(header, data, filename, "write")
updater(filename)


def writer(header, data, filename, option):
	with open(filename, "w", newline = "") as csvfile:
		if option == "write":
			movies = csv.writer(csvfile)
			movies.writerow(headers)
			for x in data:
				movies.writerow(x)

		elif option == "update":
			writer = csv.DictWriter(csvfile, fieldnames = headers)
			writer.writeheader()
			write.writerow(data)
		else:
			print("option is not know")

def updater(filename):
	with open(filename, newline= "") as file:
		readData = [row for row in csv.DictReader(file)]
		readData[0]['Rating'] = '9.4'

		readHeader = readData[0].keys()
		writer(readHeader,readData,filename,"update")


if __name__ = "__main__":
	main()

```






































