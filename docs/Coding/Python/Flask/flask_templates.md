Flask use [Jinja](https://jinja.palletsprojects.com/en/2.11.x/templates/) template labray to render the templates.

Jinja is base in Django and Python syntax, although, the blocks are represented by special delimiters whihc will distinguish the jijnaja suyntax from the static data in the template.

Anything between `{{` and `}}` is and expresuion and it will be output to the final document, example, the value of a variable `{{ g.user['username'] }}`. Now the control flow statemente like `if` and `for` will use `{%` and `%}` but here is de difference with python. Python use indentation to denotate the blocks, jinja will use a special tag, like:   
```
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

{% ... %} for Statements

{{ ... }} for Expressions to print to the template output

{# ... #} for Comments not included in the template output

#  ... ## for Line Statements