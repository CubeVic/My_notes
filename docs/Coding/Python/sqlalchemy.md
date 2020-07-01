#SQLAlchemy

the website describe it as the Python SQL toolkit and Object Relational Mapper
Although the description is deeper and for sure I'm been shallow in my description, **SQLAlchemy** abstract all the code necessary to interact with the database, and do it in a way that make it easy to change databases, example the development can be done in `sqlite` and production can be in `PostgreSQL` and the changes will be minimum.  

[SQLAlchemy docs 1.3](https://docs.sqlalchemy.org/en/13/)

## SQLAlchemy Introduction

this library facilitate the communication between python and databases, the library use `Object Relational Mapper (ORM)`  tool to translate python classes into relational tables, and automatically convert functions calls to SQL statements. thanks to the SQLAlchemy boilerplate code handling task like database connection is abstracted away then the developer can focus in the business logic.

### Python DBAPI

The Python DataBase API or DBAPI was created to specify how Python modules that integrate with the database should expose their interface, i wont go in details about it, just because is a deeper topic and SQLAlchemy works as a facade to it, so common functions like `connect`, ` close` , `commit` and `rollback` are already defined on the library.

I will follow an [article](https://auth0.com/blog/sqlalchemy-orm-tutorial-for-python-developers/?utm_source=medium&utm_medium=sc&utm_campaign=sqlalchemy_python) that use the most popular PostgrSQL DBAPI implementation available (`psycopg`), again I wont go deeper into it.

## SQLAlchemy Engines

> we can install SQLAlchemy using pip.   
```python 
pip install sqlalchemy
```   

In SQLAlchemy to interact with the database we will  need to create an `Engine`. This "Engine" is use to  manage two crucial factors: **Pools** and **Dialects** ( see more details bellow) 

```Python
from sqlalchemy import create_engine
engine = create_engine('postgresql://usr:pass@localhost:5432/mydatabase')
```
from the previous code:

* `usr:pass` are the credentials for the `mydatabase` database.  
* `localhost` the host.  
* `5432` refers to the `port` in this case the default postgresql port.  

In this case the URI doesn't show the Dialect but most of the common databases and Dialect are integrated we can get more information in the [official documentation](https://docs.sqlalchemy.org/en/13/core/engines.html), as example (from the documentation):

```Python
# default
engine = create_engine('postgresql://scott:tiger@localhost/mydatabase')
# psycopg2
engine = create_engine('postgresql+psycopg2://scott:tiger@localhost/mydatabase')
# pg8000
engine = create_engine('postgresql+pg8000://scott:tiger@localhost/mydatabase')
```
I think in more of the case for the small applications the database use will be `sqlite`, SQLite is connects to local files, the URL format is slightly different. The *"file"* portion of the path is going to be the filename of the database. For a relative file path, this requires three slashes (four slashes for a specific one):

```Python
engine = create_engine('sqlite:///foo.db')
```

### SQLAlchemy Connection Polls

The connection pools is a implementation of the object pool pattern, this allow the re-usage of pre-initialized objects ready to use, instead of create new instances of create object that are frequently needed  ( like db connection) the program fetch an existing object from the pool, used it as desired and puts back when done.   

There are various implementation of the connection pool pattern in SQLAlchemy, as an example, when we create the Engine using `create_engine()` this function generate a `QueuePool`, the default configuration is a reasonable default, like maximum pool size of 5 connections.

The most common options with their description:  

* `pool_size`: Sets the number of connections that the pool will handle.
* `max_overflow`: Specifies how many exceeding connections ( relative to `pool_size`) the pool supports.
* `pool_recycle`: Configures the maximum age (in seconds) of connections in the pool.
* `pool_timeout`: Identifies how many seconds the program will wait before giving up on getting a connection from the pool.

and example of this concept will be:

```python 
engine = create_engine('postgresql://me@localhost/mydb', pool_size=20, max_overflow=0 )
```  

###  SQLAlchemy Dialects

SQLAchelmy serve as a facade that allow us to connect to different databases engines using the same API, the most of the database follow SQL (Structured Query Language) standard, but there are different variations, this is the reason of dialects.

* **Microsoft SQL**
```SQL
SELECT TOP 10* FROM people;
```

* **MySQL** 
```SQL
SELECT *FROM people LIMIT 10;
```

Therefore, to know precisely what query to issue, SQLALchemy needs to be aware of the type of the database that it is dealing with
