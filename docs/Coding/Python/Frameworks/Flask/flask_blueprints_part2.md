In this part of the notes we will focus in the blueprint that will handle the Blog part of the application.

##The Blueprint

First we need to create the blue print **flaskr/blog.py** and later register it to the application factory.

**flaskr/blog.py**
```python 
from flask import (Blueprint, flash, g, redirect, render_template, request, url_for)
from werkzeug.exceptions import abort
from flaskr.auth import login_required
from flaskr.db import get_db

bp = Blueprint('blog', __name__)
``` 
now using `app.register_blueprint()` on **flaskr/__init__.py** to import and register the new blueprint

```python 
def create_app():
    app = ...
    # existing code omitted

    from . import blog
    app.register_blueprint(blog.bp)
    app.add_url_rule('/', endpoint='index')

    return app
``` 

Couple difference with the `auth` blueprint, the `blog` blueprint doesn't have the `url_prefix` so in this case the index will be add `/` and create at `/create`.

now we use the `add_url_rule` to define the endpoint for the index, so the URL create with `url_for('index')` or `url_for('blog.index')` will both work and they will generate `/` URL.

> it sound or read complicated, but basically with the `add_url_rule` I'm making sure that i will generate the correct URL every-time i decided to call the endpoint index, either using `url_for('index')` or `url_for('blog.index')`

### Index

The index will be the view were we can see all the post, therefore we will use a SQL `JOIN` with the user table to get back all the information from the database.

**flaskr/blog.py**
```python 
@bp.route('/')
def index():
    db = get_db()
    posts = db.execute(
        'SELECT p.id, title, body, created, author_id, username'
        ' FROM post p JOIN user u ON p.author_id = u.id'
        ' ORDER BY created DESC'
    ).fetchall()
    return render_template('blog/index.html', posts=posts)
``` 
now the template will be as follow: 

```HTML
{% extends 'base.html' %}

{% block header %}
  <h1>{% block title %}Posts{% endblock %}</h1>
  {% if g.user %}
    <a class="action" href="{{ url_for('blog.create') }}">New</a>
  {% endif %}
{% endblock %}

{% block content %}
  {% for post in posts %}
    <article class="post">
      <header>
        <div>
          <h1>{{ post['title'] }}</h1>
          <div class="about">by {{ post['username'] }} on {{ post['created'].strftime('%Y-%m-%d') }}</div>
        </div>
        {% if g.user['id'] == post['author_id'] %}
          <a class="action" href="{{ url_for('blog.update', id=post['id']) }}">Edit</a>
        {% endif %}
      </header>
      <p class="body">{{ post['body'] }}</p>
    </article>
    {% if not loop.last %}
      <hr>
    {% endif %}
  {% endfor %}
{% endblock %}
```

There some point to be aware off in this template:

1. if the user is loggin in we display `create` as title.
2. if the user if the user is the author of the post they will say "Edit"
3. we use a special Jinja loop `loop.last` so if the post is the last one it wont have the line that separate each post visually.

### Create
### Update
### Delete
