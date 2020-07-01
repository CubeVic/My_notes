#SQLAlchemy

the website describe it as the Python SQL toolkit and Object Relational Mapper
Although the description is deeper and for sure I'm been shallow in my description, **SQLAlchemy** abstract all the code necessary to interact with the database, and do it in a way that make it easy to change databases, example the development can be done in `sqlite` and production can be in `PostgreSQL` and the changes will be minimum.  

[SQLAlchemy docs 1.3](https://docs.sqlalchemy.org/en/13/)

## Installation 

The installation is no different than other libraries.

```
pip install sqlalchemy
```

> using VScode and pylint I ran into some issue where pylint report the `from sqlalchemy ....` as an error, to solve it i modify some setting in the settings.json of the work space in VScode, it was based in an answer on stackoverflow but since them i lost the link to it.

## Connecting to the database

(Not totally accurate but is just a reference) for the connection with the bases in python normally i will need to create a connection later a cursor, needless to say the set up of the engine, all of this might , emphasis in MIGHT, be different depending of the DB that we will use. In SQLAlchemy it will be a bit more simple 

```python 
import sqlalchemy as db
engine = db.create_engine('dialect+driver://user:pass@host:port/db')
``` 

what is inside the `create_engine()` is what will vary depending of the database, here some information from the official docs engine configuration](https://docs.sqlalchemy.org/en/13/core/engines.html#postgresql)

for now, we will use `sqlite`

```python 
 import sqlalchemy as db
 engine = db.create_engine('sqlite///mydb.sqlite')
```

the `///` meas relative path, `////` means full path, in most of the cases a relative path will do.

## Viewing Table Details

there is something mentioned in several tutorials, that i don't see the use yet, but that i will use here, it is the creation on a table using *reflection*. Reflection is the process of create metadata by reading the database

here we will use a example from a [medium article](https://medium.com/hacking-datascience/sqlalchemy-python-tutorial-abcc2ec77b57)

> I use the medium article's structure because I think is easy to follow and will be easy to find a specific thing in the future 

```python 
import sqlalchemy as db

engine = db.create_engine('sqlite:///census.sqlite')
connection = engine.connect()
metadata = db.MetaData()
census = db.Table('census', metadata, autoload=True, autoload_with=engine)
print(census.columns.keys())
#['state', 'sex', 'age', 'pop2000', 'pop2008']
print(repr(metadata.tables['census']))
"""
Table('census', 
	MetaData(bind=None), 
	Column('state', VARCHAR(length=30), table=<census>), 
	Column('sex', VARCHAR(length=1), table=<census>), 
	Column('age', INTEGER(), table=<census>), 
	Column('pop2000', INTEGER(), table=<census>), 
	Column('pop2008', INTEGER(), table=<census>), schema=None)
"""
```