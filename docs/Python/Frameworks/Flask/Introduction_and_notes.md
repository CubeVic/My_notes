#Flask
![Flask logo](images/flask.png){: .center}

>Flask is a micro web framework written in Python. It is classified as a microframework because it does not require particular tools or libraries.

1. [Pypi page](https://pypi.org/project/Flask/)
2. [Documentation](https://flask.palletsprojects.com/en/1.1.x/)

## Index

I have several notes in this case, the first notes are from a youtube video and explain how to make a small application that use SQLite as database and Heroku for "live deployment", be aware that the app still use the `DEBUG=True` in a really live app that should be set to `False`.

1. Quick & Dirty First App.
2. Official Flask tutorial.
2.1. Application Layout (Structure).
2.2. Application Factory.
2.3. Application Database.
2.4. Blueprints (part 01-Auth).
2.5. Templates.
2.6. Blueprints (part 02-Blog).

## Extra notes

### Nuggets for Template Jinja2

* `{% include %}` it is used to add to the current template, in some cases are called partial, this is to further separate the templates, it is use to 'include' extra parts to the base or other templates.
* `{% extends 'html_file.html'%}`  it is similar to inheritance.
* `{{ super() }}` it is use in combination with `{% extends %}` and inside `{% Block %}` part of a child template this will tell jinja2 to render the content of the block and keeping the content of the original parent template's block.

### Common plug-ins

<aside>
* **Flask-SQLAlchemy**:  For database interaction
* **Flask-Session**:  User sessions management
* **Flask-login**: Management user login
* **Flask-WTF**: To handle forms
</aside>
#### Common configuration variables

???important "General"
     * FLASK_ENV
     * DEBUG
     * TESTING
     * SECRET_KEY
     * SERVER_NAME

???important "Flask SQLAlchemy"
     * SQLALCHEMY_DATABASE_URI
     * SQLALCHEMY_ECHO
     * SQLALCHEMY_ENGINE_OPTIONS

???important "Flask Session"
     * SESSION_TYPE
     * SESSION_PERMANENT
     * SESSION_KEY_PREFIX
     * SESSION_REDIS
     * SESSION_MEMCHED
     * SESSION_MONGODB
     * SESSION_SQLALCHEMY

???important "Flask WTF"
     * WTF_CSRF_ENABLED ==> Set `False` to disable CSRF security

### *I learned from experience*

???success "About Cache and potential effects"
    **If CSS is not reflected try clean the cache of the browser.**
    I was struggling in a project, I made changes on the CSS and didn't see those reflected in the browser, I check the code and the redo the whole thing.
    *Solution*: Clean the cache of the browser.
