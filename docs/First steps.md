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
* `mysite/settings.py`: [Settings/configuration](https://docs.djangoproject.com/en/2.2/topics/settings/) for this Django project.   
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

## brief view to [URL dispatcher](https://docs.djangoproject.com/en/2.2/topics/http/urls/)

To design URLs for an app, you create a Python module informally called a URLconf (URL configuration). This module is pure Python code and is a mapping between URL path expressions to Python functions (your views).

# How Django processes a request 

When a user requests a page from your Django-powered site, this is the algorithm the system follows to determine which Python code to execute:

1. Django determines the root URLconf module to use. Ordinarily, this is the value of the **ROOT_URLCONF** setting, but if the incoming *HttpRequest* object has a urlconf attribute (set by middleware), its value will be used in place of the **ROOT_URLCONF** setting.  

2. Django loads that Python module and looks for the variable *urlpatterns*. This should be a sequence of **django.urls.path()** and/or **django.urls.re_path()** instances.

3. Django runs through each URL pattern, in order, and stops at the first one that matches the requested URL.  

4. Once one of the URL patterns matches, Django imports and calls the given view, which is a simple Python function (or a class-based view). The view gets passed the following arguments:

* An instance of HttpRequest.  
* If the matched URL pattern returned no named groups, then the matches from the regular expression are provided as positional arguments.  
* The keyword arguments are made up of any named parts matched by the path expression, overridden by any arguments specified in the optional *kwargs* argument to **django.urls.path()** or **django.urls.re_path()**.  

5. If no URL pattern matches, or if an exception is raised during any point in this process, Django invokes an appropriate error-handling view