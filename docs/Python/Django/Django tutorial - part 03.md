In this part we will focus in the "views", the views are a type of webpage that serve a specific function and has a specific template, for this polls example we will have four views:

* Question 'index' page:  Display the latest few questions.
* Question "details" page: Displays a question text, with no results but with a form to vote.
* Question "results" page: display results for a particular question
* vote action: handle voting for a particular choice in a particular question.

Now from Django tutorial page we have:

> In Django, web pages and other content are delivered by views. each view is represented by simple python function (or methods, in the case of class-based views). Django will choose a view by examining the URL that 's requested ( to be precise the part of the URL after the domain name)
> A URL pattern is simply the general form of a URL - for example: 
`/newsarchive/<year>/<month>/`
> The get from URL to a View, Django use 'URLconfs' a URLconfs map the URL pattern to views
more info in [URL dispatcher](https://docs.djangoproject.com/en/2.2/topics/http/urls/)


## Writing more views

Now, to add more views we can go to `polls/views.py` and add

```python
def detail(request, question_id):
	return HttpResponse("You're looking at question %s" % question_id)

def results(request,question_id):
	response = "you're looking at the results of question %s"
	return HttpResponse(response % question_id)

def vote(request, question_id):
	return HttpResponse("you're voting on question %s" % question_id)

```

wire these new views into the `polls.urls` module by adding the `path()` calls:

```python
from django.urls import path

from . import views

urlpatterns = [
	# ex: /polls/
    path('', views.index, name='index'),
    # ex: /polls/5/
    path('<int:question_id>/', views.detail, name='detail'),
    # ex: /polls/5/results/
    path('<int:question_id>/results/', views.results, name='results'),
    # ex: /polls/5/vote/
    path('<int:question_id>/vote/', views.vote, name='vote'),

]
```

>When somebody requests a page from your website – say, `“/polls/34/”`, Django will load the mysite.urls Python module because it’s pointed to by the `ROOT_URLCONF` setting. It finds the variable named urlpatterns and traverses the patterns in order. After finding the match at `'polls/'`, it strips off the matching text `("polls/")` and sends the remaining text – `"34/"` – to the `‘polls.urls’` URLconf for further processing. There it matches `'<int:question_id>/'`, resulting in a call to the `detail()` view like so: 
```python 
detail(request=<HttpRequest object>, question_id=34)
``` 
>The `question_id=34` part comes from `<int:question_id>`. Using angle brackets “captures” part of the URL and sends it as a keyword argument to the view function. The `:question_id>` part of the string defines the name that will be used to identify the matched pattern, and the `<int:` part is a converter that determines what patterns should match this part of the URL path.

## `views` that actually do something 

The `view` a clear responsibility, returns a `HttpResponse` object containing the content of the page requested, or raise a `Http404` exception the rest its depends of the user.

the view can record or retrieve content of a database, create zip or pdf files, can use the template system of  Django or a third party, it can do pretty much everything you want and using whatever you want from the python libraries.

in the words of the tutorial "all Django wants is that `HttpResponse` or and exception"

in this example we will continue with the build-in database, and we will display the latest 5 polls separated by comas.

```python 
from django.http import HttpResponse

from .models import Question

def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    output = ', '.join([q.question_text for q in latest_question_list])
    return HttpResponse(output)
``` 

the only problem here, is that all the code is hardcoded, which will make it difficult to make modification to it, is there where the feature of **Templates** came handy, with Django template system we can separate the design from the python code making it easy to change the appearance without the need to change the python code. 

### Templates and how to do it

First, we need a new directory, it will be call **templates** it will be in the directory **polls**, Django will look for the templates in this directory.

here some explanation from the Django documentation: 
>Your project’s **TEMPLATES** setting describes how Django will load and render templates. The default settings file configures a **DjangoTemplates** back-end whose **APP_DIRS** option is set to **True**. By convention **DjangoTemplates** looks for a “templates” subdirectory in each of the **INSTALLED_APPS**.

Inside this **templates** directory we need to create a new directory called **polls** and inside a document call **index.html**, so it will be something like **polls/templates/polls/index.html**

inside this new file, the template file, we are going to add the following code

```html
{%if latest_question_list %}
    <ul>
        {%for question in latest_question_list %}
        <li><a href="/polls/{{question.id}}">{{question.question_text}}</a>
        </li>
        {% endfor %}
    </ul>
{% else %}
    <p>No polls are available</p>
{% endif %}
```

but if we run it in this way we will have a lot of errors,

we need to make sure we make modification to the `polls/views.py` file

#### Modify the `views` file

1. make sure to add `from .models import Question` to import the models 
2. import the templates with `from django.template import loader`
3. modify the function index in the following way

```python 
def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    template = loader.get_template('polls/index.html')
    context = {
        'latest_question_list': latest_question_list,
    }
    return HttpResponse(template.render(context, request))
``` 

so the script `polls/views.py` will be

```python 
from django.http import HttpResponse
from django.template import loader

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    template = loader.get_template('polls/index.html')
    context = {
        'latest_question_list': latest_question_list,
    }
    return HttpResponse(template.render(context, request))
``` 

now if we go to our browser *http://127.0.0.1:8888/polls/* we will see a list of the polls 


## Shortcut `render()`

There is a way to make the previous code a bit shorter, that will be using the method `render()` this method will take as a *first* argument the *request object*, *second* a template, *third* (optional) a dictionary, and it will give back a `HttpResponse`

so the new `index()` view will be

```python 
from django.shortcuts import render

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)
``` 

## Raising 404 errors

Now, for those cases where the page is not found, of the question is not found we can use the `Http404` error, for that we will need to raise an exception, we are going to use the details view  on `polls/views.py`

```python 
from django.shortcuts import render
#from django.template import loader #cuz we are using render()
# Create your views here.
from django.http import HttpResponse
from .models import Question


#Because we are using render()
# def index(request):
#     latest_question_list = Question.objects.order_by('-pub_date')[:5]
#     template = loader.get_template('polls/index.html')
#     context = {
#         'latest_question_list': latest_question_list,
#     }
#     return HttpResponse(template.render(context, request))


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)
    
def detail(request, question_id):
    try:
        question = Question.objects.get(pk=question_id) #pk stand for primary key
    except Question.DoesNotExist:
        raise Http404("Question does not exist")
    return render(request, 'polls/detail.html',{'question': question})

def results(request,question_id):
    response = "you're looking at the results of question %s"
    return HttpResponse(response % question_id)

def vote(request, question_id):
    return HttpResponse("you're voting on question %s" % question_id)
``` 

and now we need to create the template, for that we will create a new file on `polls/templates/polls` this file will be `details.html` so the full address will be `polls/templates/polls/details.html` and inside 

```html
{{question}}
```

### Shortcut `get_object-or-404()`

Like with the previous scenario there is a way to make the code shorter, for that we can use `get_object_or_404()`

`get_object_or_404()` take as *first* argument  the model, this method can take several other keyword arguments that can be pass to the `get()` function of the model's manager. It raise the `Http404` if the object doesn't exist 

so the modification to the `details()` view will be 

```python 
def detail(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/detail.html', {'question': question})
``` 

making the hold file 


```python 
from django.shortcuts import render
#from django.template import loader #cuz we are using render()
# Create your views here.
from django.http import HttpResponse
from .models import Question


#Because we are using render()
# def index(request):
#     latest_question_list = Question.objects.order_by('-pub_date')[:5]
#     template = loader.get_template('polls/index.html')
#     context = {
#         'latest_question_list': latest_question_list,
#     }
#     return HttpResponse(template.render(context, request))


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)
    
# because we use get_object_or_404()
# def detail(request, question_id):
#     try:
#         question = Question.objects.get(pk=question_id) #pk stand for primary key
#     except Question.DoesNotExist:
#         raise Http404("Question does not exist")
#     return render(request, 'polls/detail.html',{'question': question})

def detail(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/detail.html', {'question': question})

def results(request,question_id):
    response = "you're looking at the results of question %s"
    return HttpResponse(response % question_id)

def vote(request, question_id):
    return HttpResponse("you're voting on question %s" % question_id)
``` 

> There’s also a `get_list_or_404()` function, which works just as `get_object_or_404()` – except using `filter()` instead of `get()`. It raises `Http404` if the list is empty.

## Using the template system  - `detail()`

now using the context variable `question` the template `polls/detail.html` will be 

```html
<h1>{{question.question_text}}</h1>
    <ul>
        {% for choice in question.choice_set.all %}
        <li> {{ choice.choice_text}} </li>
        {% endfor %}
    </ul>
```

In the templates the dot-lookup notation is use to access variable attributes, example `{{ question.question_text}}`, Django first make a dictionary lookup if this fail it will do a list lookup.

Method-calling happens in the `{% for %}` loop: `question.choice_set.all` will create a iterable of the object `Choice` the statement is interpreted by python as `questionn.choice_set.all()` this iterable object is suitable for the `{% for %}`.

> Documentation about templates here [template guide](https://docs.djangoproject.com/en/3.0/topics/templates/)

### Brief view to **The Django template language**

Template are rendered in a context, Rendering replace the content of the variables of this context, tags are execute and then everything else is output as is.

There are 4 constructs in Django:

* Variables
* Tags
* Filters
* Comments 

#### Variables 

The variables are placeholders that going to be located between "{{" and "}}", the output of this variables it is going to depend of the context, which is a dict-like object that map key values, everything will be clear with the example 

Let say the context is: 
```
 {'first_name': 'John', 'last_name': 'Doe'}
```
and we have something like 
```html
My first name is {{ first_name }}. My last name is {{ last_name }}.
```
we will have an answer like 
```
My first name is John. My last name is Doe.
```

The notation implemented for Dictionary lookup, object lookup and list lookup will be 

```html
{{ my_dict.key }}
{{ my_object.attribute }}
{{ my_list.0 }}
```

#### Tag

Provide arbitrary logic in the rendering process.

The definition is vague on purpose, this can serve control structures, get database data or access other templates

It is surrounded by "{%" and "%}"

```DTL
{% if user.is_authenticated %}Hello, {{ user.username }}.{% endif %}
```
More information about [Tag](https://docs.djangoproject.com/en/3.0/ref/templates/builtins/#ref-templates-builtins-tags)

#### Filter

Filters transform the values of the variable or the tags 
for a filter like:

```hmtl
{{ django|title }}
```
with a context like:
```html
{'django': 'the web framework for perfectionists with deadlines'}
```
result will be 
```html
The Web Framework For Perfectionists With Deadlines
```

more information about [Filter](https://docs.djangoproject.com/en/3.0/ref/templates/builtins/#ref-templates-builtins-filters)

#### Commets

The comments look like
```html
{# comments #}
```

for a multi-line comments

```html
{% comments %}
```

## Removing hardcore URLs in templates 

To maintain a loosely couple approach we will, need to modify the hard-code that we have in the `polls/index.html` template, this can be achieve thank to the name argument in the `path()` function in the `pools.urls` module, we will use the tag `url` to do this in the template.

so from a template like
```html
<li><a href="/polls/{{ question.id }}/">{{ question.question_text }}</a></li>
```
we have a template like 
```html
<li><a href="{% url 'detail' question.id %}">{{ question.question_text }}</a></li>
```
this works because Django will look the URL definition as specified in `polls.urls` module. and the we can see **'detail'** defined 

```python 
...
# the 'name' value as called by the {% url %} template tag
path('<int:question_id>/', views.detail, name='detail'),
...
```

so if in the future we decided to change the url of the polls we can do it in `polls/urls.py` and just in that file
