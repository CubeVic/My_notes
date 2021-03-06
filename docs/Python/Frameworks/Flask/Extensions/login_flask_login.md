![flask-login.png](images/flask_login_logo.png){: .center}

Flask-Login is Flask extension that provide user session management to flask app, it handle the most common task related with the login procedure, task such as Logging in, Logging out, Remember sessions (permanent of by a define amount of time).  

1. [Official documentation:](https://flask-login.readthedocs.io/en/latest/)
2. [PIP page:](https://pypi.org/project/Flask-Login/)
3. [Git:](https://github.com/maxcountryman/flask-login)

From the official documentation of Flask-Login: 

* Store the active user’s ID in the session, and let you log them in and out easily.
* Let you restrict views to logged-in (or logged-out) users.
* Handle the normally-tricky “remember me” functionality.
* Help protect your users’ sessions from being stolen by cookie thieves.
* Possibly integrate with Flask-Principal or other authorization extensions later on.

### Installation
```bash
pip install Flask-Login
```
## Password Hashing

Flask Has a dependency that can handle the hashing of passwords, this dependency is called [Werkzeug](https://werkzeug.palletsprojects.com/en/1.0.x/), this is an example of a password hash using `generate_password_hash()`

![Werkseug](images/flask_login_001.png){: .center}

Now to verify the hashed password we can use the function `check_password_hash()`

![Werkseug](images/flask_login_002.png){: .center}

In this case the `check_password_hash()` will return `True` if the hash password matches, and `False` when they don't matches.

### Password hashing and verification

The whole password hashing logic can be implemented as two new methods in the user model

**app/models.py**
```python
from werkzeug.security import generate_password_hash, check_password_hash

#...

class User(db.Model):
	#...

	def set_password(self, password):
		self.password_hash = generate_password_hash(password)

	def check_password(self, password):
		return check_password_hash(self.password_hash, password)
```

we can check if this is working with the flask shell

![Werkseug](images/flask_login_003.png){: .center}

## Introduction to Flask-login

Flask-login help us to handle the logged-in state, in other words "remembers" the state, so the user can navigate the site and maintain the session state.

As other Flask extensions we need to register it, for that we need to modify the `__init__.py`

**application/__init__.py**
```python

#...

from flask_login import LoginManager

app = Flask(__name__)

#...
login = LoginManager(app)

```

## Preparing The User Model for Flask-login

Flask-login extension work with any model and multiple databases the only requirements is the implementation of four items:

* `is_autheticated`:  Property is `True` if the user is valid, `false` if is not.    
* `is_active`: Property is `True` if the user is active and `False` otherwise.  
* `is_anonymous`: Property is `False` if the user is a regular user, `True` if is special anonymous user.  
* `get_id()`: it returned a unique identifier for the user as a string.


Although Flask-login provided a *mixin* class called `UserMixin` that include the generic implementation that are appropriate for most user model classes.

**application/models.py**
```python
#...

from flask_login import UserMixin

class User(UserMixin, db.Model):
	#...
```

## User Loader Function

This extension track the logged user by storing the user identifier  in a Flask's user sessions, each time the logged-in user navigate to a new page, the extension retries the Id of the user from the session, and the loads the user into memory.

Flask-Login need some help to load the user, in that case we need to create a new function.

**application/models.py**
```python
from application import login

# ...

@login.user_loader
def load_user(id):
	return User.query.get(int(id))
```

Now, we need to register the **User loader** to the extension, in this case we register the **user loader** to the Flask-login with the decorator `@login.user_loader`, if we check in detail, there is a cast from string to Integer, that is because the ID of the user Flask-login pass is a string

## Logging User In

## Logging Users Out

## Requiring User To Login

## Showing The Logged In User in Templates

## User Registration



