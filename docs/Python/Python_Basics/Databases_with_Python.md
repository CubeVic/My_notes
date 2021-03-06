In this examples we are going to use SQLite as database.

## Import, Connect and Cursor

To start to use SQLite with python we will need to import the library 'sqlite3', once imported we can start using it, first we will establish a connection with the database using `sqlite3.connect()`, later, to start the navigation we will need a cursor, for that we use  `.cursor()`.

```python 
import sqlite3

conn = sqlite3.connect('name database')
cur = conn.cursor()
```

using as example chapter 15 of  "Python for everyone" as an example we have

```python
import sqlite3

conn = sqlite3.connect('rosterdb.sqlite')
cur = conn.cursor()

```

where `rosterdb.sqlite` is the name of the database 

## `executescript()` and `execute()`

there are two ways to execute SQL statements in python, one will be `executescript()` this will allow me to execute several SLQ statement art the same time, if this statement finish with ";". The second option will be `execute()` this will be limited to one SQL statement.

### `executescript()` example

In the following code we will execute several SLQ statement

1. we start with `executescript()`, we are goin to use "\'\'\'".

```python
import sqlite3

conn = sqlite3.connect('rosterdb.sqlite')
cur = conn.cursor()

cur.executescript(''' SQL statements''')
```

2. We will delete any existing tables with the names "User", "Member", "Course"

```python
import sqlite3

conn = sqlite3.connect('rosterdb.sqlite')
cur = conn.cursor()

cur.executescript(''' 
DROP TABLE IF EXISTS User;
DROP TABLE IF EXISTS Member;
DROP TABLE IF EXISTS Course;
''')
```
3. Now we will create 3 tables; "User", "Course", "Member". Member table contain a primary key composed of take two parameters, this is a way to link to the other 2 tables and create the many to many relationship

```python
import sqlite3

conn = sqlite3.connect('rosterdb.sqlite')
cur = conn.cursor()

# Do some setup
cur.executescript('''
DROP TABLE IF EXISTS User;
DROP TABLE IF EXISTS Member;
DROP TABLE IF EXISTS Course;

CREATE TABLE User (
    id     INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT UNIQUE,
    name   TEXT UNIQUE
);

CREATE TABLE Course (
    id     INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT UNIQUE,
    title  TEXT UNIQUE
);

CREATE TABLE Member (
    user_id     INTEGER,
    course_id   INTEGER,
    role        INTEGER,
    PRIMARY KEY (user_id, course_id)
)
''')
```


## `INSERT`, `IGNORE`, `REPLACE` and `SELECT`

In previous steps we create the shema of the database, now we need to populate this database with information, in this case we are goin to extract information from a JSON file and use it to feed the datase.

### Getting the data from JSON

First we need to import json

```python
import json
[...]
```

second we need to get the information of a JSON file, in this case we are going to use one of the JSON file examples from the book "Python for everyone"

```python
[...]
fname = input('Enter file name: ')
if len(fname) < 1:
    fname = 'roster_data_sample.json'

# [
#   [ "Charley", "si110", 1 ],
#   [ "Mea", "si110", 0 ],

str_data = open(fname).read()
json_data = json.loads(str_data)
[...]
```

Now all the information is in the variable `json_data` (a list) we will need though this list

```python
[...]
fname = input('Enter file name: ')
if len(fname) < 1:
    fname = 'roster_data_sample.json'

# [
#   [ "Charley", "si110", 1 ],
#   [ "Mea", "si110", 0 ],

str_data = open(fname).read()
json_data = json.loads(str_data)
print(type(json_data))

for entry in json_data:

    name = entry[0]
    title = entry[1]
    role = entry[2]

    print((name, title, role))

```

## `INSERT OR IGNORE`

Now we are goin to insert the information in the different tables, for that we will use `INSERT` and we will add `IGNORE` to avoid those cases when a error appears

```python 
   cur.execute('''INSERT OR IGNORE INTO User (name)
        VALUES ( ? )''', ( name, ) )
```

