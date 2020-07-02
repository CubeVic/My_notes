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

## SQLALchemy ORM

**Object Relational Mapper**, is a specialization of the Data Mapper design pattern that addresses relational databases, Mappers are responsible for moving data between objects and a database while keeping them independent of each other.

for example to create `Product` class and an `Order` class to relate as many instance as needed from one class to another (many to many), but in a relational database , we will need three entities, one for products, another for orders, and the third one to relate (through foreign key) products and orders.

### SQLAlchemy Data Types

This library provide support for [the common data types](https://docs.sqlalchemy.org/en/13/core/type_basics.html#generic-types) found in relational databases, example, booleans, dates, times, string, and numeric values, SQLALchemy implements some [vendor-specific type](https://docs.sqlalchemy.org/en/13/core/type_basics.html#sql-standard-and-multiple-vendor-types) such as JSON.

```Python
class Product(Base):
	__tablename__ = 'product'
	id = Column(Integer, primary_key=True)
	title = Column('title', String(32))
	in_stock = Column('in_stock', Boolean)
	quantity  Column('quatity', Integer)
	price = Column('price', Numeric)
```

* The `__tablename__` property tells SQLAlchemy that rows of the products table must be mapped to this class.
* The `id`  property identifies that this is the `primary_key` in the table and it is an **Integer**.
* The `title` property indicate the a column in the table  and is a **String**.
* The `in_strock` property type **Boolean**.
* The `quantity` property type **Integer**.
* The `price` property type **Numeric**.

This type are different to the type we will see in a pure implementation or SQL but this is part of the abstraction, SQLALchemy will translate to the correct type depending of the dialect.

### SQLAlchemy Relationship Pattern

SQLAlchemy support 4 type of relationships: 

* One to Many.  
* Many to One.  
* One to One.  
* Many to Many.  

#### One to Many

One instance of a class can be associated with many instance of another class

```python 
class Article(Base):
	__tablename__ = 'articles'
	id = Column(Integer, primary_key=True)
	comments = relationship('Comment')

class Comment(Base):
	__tablename__ = 'comments'
	id = Column(Integer, Primary_key=True)
	article_id = Column(Integer, ForeignKey('article.id'))
``` 

#### Many to One

it is similar to the relationship describe about 


```python 
class Tire(Base):
	__tablename__ = 'tires'
	id = Column(Integer, primary_key=True)
	car_id = Column(Integer, ForeignKey('car.id'))
	car = relationship('Car')

class Car(Base):
	__tablename__ = 'cars'
	id = Column(Integer, primary_key=True)
```

#### One to One

```python 
class Person(Base):
	__tablename__ = 'people'
	id = Column(Integer, primary_key=True)
	mobile_phone = relationship('MobilePhone', uselist=False, back_populates="person" )

class MobilePhone(Base):
	__tablename__ = 'mobile_phones'
	id = Column(Integer, primary_key=True)
	person_id = Column(Integer, ForeignKey('people.id'))
	person = relationship("Person", back_populates="mobile_phone")
``` 

two new parameter in the `relationship` method:

* `uselist=False` Make SQLAlchemy understand that `mobile_phone` will hold only a single instance and not an array.
* `back_populates` instruct SQLAlchemy to populate the other side of the mapping.

#### Many to Many

```python 
student_classes_association = Table('students_classes', Base.metadata,
		Column('stundent_id', Integer, ForeignKey('student.id')),
		Column('class_id', Integer, ForeignKey('classes.id')) 
)

class Student(Base):
	__tablename__ = 'students'
	id = Column(Integer, primary_key=True)
	classes = relationship("Class", secondary=student_classes_association)

class Class(Base):
	__tablename__ = 'classes'
	id = Column(Integer, primary_key=True)
``` 

In this case a secondary table or a helper table must be created to persist the association between instances of `student` and instances of `Class`, to make SQLAlchemy aware of the helper table, we passed it in the `secondary` parameter of the `relationship` function.

### SQLAlchemy ORM Cascade

Sometimes wen we update one table we need to propagate those changes to the other related tables, these changes can be simple updates (cascade updates) or deletes ( cascade deletes). SQLAlchemy ORM enables developers to map cascade behavior when using `relationship()`  the most common cascade:

* `save-update`
* `delete`
* `delete-orphan`
* `merge`

>The default behavior of cascade is limited to cascades of the so-called save-update and merge settings. The typical “alternative” setting for cascade is to add the delete and delete-orphan options; these settings are appropriate for related objects which only exist as long as they are attached to their parent, and are otherwise deleted.


