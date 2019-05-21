The information in this page is taken from the Django documentation, in some case i will complement with tutorials (in first place with freecodecamp tutorial).

## Verify Django is installed and what Version are we using

to verify which version are we using we can use;

```
py -m django --version
```

## Creating a project

To create a project, first, we need to navigate to the location where we want to store the project, we can use *cd* to do so, second we type:

```
django-admin startproject mysite
```

where `mysite` is the name of the project.
The following will be the structure of the project:

```
mysite/
	manage.py
	mysite/	
		__init__.py
		settings.py
		urls.py
		wsgi.py
```

this files are:

* the outer `mysite/` root directory is just a container for your project, the name doesn't matter to Django; you can rename it to anything you like.  
* `manage.py`: A command line utility that let you interact with this Django project in various ways.  
* the inner `mysite/` directory is the actual Python package for the project.  
* `mysite/__init__.py`:and empty file that tells Python package that this directory should  be considered a Python package.  
* `mysite/settings.py`: Settings/configuration for this Django project.   
* `mysite/urls.py`: The URL declarations for this Django project; a “table of contents” of your Django-powered site.  
* `mysite/wsgi.py`: An entry-point for WSGI-compatible web servers to serve your project. See How to deploy with WSGI for more details.  



#[django-admin and manage.py](https://docs.djangoproject.com/en/2.2/ref/django-admin/)

`django-admin` is the Django's command-line utility, the manage.py is created automatically when the project is created and it does the same thing as django-admin.

*Usage*

```
$ django-admin <command> [options]
$ manage.py <command> [option]
```
*Getting runtime help*

```
django-admin help
```

* Run `django-admin help` to display usage information and a list of commands
* Run `django-admin help --commands` to display a list of all available commands

*determining the version*

```
django-admin version
```

to get the version use in this project.  

##