in the previous statement `execute()` will execute an `INSERT` instruction to the "User" table, to the column "name", the "?" is a placeholder and the "`(name,)`" is a tuple that indicade that the information on the variable "name" is going to be place in the "?", and this information will be insert in the table "User".

Bellow the example of the other statement, the only remark will be the usage of `REPLACE` which will replace the value of what ever is in that column(s).

```python
    cur.execute('''INSERT OR IGNORE INTO User (name)
        VALUES ( ? )''', ( name, ) )


    cur.execute('''INSERT OR IGNORE INTO Course (title)
        VALUES ( ? )''', ( title, ) )


    cur.execute('''INSERT OR REPLACE INTO Member
        (user_id, course_id, role) VALUES ( ?, ?, ? )''',
        ( user_id, course_id, role ) )
```
### `SELECT` and `fetchone()[0]`

now we are going to select one of the records in the database and store the first row, for this we will execute the `SELECT` and later use `fetchone[0]` to store the first record

```python
    cur.execute('SELECT id FROM User WHERE name = ? ', (name, ))
    user_id = cur.fetchone()[0]
``` 
we use "[0]" to be sure that we will get just the first record ( `fetchone()` will get back just one record, to get more you can use `fetchall()`)

## `commit`

Finally to commit this changes or this addition to the database we can use the function `commit()`, this will commit the changes to the database and wait until is done, that is one of the reason in some case the commit is done after several changes and not after each change, since this will make the execution of the script slower.

```python
    conn.commit()
```

## the full script

```python
import json
import sqlite3

conn = sqlite3.connect('rosterdb.sqlite')
cur = conn.cursor()

# Do some setup
cur.executescript('''
DROP TABLE IF EXISTS User;
DROP TABLE IF EXISTS Member;
DROP TABLE IF EXISTS Course;

CREATE TABLE User (
    id     INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT UNIQUE,
    name   TEXT UNIQUE
);

CREATE TABLE Course (
    id     INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT UNIQUE,
    title  TEXT UNIQUE
);

CREATE TABLE Member (
    user_id     INTEGER,
    course_id   INTEGER,
    role        INTEGER,
    PRIMARY KEY (user_id, course_id)
)
''')

fname = input('Enter file name: ')
if len(fname) < 1:
    fname = 'roster_data_sample.json'

# [
#   [ "Charley", "si110", 1 ],
#   [ "Mea", "si110", 0 ],

str_data = open(fname).read()
json_data = json.loads(str_data)
print(type(json_data))

for entry in json_data:

    name = entry[0]
    title = entry[1]
    role = entry[2]

    print((name, title, role))

    cur.execute('''INSERT OR IGNORE INTO User (name)
        VALUES ( ? )''', ( name, ) )
    cur.execute('SELECT id FROM User WHERE name = ? ', (name, ))
    user_id = cur.fetchone()[0]

    cur.execute('''INSERT OR IGNORE INTO Course (title)
        VALUES ( ? )''', ( title, ) )
    cur.execute('SELECT id FROM Course WHERE title = ? ', (title, ))
    course_id = cur.fetchone()[0]

    cur.execute('''INSERT OR REPLACE INTO Member
        (user_id, course_id, role) VALUES ( ?, ?, ? )''',
        ( user_id, course_id, role ) )

    conn.commit()
```

and an example of the JSON file

```JSON
[
  [
    "Alekzander",
    "si110",
    1
  ],
  [
    "Tione",
    "si110",
    0
  ],
  [
    "Samy",
    "si110",
    0
  ],
  [
    "Alicia",
    "si110",
    0
  ],
  [
    "Kruz",
    "si110",
    0
  ],
  [
    "Dillan",
    "si110",
    0
  ],
  [
    "Badr",
    "si110",
    0
  ],
  [
    "Murry",
    "si110",
    0
  ],
  [
    "Ruslan",
    "si110",
    0
  ],
  [
    "Aliesha",
    "si110",
    0
  ],
  [
    "Gracielynn",
    "si110",
    0
  ],
  [
    "Markus",
    "si110",
    0
  ]
 ]
```