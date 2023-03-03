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

The `create` view and the `register` view work quite similarly, either the form is displayed, or it is validated for later post it.

Something to remark is the usage of the decorator `login_required` wrote before, this tells the flask that the user must be logged in to be able to see this post, otherwise must be redirected to the login page.

** flaskr/blog.py**
```python
@bp.route('/create', methods=('GET', 'POST'))
@login_required
def create():
    if request.method == 'POST':
        title = request.form['title']
        body = request.form['body']
        error = None

        if not title:
            error = 'Title is required.'

        if error is not None:
            flash(error)
        else:
            db = get_db()
            db.execute(
                'INSERT INTO post (title, body, author_id)'
                ' VALUES (?, ?, ?)',
                (title, body, g.user['id'])
            )
            db.commit()
            return redirect(url_for('blog.index'))

    return render_template('blog/create.html')
```

** flaskr/templates/blog/create.html **

```html
{% extends 'base.html' %}

{% block header %}
  <h1>{% block title %}New Post{% endblock %}</h1>
{% endblock %}

{% block content %}
  <form method="post">
    <label for="title">Title</label>
    <input name="title" id="title" value="{{ request.form['title'] }}" required>
    <label for="body">Body</label>
    <textarea name="body" id="body">{{ request.form['body'] }}</textarea>
    <input type="submit" value="Save">
  </form>
{% endblock %}
```

### Update
The Update and delete views have some similarities, therefore we can make something different. Both `update` and `delete` fetch the `post`  by `id`, so we can create the function to fetch the post and later reuse it in each view

#### Fetch post by id

** Flaskr/blog.py**
```python
def get_post(id, check_author=True):
    post = get_db().execute(
        'SELECT p.id, title, body, created, author_id, username'
        ' FROM post p JOIN user u ON p.author_id = u.id'
        ' WHERE p.id = ?',
        (id,)
    ).fetchone()

    if post is None:
        abort(404, "Post id {0} doesn't exist.".format(id))

    if check_author and post['author_id'] != g.user['id']:
        abort(403)

    return post
```

The `abort()` function will raise and exception that returns a HTTP status code, it take the code and additional message, if the message is not provided it will display some default message example:

* 404 "Not Found".
* 403 "Forbidden".
* 401 "Unauthorized".

Additionally the `check_author` argument is create it so we can look for the post without the check the author, this can be use in a view where a single post will be display but the author doesn't matter, since the user wont make a modification of that post.

**Flaskr/blog.py**
```python
@bp.route('/<int:id>/update', methods=('GET', 'POST'))
@login_required
def update(id):
    post = get_post(id)

    if request.method == 'POST':
        title = request.form['title']
        body = request.form['body']
        error = None

        if not title:
            error = 'Title is required.'

        if error is not None:
            flash(error)
        else:
            db = get_db()
            db.execute(
                'UPDATE post SET title = ?, body = ?'
                ' WHERE id = ?',
                (title, body, id)
            )
            db.commit()
            return redirect(url_for('blog.index'))

    return render_template('blog/update.html', post=post)
```
something to pay attention is the usage of the `id` argument in the raout, in this case we are using `<init: id>` in the route, which will translate to `/1/update`. To generate this URL we will need to use the id as well, so the `url_for()` will look like `url_for('blog.update', id=post['id'])`

```HTML
{% extends 'base.html' %}

{% block header %}
  <h1>{% block title %}Edit "{{ post['title'] }}"{% endblock %}</h1>
{% endblock %}

{% block content %}
  <form method="post">
    <label for="title">Title</label>
    <input name="title" id="title"
      value="{{ request.form['title'] or post['title'] }}" required>
    <label for="body">Body</label>
    <textarea name="body" id="body">{{ request.form['body'] or post['body'] }}</textarea>
    <input type="submit" value="Save">
  </form>
  <hr>
  <form action="{{ url_for('blog.delete', id=post['id']) }}" method="post">
    <input class="danger" type="submit" value="Delete" onclick="return confirm('Are you sure?');">
  </form>
{% endblock %}
```

The previous template will have 2 forms, the first with the first post to be edited (`/<id>/update`). The other form contain just only the button and species and action attribute that the post to the delete view instead.

The `{{ request.form['title'] or post['title']}}` is used to choose what data appears in the form.

### Delete

The `delete` view doesnt have its own template it will reuse the one use in `update`, now similar to the previous view, we need to pay attention to the route `/<id>/delete`.

```python
@bp.route('/<int:id>/delete', methods=('POST',))
@login_required
def delete(id):
    get_post(id)
    db = get_db()
    db.execute('DELETE FROM post WHERE id = ?', (id,))
    db.commit()
    return redirect(url_for('blog.index'))
```
