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