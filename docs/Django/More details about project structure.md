# More Details about the project structure and  essencial methods/files

##[django-admin and manage.py](https://docs.djangoproject.com/en/2.2/ref/django-admin/)  

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

## Brief view to [URL dispatcher](https://docs.djangoproject.com/en/2.2/topics/http/urls/)

To design URLs for an app, you create a Python module informally called a URLconf (URL configuration). This module is pure Python code and is a mapping between URL path expressions to Python functions (your views).

## How Django processes a request 

When a user requests a page from your Django-powered site, this is the algorithm the system follows to determine which Python code to execute:

1. Django determines the root URLconf module to use. Ordinarily, this is the value of the **ROOT_URLCONF** setting, but if the incoming *HttpRequest* object has a urlconf attribute (set by middleware), its value will be used in place of the **ROOT_URLCONF** setting.  

2. Django loads that Python module and looks for the variable *urlpatterns*. This should be a sequence of **django.urls.path()** and/or **django.urls.re_path()** instances.

3. Django runs through each URL pattern, in order, and stops at the first one that matches the requested URL.  

4. Once one of the URL patterns matches, Django imports and calls the given view, which is a simple Python function (or a class-based view). The view gets passed the following arguments:
	* An instance of *HttpRequest*.  
	* If the matched URL pattern returned no named groups, then the matches from the regular expression are provided as positional arguments.  
	* The keyword arguments are made up of any named parts matched by the path expression, overridden by any arguments specified in the optional *kwargs* argument to **django.urls.path()** or **django.urls.re_path()**.  

5. If no URL pattern matches, or if an exception is raised during any point in this process, Django invokes an appropriate error-handling view.

**Example**

```python
from django.urls import path

from . import views

urlpatterns = [
    path('articles/2003/', views.special_case_2003),
    path('articles/<int:year>/', views.year_archive),
    path('articles/<int:year>/<int:month>/', views.month_archive),
    path('articles/<int:year>/<int:month>/<slug:slug>/', views.article_detail),
]
```
Notes:

* To capture a value from the URL, use angle brackets.  
* Captured values can optionally include a converter type. For example, use **<int:name>** to capture an integer parameter. If a converter isn’t included, any string, excluding a **/** character, is matched.

* There’s no need to add a leading slash, because every URL has that. For example, it’s **articles**, not **/articles**.

Example requests:

* A request to **/articles/2005/03/** would match the third entry in the list. Django would call the function ` views.month_archive(request, year=2005, month=3)`.  

* **/articles/2003/** would match the first pattern in the list, not the second one, because the patterns are tested in order, and the first one is the first test to pass. Feel free to exploit the ordering to insert special cases like this. Here, Django would call the function `views.special_case_2003(request)`  

* **/articles/2003** would not match any of these patterns, because each pattern requires that the URL end with a slash.  

* **/articles/2003/03/building-a-django-site/** would match the final pattern. Django would call the function `views.article_detail(request, year=2003, month=3, slug="building-a-django-site")`.  


### Path converters¶
The following path converters are available by default:

* **str** - Matches any non-empty string, excluding the path separator, '/'. This is the default if a converter isn’t included in the expression.

* **int** - Matches zero or any positive integer. Returns an int.

* **slug** - Matches any slug string consisting of ASCII letters or numbers, plus the hyphen and underscore characters. For example, building-your-1st-django-site.

* **uuid** - Matches a formatted UUID. To prevent multiple URLs from mapping to the same page, dashes must be included and letters must be lowercase. For example, **075194d3-6885-417e-a8a8-6c931e272f00**. Returns a **UUID** instance.

* **path** - Matches any non-empty string, including the path separator, **'/'**. This allows you to match against a complete URL path rather than just a segment of a URL path as with str.


## `path()`

**path(route,view,kwarg=None,name=None**

Returns an element for inclussion in `urlpatters`, for example:

```python
from django.urls import include, path

urlpatterns = [
    path('index/', views.index, name='main-view'),
    path('bio/<username>/', views.bio, name='bio'),
    path('articles/<slug:title>/', views.article, name='article-detail'),
    path('articles/<slug:title>/<int:section>/', views.section, name='article-section'),
    path('weblog/', include('blog.urls')),
    ...
]
```

* The **route** is in [more cases](https://docs.djangoproject.com/en/2.2/topics/i18n/translation/#translating-urlpatterns) a string, this string can contain anlge brakets, like `<username>` in the example above, this can be use to capture a part of the URL and send it as a keyword argument to the view, this angle brakes may include converter specification, like `<int:section>`, in this case the it will catch or match a string of decimal digits and converts the value to a *int* .

* The **view** argument is a view that will be the result of the match, this argument can be a `include()`

* The *kwargs* argument allows you to pass additional arguments to the view function or method, more info [here](https://docs.djangoproject.com/en/2.2/topics/http/urls/#views-extra-options).

* The name is an useful argument to name the URL and its advantage are mentioned [here](https://docs.djangoproject.com/en/2.2/topics/http/urls/#naming-url-patterns)

more versions of `path()` such as `re_path()` for regular expression adn more information about `include()` can be find in [django.urls.path](https://docs.djangoproject.com/en/2.2/ref/urls/#django.urls.path)