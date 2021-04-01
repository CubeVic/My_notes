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

With the database in place, with the *user loader* done and with the modification in the User model we can make a modification of the view function handling the login.

**application/routes.py**
```python
#...

from flask_login import current_user, login_user
from application.models import User

#...

@app.route('/login', methods=['GET','POST'])
def login():
	if current_user.is_authenticated:
		return redirect(url_for('index'))
	form = LoginForm()
	if form.validate_on_submit():
		user = User.query.filter_by(username=form.username.date).first()
		if user is None or not user.check_password(form.password.data):
			flash('Invalid username or password')
			return redirect(url_for('login'))
		login_user(user, remember=form.remember_me.data)
		return redirect(url_for('index'))
	return render_template('login.html', title='Sign In', form=form)

```

From the previous code we have:

1. The first two lines have two important items, the first `current_user` this variable contain the user, and the parameter `is_authenticated`, if the user is already log in the parameter `is_authenticated` will be `True`, and them the user is redirect to the index.
2. we get back the user from the database if hte user is not already log in, in this case we use the `query.filter_by` and the method `first()` to filter the records by user name and get back the first record found.
3. Now we verify the password, in this case we need to remember that the password is hash so we use the method `check_password()`, the there is no match we will use the `flash()` method to display the error and redirect to login page.
4. if the user and password are correct, we call the method `login_user()`, this function comes from Flask-login, this function will register the user as logged in, so that means that any future pages the user navigates will the variable `current_user` set to that user.
5. last step is to redirect the newly logged user to the index page.

## Logging Users Out

We can use the `logout_user()` to complete the log out process

**application/routes.py**
```python 
# ...

from flask_login import logout_user

# ...

@app.route('/logout')
def logout():
	logout_user()
	return redirect(url_for('index'))
```

Now, we need to expose the link to the user, we ned to switch the login link in the navigation bar to logout if the user is log in.

### Modification to the Templates 

**application/templates/base.html**
```HTML
    <div>
        Microblog:
        <a href={{ url_for(endpoint='index') }}>Home</a>
        {% if current_user.is_anonymous %}
        <a href={{ url_for(endpoint='login') }}>Login</a>
        {% else %}
        <a href={{ url_for(endpoint='logout' }}>Logout</a>
        {% endif %}
    </div>
```

From the class `UserMixin` we have access to the property `is_anonymous`. The `current_user.is_anonymous` expression is going to be True only when the user is not logged in.

## Requiring User To Login

With some of the features of Flask-login we can "force" the user to login before they can view certain pages of the application, if a user who is not logged in tries to view a protected page Flask-Login will automatically redirect the user to the login form, and only redirect back to the page the user wanted to view after the login process is complete.

To implement this function  we will need to tel flask-login which is the view function handling the login.

**application/__init__.py**
```python
#...
login = LoginManager(app)
login.login_view = 'login'
```
the `'login'` value in the code above  is the name of the login view, the same we use in `url_for()`.

Now the way Flask-Login protect a view function against anonymous users is with the decorator `@login_required`, this decorator is added to the view function bellow `@app.route`, a function with this decorator becomes protected and will not allow access to a not authenticated.

**application/routes.py**
```python
from flask_login import login_requered

@app.route('/')
@app.route('/index')
@login_required
def index():
	#...
```

The `@login_required` will intercept the request and respond with a redirect to `/login`, but it will add a query string argument to this URL, the complete URL will be like `/login?next=/index`. The `next` query string argument is set to the original URL, so the application can use  that to redirect back after login.

Now we need to read and process the `next` query string argument:

**Application/routes.py**
```python
from flask import request
from werkzeug.urls import url_parse

@app.route('/login'. methods=['GET','POST'])
def login():
	#...
	if form.validate_on_submit():
		user = User.query.filter_by(username=form.username.data).first()
		if user is None or not user.check_password(form.password.data):
			flash('Invalid username or password')
			return redirect(url_for(endpoint='login'))
		login_user(user, remember=form.remember_me.data)
		next_page = request.args.get('next')
		if not next_page or url_parse(next_page).netloc !='':
			next_page = url_for(endpoint='index')
		return redirect(next_page)
	return render_template('login.html', title='Sign In', form=form)
```
once the user is login and the function `login_user()` is used, the value of the `next` string query argument is obtained. The variable `request` come from flask and it store all the information the client sent with the request. From this variable we can check the attribute `arg` as `request.arg` this attribute contain all the content of the query string, this information is format as a dictionary thus the use of `get('next')` to get back the page to be redirected to.

Now we need to give a bit more explanation to the statement `if not next_page or url_parse(next_page).netloc != ''`. Consider the possibilities of the redirection after a successful login:

1. The URL doesn't contain a `next` argument, in that case we redirect the user to the index page.  
2. The URL include a `next` argument, this argument is a relative path (a URL without a domain part), the user is redirect to that URL.  
3. The URL include a `next` argument, however in this case the value is a full URL, the URL includes a domain name, in this case the use is redirected to the index page.  

