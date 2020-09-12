Flask use [Jinja](https://jinja.palletsprojects.com/en/2.11.x/templates/) template labray to render the templates.

Jinja is base in Django and Python syntax, although, the blocks are represented by special delimiters whihc will distinguish the jijnaja suyntax from the static data in the template.

Anything between `{{` and `}}` is and expresuion and it will be output to the final document, example, the value of a variable `{{ g.user['username'] }}`. Now the control flow statemente like `if` and `for` will use `{%` and `%}` but here is de difference with python. Python use indentation to denotate the blocks, jinja will use a special tag, like:   
```jinja2
{% if condition %} 
	here the logic 
{% endif %}
```  

Here some delimiters

* `{% ... %}` for [Statements](https://jinja.palletsprojects.com/en/2.11.x/templates/#list-of-control-structures).  
* `{{ ... }}` for [Expressions](https://jinja.palletsprojects.com/en/2.11.x/templates/#expressions) to print to the template output.  
* `{# ... #}` for [Comments](https://jinja.palletsprojects.com/en/2.11.x/templates/#comments) not included in the template output.
* `#  ... ##` for Line [Statements](https://jinja.palletsprojects.com/en/2.11.x/templates/#line-statements).

## The Base Layout

As a template we can create a basic template that will work as base to all the other templates, in this case all the layout will fallow a similar pattern but with different body, so we can create a base layout and the other will extend of this base template and override the specific sesctions.

**flaskr/template/base.html**
```html
<!doctype html>
<title>{% block title %}{% endblock %} - Flaskr </title>
<link rel="stylesheet" href="{{ url_for('static', filename='style.css')}}">
<nav>
	<h1>Flaskr</h1>
	<ul>
		{% if g.user %}
			<li><span>{{ g.user['username'] }}</span>
			<li><a href="{{ url_for('auth.logout') }}"> Log Out</a>
		{% else %}
			<li><a href="{{ url_for('auth.register') }}">Register</a>
      		<li><a href="{{ url_for('auth.login') }}">Log In</a>
		{% endif %}
	</ul>
</nav>

<section class="content">
	<header>
		{% block header %}{% endblock %}
	</header>
	{% for message in get_flashed_messages() %}
		<div class="flash">{{ message }}</div>
	{% endfor %}
	{% block content %}{% endblock %}
</section>
```

`g` is available in templates, thanks to `g.user` from `load_logged_in_user`, if the value of `g.user` is `TRUE`, the user name and the logout option are display, otherwise the registration and log in links are display.

just before the content and after the page title we will display the error message, if any. we create a loop with the message returned by `get_flashed_message()`, this is the code to display it, and work together with the code in the view `flash()`, `flash()` show the error message and code in the above example display it.

In the previous code we defined 3 blocks, those blocks are going to be overwrite for each specific template ( it will make more sense after the following items):

1. `{% block title %}` this block will be use to change the title in the browser tab
2. `{% block header %}` this will change the title display on the page
3. `{% block content %}` Here is where all the content of each specific page goes.


> to keep everything organize, it is a good practice to keep the templates in a folder with the same name of the blue print.

## Register Template

Here is were we start to get an idea of what the template system can do, in this case we will create a page that `extends` from he basic template so we don't need to worry about the common elements line the navigation bar, we just code the specific logic and experience of this page, in this case registration.

**flaskr/templetes/auth/register.html**
```html
{% extends 'base.html' %} 

{% block header %} 
	<h1>{% block title %} Register {% endblock %} </h1>
{% endblock %} 

{% block content %}
  <form method="post">
    <label for="username">Username</label>
    <input name="username" id="username" required>
    <label for="password">Password</label>
    <input type="password" name="password" id="password" required>
    <input type="submit" value="Register">
  </form>
{% endblock %}
```

The point to remark here: 

* `{% extends 'base.html' %}` here we tell jinja that this is a template that should replace the blocks in the base templates, in this case `base.html`
* `{% block header %}`,`{% block content %}` and `{% endblock %}`  the first to just contain the content that must be replace in the template, the last one `{% endblock %}`  is just to indicate the end of the block.

## Log In

Similar to the previous template with the difference in the summit button

**flaskr/templetes/auth/login.html**
```html
{% extends 'base.html' %}

{% block header %}
  <h1>{% block title %}Log In{% endblock %}</h1>
{% endblock %}

{% block content %}
  <form method="post">
    <label for="username">Username</label>
    <input name="username" id="username" required>
    <label for="password">Password</label>
    <input type="password" name="password" id="password" required>
    <input type="submit" value="Log In">
  </form>
{% endblock %}
```

## Static files

This will be the CSS, Javascript files and logos for the application, on the base template we can see that we use `{{ url_for('static', filename='style.css')}}` this will search in the relative path to the `flaskr/static` directory.

