## Database Setup

By default Django use SQLite as a database, this will be created when is need it so if we are not going to use any other database we wont need to do anything.

Now to see the configuration lets for to **mysite/settings.py**, here we will have several configuration, one for those configuration is about the databases.


![001_database_settings](images/001_database_settings.png)


To change to other database we will need to change the key in **DATABASES 'default'** to match the setting of the other database:

* **ENGINE:** the default will be `django.db.backends.sqlite3` but we have `djando.db.backends.postgresql`,`django.db.backends.mysql` or `django.db.backends.oracle` 
* **NAME:** this is the name of the database, in the case of the SQLite this will be a file, and the **NAME** should be the absolute path to the file `os.path.join