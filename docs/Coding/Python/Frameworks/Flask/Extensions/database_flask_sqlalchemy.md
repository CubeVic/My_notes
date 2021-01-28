![flask-sqlalchemy-logo.png](images/flask-sqlalchemy-logo.png){: .center}
![flask-sqlalchemy-title.png](images/flask-sqlalchemy-title.png){: .center}

Flask-SQLAlchemy is a wrapper for SQLALChemy, SQLALchemy is a ORM or Object Relational Mapper, this allow the application to manage the database using high level objects such as classes, objects and methods instead of tables and SQL, in other words ORM translate high-level operations in database commands.

1. [Official documentation:](https://flask-sqlalchemy.palletsprojects.com/en/2.x/quickstart/)
2. [PIP page:](https://pypi.org/project/Flask-SQLAlchemy/)

Flask-SQLAlchemy support different databases, relational an no-n relational, we can use a simple database such as SQLite for prototyping and development and once deploy we can switch to a more complex database without the need to change much parts for the code.

### Installation
```bash
pip install flask-sqlalchemy
```

## Database migration 

The author of mega-tutorial make a good point, not all tutorial cover migration of a database, this is important since the relational databases are base in structures data so if data change the database need to change and we will need to make the migration of the data that already exist, so there is where the author introduce a library write by himself called [`Flask-migrate`](https://github.com/miguelgrinberg/flask-migrate) which is a wrapper for [`Alembic`](https://github.com/sqlalchemy/alembic).

### Installation
```bash
pip install flask-migrate
```

## `Flask-SQLAlchemy` Configuration

I will continue using the example of the microblog use in the form extension notes, and we are going to use the SQLite database.

We are going to add two new configuration to the config file

**config.py**
```python 
import os

#1. new configuration
basedir = or.path.abspath(os.path.dirname(__file__))

class Config(object):
	"""COnfiguration class"""
	SECRET_KEY = os.environ.get('SECRET_KEY') or "secretKey"

	#2. New configuration
	SQLALCHEMY_DATABASE_URL = os.environ.get('DATABASE_URL') or 'sqlite:///' + os.path.join(basedir,'app.db')
	SQLALCHEMY_TRACK_MODIFICATIONS = False

``` 

so from the previous code

1. the definition of `basedir`  I just define a base directory.
2. SLQAlchemy take the location of the database from the configuration variable `SQLALCHEMY_DATABASE_UR`  as we mentioned in the notes for forms, it is a good practice store the configuration variable in the environment variable, and provide a fall-back in case of failure 

## Database Models

## Creating The Migration Repository

## The First Database Migration

## Database Upgrade and Downgrade Workflow

## Database Relationships

## Play Time

## Shell Context  