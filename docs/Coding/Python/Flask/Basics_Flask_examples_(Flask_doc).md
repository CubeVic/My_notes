In this notes I will use the example on the official documentation to learn how to use it, in other notes in this same directory i might use other sources, but in this case i will use the [official documentation](https://flask.palletsprojects.com/en/1.1.x/)

Lets first get something out of the ways, the 99% of the examples and tutorials on the web use the basic hello world example of Flask and don't enter in details or good practice, that is the main reason to start with the Official documentation first in this learning path, here is the typical hello world on Flask

![Flask_Hello_World](images/Flask_hello_world_01.png){: .center}


## Application Layout

This layout might change depending of the size or the length of the application although i think this will suite most of the application I'm thinking to use Flask for.
Here I follow exactly the documentation

![Flask layout](images/Flask_layout_01.png)

> The tutorial assume that all the content will be in a folder called "Flask-tutorial" and a virtual environment was created 

the documentation suggest some to add an specific `.gitignore` that i thing came useful since will help me to avoid commit any unnecessary document or folder to git or any version control system 

#### `gitignore` Example

```
venv/

*.pyc
__pycache__/

instance/

.pytest_cache/
.coverage
htmlcov/

dist/
build/
*.egg-info/
```

## Application Factory

As shown on the `hello world!` code snippet, a typical Flask application is a instance of the **Flask** class, any configuration, URL or change will be done with the class ( or register with the class), this instance is a global instance.  
In this example, they took another approach, it seems to be a best practice, and a future prove implementation. They, instead of, a global instance, they will create a instance inside a function. This function is called **Application factory**, all configuration registration or set up will be done inside this function, and then application will be returned, in other words, the return of this `application factory` will be the application itself.

We will create a script called `__init__.py` that will serve as container of the **application Factory** and it tells Python to tread the current directory as a package ( in this case the directory is *flaskr*)

**flaskr/__init__.py**
```python 
import os

from flask import Flask

def create_app(test_config=None):
	""" Creates and configure the application, it is the application factory """

	app = Flask(__name__, instance_relative_config=True)
	app.config.from_mapping(
		SECRET_KEY='dev',
		DATABASE=os.path.join(app.instance_path, 'flaskr.sqlite'),
		)

	if test_config is None:
		""" load the instance config, if it exist, when not testing"""
		app.config.from_pyfile('config.py', silent=True)
	else: 
		""" load the testing config if passed in"""
		app.config.from_mapping(test_config)

	# Ensure the instance folder exist
	try: 
		os.makedirs(app.instance_path)
	except OSError:
		pass

	# a simple page that say hello
	@app.route('/hello')
	def hello():
		return ' Hello, world!'

	return app
``` 

#### `create_app()` the application factory

1. `app = Flask(__name__, instance_relative_config=True)` Create a Flask instance:
	*	`__name__` is the name of the current python module, it is a convince way to tell the app where it is located.
	*	`instance_relative_config`  a way to let the app knows the location of some configuration, this configuration are particular of this instance and are not committed to the version control, this configuration are store on [Instance folder](https://flask.palletsprojects.com/en/1.1.x/config/#instance-folders) this folder is located outside the directory `flaskr`
2. `app_config.from_mapping()` set some default configuration that the app will use: 
	*	`SECRET_KEY` it is use by Flask to keep the application safe, in a development stage the value is 'dev' but in production must be replace for a random string.
	*	`DATABASE` it is the path to the instance folder where the SQLite database is store.  
3. `app.config.from_pyfile()` It overwrite the configuration or default configuration, the values are taken from a file called `config.py` file in the instance folder if it exist. the production `SECRET_KEY` can be store here.
	*	`test_config` can be also past to this factory, and it will be use instead of the instance configuration.
4. `os.makedirs()` It ensure the `app.instance_path` exist, Flask doesn’t create the instance folder automatically, but it needs to be created because your project will create the SQLite database file there.
5. `@app.route()` Create the route the the function that will give back the webpage  

## Run the application

We are going to lunch the app in development mode, in this way the browser will be refresh and server restarted after any change in the code.
You should be in the top-level not inside the folder **flaskr**

#### For linux and Mac:
```
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```
#### For Windows:
```
set FLASK_APP=flaskr
set FLASK_ENV=development
flask run
```

Run this in the terminal or CMD and we will get a message like
![Flask running](images/Flask_running.png){: .center}

## Regarding the Database and the connection.

For this example the Flask tutorial use the SQLite, since it is already integrated with python.
As it is mentioned in the tutorial, the first thing we need to do when working with databases is to establish a connection, any operation or query to the DB is done through this connections, this connections must be close once the operation is finished.

**flaskr/db.py**
```python 
import sqlite3

import click
from flask import current_app, g
from flask.cli import with_appcontext

def get_db():
	if 'db' not in g:
		g.db = sqlite3.connect(
            current_app.config['DATABASE'],
            detect_types=sqlite3.PARSE_DECLTYPES
        )
		g.db.row_factory = sqlite3.Row

		return g.db

def close_db(e=None):
	db = g.pop('db', None)

	if db is not None:
		db.close()

``` 

There are couple objects that still i don't fully understand but that make the development easier, or with better practice ( according with documentation), this are `g` and `current_app`, here some description ( and links) of this code snippet

1. [`g`](https://flask.palletsprojects.com/en/1.1.x/api/#flask.g)[^1]: it is an special object that is unique for each request, use to store data that might be user accessed by multiple function during the request. In this case the connection is stored and reused instead of creating a new one, if the get_db is use a second time at in the same request.

2. [`current_app`](https://flask.palletsprojects.com/en/1.1.x/api/#flask.current_app)[^2]:  Another special object, it points to the Flask application handling request, if we develop like this example we will be using the **application factory**, thus, we wont have an application object we writing the rest of the code, *"the `get_db()` will be call when the application is create and is handling a request, so current_app can be used."*

3. `sqlite3.connect()` establish a connection to the file pointed at by the `DATABASE` configuration key. at the beginning the file wont exist we need to initialize the database (I will explain it bellow)

4. `sqlite.Row` tells the connection to return rows that behave like `dicts`. This allows accessing the columns by name.  

### Creating the tables

In this case the initial table will be store in a file `.sql`

flaskr/schema.sql
```SQL
DROP TABLE IF EXIST user;
DROP TABLE IF EXIST post;

CREATE TABLE user (
	id INTEGER PRIMARY KEY AUTOINCREMENT,
	username TEXT UNIQUE NOT NULL
	password TEXT NOT NULL
);

CREATE TABLE post (
	id INTEGER PRIMARY KEY AUTOINCREMENT,
	author_id INTEGER NOT NULL, 
	created TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
	title TEXT NOT NULL,
	body TEXT NOT NULL,
	FOREIGN KEY (author_id) REFERENCES user (id)
);
``` 
Now, The next step is create the logic to initialize the database, this will be in different parts and two different files:

1. Create the functions to run the SQL statements, this will be done on **flask/db.py**
2. Register with the application, we need to let the application know that there is a database, create the initializer ( will include some CLI commands) **flaskr/db.py**, and later the logic to import it to the application factory **flaskr/__init__.py**.

### Function to run the SQL commands

code to add:
**flaskr/db.py**
```python 
def init_db():
	db = get_db()

	with current_app.open_resource('schema.sql') as f:
		db.executescript(f.read().decode('utf8'))

@click.command('init-db')
@with_appcontext
def init_db_command():
	""" clear the existing data and create new tables """
	init_db()
	click.echo('Initialized the database.')
``` 


so the code until on **flaskr/db.py** will be: 
![Flask_db_001.png](images/Flask_db_001.png)

###Register the application 

Now the functions `close_db` and `init_db_command` are defined but they are not register to be use by the application, in other words, in order to use the functions we need to register them with the instance of the application, although, in this case we are using **application factory**, so, technically the applications doesn't exist yet, or the instance is not available, so in this case we will need a function that make the registration for us and later we will import that function on the factory.

> We create a function on **flaskr/db.py** later import that function on **flask/__init__.py** in the factory function `create_app()`

**flaskr/db.py**
```python 
def init_app(app):
	app.teardown_appcontext(close_db)
	app.cli.add_command(init_db_command)
```   
1. `app.teardown_appcontext()` this function is executed after returning the response, during the clean up process, and basically allow me to run a function in that moment, in that case `close_db()`
2. `app.cli.add_command()` add a new command that can be call with the **flask** command.  

so the **flaskr/db.py** will be
![Flask_db_002.png](images/Flask_db_002.png)

Now we need to call the function `init_app()` from the factory

**flaskr/__init__.py**
```python 
def create_app():
	app = ...
	#existing code

	from . import db
	db.init_app(app)

	return app
``` 
so the Factory function will look like this: 

![application_factory_001.png](images/application_factory_001.png)

### Initialize the database

We create the Flask commands, we register those commands and import it to the factory, so now we can initialize the database using `flask`

on the Command (CMD) or terminal 
```bash
flask init-db
# --> Initialized the database
```

There now on the **instance** folder we will have a file **flask.sqlite**

## Blueprints and Views

With the Blueprints[^3], we can organize a group of related views and other part of the code, this views and code are not register to the Application, instead the are register to the Blueprint, then the blueprint is registered with the application when it is available in the factory function.

In this example I will use the same two blue prints use in the documentation example, one for the authentication functions and other for the blog posts itself. These blueprints are going to be in two separate modules.

### Creating a Blueprint

Authentication go first:

**flaskr/auth.py**
```python 
import functools

from flask import ( 
	Blueprint, flask, g, render_template, request, sessions, url_for
)
from werkzeug.security import check_password_hash, generate_password_hash
from flaskr.db import get_db

bp = Blueprint('auth', __name__, url_prefix='/auth')
``` 

1. We create a blueprint called `auth`.
2. we provide a location for the blueprint `__name__`.
3. `url_prefix` will be prepended to all the URL associated with the blueprint.

Now we need to import and register from the factory 

**flaskr/__init__.py**
```python 
def create_app():
	app = ...
	# existing code

	from . import auth
	app.register_blueprint(auth.bp)

	return app
``` 

1. `app.register_blueprint()` use to register the blueprint with the application

### Views (auth module)

Now we need to do the views, these views will have to parts, the templates ( the jinja2 templates) and the functions binded to them.

#### Register View

This view will take care of the registration of a new user, so any user visiting `/auth/register` URL will receive a HTML as a response, this response will be deliver by the `register` view.

**flaskr/auth.py**
```python 
@bp.route('/register', methods=('GET','POST'))
def register():
	""" this is the register view"""
	if request.method == 'POST':
		username = request.form['username']
		password = request.form['password']
		db = get_db()
		error = None

		if not username:
			error = 'Username is required.'
		elif not password:
			error = 'password is required.'
		elif db.execute(
				'SELECT id FROM user WHERE user = ?',(username,)
			).fetchone() is not None:
				error = 'User {} is already register.'.format(username)

		if error is None:
			db.execute(
				'INSERT INTO user (user, password) VALUES (?, ?)',
				(username, generate_password_hash(password))
			)
			db.commit()
			return redirect(url_for('auth.login'))
		
		flash(error)

	return render_template('auth/register.html')
``` 
Now a description of the code:

1. `@bp.route` this is a decorator that associate the URL `/register` with the register view function, so if flash receives a request to `/auth/register`, it will call `register` and return a value as response.  

2. We check if the request was made by `POST`, if yes, we validate the input.

3. `request.form` it is a special `dict` it will store the key and values of the information submitted on a html form, in this case username and password. Validate if the username and password are not empty.  

4. Validate `username` doesnt exist already on the database, `fetchone()` give back the first row in the result, if thre are not result it return `None`.

5. Password shouldnt be store in plain text on the database, instead we use `generate_password_hash()` to hash the password and store the hash, after this modification we commit to the database `db.commit()`

6. After commit to the database the user is redirect to the login page.  

7. If there is any error `flash()` stores messages that can be retrieved when rendering the template.  

8. When the user initially navigates to `auth/register`, or there was a validation error, an HTML page with the registration form should be shown. `render_template()` will render a template containing the HTML.  


#### Login View

Following similar pattern of `register` view here the login view:

**flaskr/auth.py**
```python 
@bp.route('/login', methods=('GET', 'POST'))
def login():
	if request.method == 'POST':
		username = request.form['username']
		password = request.form['password']
		db = get_db()
		user = db.execute(
				'SELECT * FROM user WHERE username = ?' (username,)
			).fetchone()

		if user is None:
			error = 'Incorrect username.'
		elif not check_password_hash(user['password'], password):
			error = 'Incorrect password.'

		if error is None:
			session.clear()
			session['user_id'] = user['id']
			return redirect(url_for('index'))

``` 




[^1]: `g` is a namespace object that can store data during an [application context](https://flask.palletsprojects.com/en/1.1.x/appcontext/), this is a [proxy](https://flask.palletsprojects.com/en/1.1.x/reqcontext/#notes-on-proxies) 

[^2]: `current_app` A proxy to the application handling the current request. This is useful to access the application without needing to import it, or if it can’t be imported, such as when using the application factory pattern or in blueprints and extensions.

[^3]: A blueprint is an object that allows defining application functions without requiring an application object ahead of time. It uses the same decorators as Flask, but defers the need for an application by recording them for later registration