The first two option are simple and predictable, but the third one is more a security measure, this is to prevent an attack where the next value will include a full URL to a malicious website. so the application only redirects when the URL is relative. To determine if the URL is relative or absolute, we use `url_parse()` from **Werkzeug** package and check if the `netloc` component is set or not.


## Showing The Logged In User in Templates

Now we modify the template to display the user name, this information will be extracted from the `current_user`

**application/template/index.html**
```html
{{% extends 'base.html' %}}

{% block content %}
	<h1>Hi, {{ current_user.username }}</h1>
	{% for post in posts %}
	<div><p>{{ post.author.username }} says: <b> {{ post.body }} </b></p></div>
	{% endfor %}

{% endblock %}

```

Now we can modify the view function

```python
@app.route('/')
@app.route('/index')
@login_required

def index():
	#...
	return render_template('index', title='Home Page', posts=posts)
```

we can use the `flask shell` to create a user and log in.
```
u = User(username='susan', email='susan@example.com')
u.set_password('cat')
db.session.add(u)
db.session.commit()
```

## User Registration


Now the last step is the creation of the registration form, for that we will start by the creation of a new class on the **forms.py**, this class will represent the registration form

### Registration form 
**application/forms.py**
```python
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField, BooleanField, SubmitField
from wtforms.validators import ValidationError, DataRequired, Email, EqualTo
from application.models import User

#...

class RegistrationForm(FlaskForm):
	username = StringField('Username', validators=[DataRequired()])
	email = String('Email', validator=[DataRequired(), Email()])
	password = passwordField('Password', validator=[DataRequired()])
	password_repeat = PasswordField('Repeat Password', validator=[DataRequired(), EqualTo('password')])
	submit = SubmitField('Register')


	def validate_username(self, username):
		user = User.query.filter_by(username=username.data).first()
		if user is not None:
			raise ValidationError('Please use a different user')


	def validate_email(seld, email):
		user = User.query.filter_by(email=email.data).first()
		if user is not None:
			raise ValidationError('Please use a different email')

```

Before running `Email()`, or added to the script, we will need to install a email-validator, this is a external dependency required by WTForms, we do this with:

```
pip install email-validator
```

From the previous code we have: 

1. there are two fields for the password, the idea is to use the second field as a verification, or a "repeat password".
2. the second field has an extra validator, this time `EqualTo()` and the argument of this method will be the name of the the first field.
3. there are two new methods called `validate_username` and `validate_password`, this are following a WTForm pattern, WTForm will take any method that follow pattern `validate_<field_name>` as a custom validator, in this case these two validator will make sure that user and password are not in the database.  
4. the custom validators are going to use `ValidationError` to handle the errors, in this case the error will be if the user input a email or an user that is already in the database.

### Template for the registration form 

The last step will be create a template to display the registration form 

**application/templates/register.html**
```html
{% extends 'base.html' %}

{% Block content %}
	<h1>Registration form</h1>
	<form action="" method="post">
		{{ form.hidden_tag() }}
		<p>
			{{form.username.label}}
			<br>
			{{form.username(size=32) }}
			{% for errors in in form.username.errors %}
				<span style="color: red;"> [{{error}}]</span>
			{% endfor %}
		</p>

		<p>
			{{form.email.label}}
			<br>
			{{form.email(size=64) }}
			{% for errors in in form.email.errors %}
				<span style="color: red;"> [{{error}}]</span>
			{% endfor %}
		</p>

		<p>
			{{form.password.label}}
			<br>
			{{form.password(size=32) }}
			{% for errors in in form.password.errors %}
				<span style="color: red;"> [{{error}}]</span>
			{% endfor %}
		</p>

		<p>
			{{form.password_repeat.label}}
			<br>
			{{form.password_repeat(size=32) }}
			{% for errors in in form.password_repeat.errors %}
				<span style="color: red;"> [{{error}}]</span>
			{% endfor %}
		</p>

		<p> {{ form.submit() }} </p>
	</form>

{% endblock %}

```

now the login form must have a link that can take new users to the registration form. wee will add

**application/templates/login.html**
```html
<p>new user? <a href="{{url_for('register')}}"> Click here to register</a></p>
```

### View function for the registration

As last step we need to create the view function to connect the registration form to the system, in this case this view function will be in the `routes.py` file 

**application/routes.py**
```python
from application import db
from application.forms import RegistrationForm

# ...

@app.route('/register', methods=['GET', 'POST'])
def register():
	if current_user.is_authenticated:
		return redirect(url_for('index'))

	form =  RegistrationForm

	if form.validate_on_submit():
		user = User(username=form.username.data, email=form.email.data)
		user.set_password(form.password.data)
		db.session.add(user)
		db.session.commit()
		flash("User register successfully")
		return redirect(url_for('login'))
	return render_template('register.html', title='Registration', form=form)
```
































