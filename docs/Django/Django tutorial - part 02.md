## Database Setup

By default Django use SQLite as a database, this will be created when is need it so if we are not going to use any other database we wont need to do anything.

Now to see the configuration lets for to **mysite/settings.py**, here we will have several configuration, one for those configuration is about the databases.


![001_database_settings](images/001_database_settings.png)


To change to other database we will need to change the key in **DATABASES 'default'** to match the setting of the other database:

* **ENGINE:** the default will be `django.db.backends.sqlite3` but we have `djando.db.backends.postgresql`,`django.db.backends.mysql` or `django.db.backends.oracle` 
* **NAME:** this is the name of the database, in the case of the SQLite this will be a file, and the **NAME** should be the absolute path to the file `os.path.join(BASE_DIR,'db.sqlite3')`

### Installed Apps

In the same document we have the `INSTALLED_APPS` here Django holds the names of all Django applications that are activated in this Django instance. This apps can be reuse in more projects.

* `django.contrib.admin` admin site 
* `django.contrib.auth` an authentication system
* `django.contrib.contenttypes` a framework for content types
* `django.contrib.sessions` A sessions framework
* `django.contrib.messages` A messaging framework
* `django.contrib.staticfiles` A framework for managing static files

![002_Installed_apps](images/002_Installed_apps.png)

some of this apps make use of database tables, therefore we need to create the table for them, this can be done with: 

```
python manage.py migrate
```

the **migrate** command looks at the **INSTALLED_APPS** settings and create any necessary database table according to the database settings in the file *mysite/settings.py*

## Creating models

the models are the database layout, with additional metadata, using the example of the polls, we are going to create two models: **Questions** and **Choice**, **Question** will contain two fields *questions* and *publication date*. A **Choice** has two fields: the *text of the choice* and the *votes*, each choice is linked to a question.

all of this concept will be implement in a Python class, in the `polls/models.py` we have:

```python
from django.db import models

class Question(models.Model):
	question_text = models.CharField(max_length=200)
	pub_date = models.DataTimeField('date published')

class Choice(models.Model):
	question = model.ForeignKey(Question, on_delete+models.CASCADE)
	choice_text = models.CharField(max_length=200)
	votes = models.IntegerField(default=0)
```

Each model is represented by a class that subclass `django.db.models.Model` each model has a number of class variables, each of which represent a database field in the model.

Each field is represented by and instance for the Field class, for example `CharField` for characters fields and **DateTimeField** for datetimes, this tells Django what type of data each fields holds.

There is something to remark, in this case each field have two names,  one machine-friendly format, like **question_text** or **pub_date** and a human-friendly or human-readable, in this case `Question.pub_date` is the only one with this human-readable name (date published).

Some **Field** classes have required arguments, for example **CharField** that required **max_length** and others can use **default** to set the *default* value, like `Choice.votes`

Finally the relationship between both models is done using **ForeignKey**, that tells Django each **Choice** is related to a single **Question**, Django support the common database relationships; many-to-one, many-to-many and one-to-one.

