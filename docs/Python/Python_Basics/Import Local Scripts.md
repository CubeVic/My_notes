## Import Local Scripts

Import is helpful when working on bigger projects where you want to organize the code into multiple files  and reuse the code in those files, if the python script is in the same directory  of the current script we can use `import` follow by the name of the file , without the .py extension.

```python
import useful_functions
```

to make it easier to use we can create aliases for the different script imported

```python
import usefull_functions as uf
uf.add_five([1,2,3,4])
```

now, in many occasions the is code in this scripts that is not useful, or not useful in a script that is calling them, so in this case we use the "main"  block

## Using a main block
To avoid running executable statements in a script when it's imported as a module in another script, include these lines in an `if __name__ == "__main__" `block. Or alternatively, include them in a function called main() and call this in the `if main` block.

The code inside the block main will be execute just when we are running the script in specific and not when we are colling it as module in a script.

```python
# demo.py

import useful_functions as uf

scores = [88, 92, 79, 93, 85]

mean = uf.mean(scores)
curved = uf.add_five(scores)

mean_c = uf.mean(curved)

print("Scores:", scores)
print("Original Mean:", mean, " New Mean:", mean_c)

print(__name__)
print(uf.__name__)

```

``` python
# useful_functions.py

def mean(num_list):
    return sum(num_list) / len(num_list)

def add_five(num_list):
    return [n + 5 for n in num_list]

def main():
    print("Testing mean function")
    n_list = [34, 44, 23, 46, 12, 24]
    correct_mean = 30.5
    assert(mean(n_list) == correct_mean)

    print("Testing add_five function")
    correct_list = [39, 49, 28, 51, 17, 29]
    assert(add_five(n_list) == correct_list)

    print("All tests passed!")

if __name__ == '__main__':
    main()
```

## Most common use Python Standard Library modules

The Python Standard Library has a lot of modules, here are a selection of our Python Standard Library modules and why we use them!

* `csv`: very convenient for reading and writing csv files
* `collections`: useful extensions of the usual data types including OrderedDict, defaultdict and namedtuple
* `random`: generates pseudo-random numbers, shuffles sequences randomly and chooses random items
* `string`: more functions on strings. This module also contains useful collections of letters like string.digits (a string containing all characters which are valid digits).
* `re`: pattern-matching in strings via regular expressions
* `math`: some standard mathematical functions
* `os`: interacting with operating systems
* `os.path`: submodule of os for manipulating path names
* `sys`: work directly with the Python interpreter
* `json`: good for reading and writing json files (good for web work)

## Techniques for Importing Modules

there are some variants of `import` that are useful in different situation.

1. To import an individual function or class:

```python
from module_name import object_name
```

2. To import multiple individual object from a module:

```python
from module_name import firts_object, second_object
```

3. To rename a module:

```python
import module_name as new_name
```

4. To import an object from a module and rename it:

```python
from module_name import object_name as new_name
```
5. To import everything

```python
import module_name
```

## Modules, packages, and Names

In order to manage the coder better, the modules of python are contain in **package**, this package is just a container for the modules, to call the sub-module from one package we use the dot notation:

```python
import package_name.submodule_name
```

## Third-party packages

normally in a project you will find a document call requirements.txt which is a list that contain all the modules, packages and its version us in the specific script, the requirements.txt file looks like:

```
beautifulsoup4==4.5.1
bs4==0.0.1
pytz==2016.7
requests==2.11.1
```
to install all the packages on this file we can use pip, the command will be:
```cmd
pip install -r requirements.txt
```
Some of the popular third-party packages are:

* [IPython](https://ipython.org/) - A better interactive Python interpreter
* [requests](https://2.python-requests.org/en/master/) - Provides easy to use methods to make web requests. Useful for accessing web APIs.
* [Flask](http://flask.pocoo.org/) - a lightweight framework for making web applications and APIs.
* [Django](https://www.djangoproject.com/) - A more featureful framework for making web applications. Django is particularly good for designing complex, content heavy, web applications.
* [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/) - Used to parse HTML and extract information from it. Great for web scraping.
* [pytest](https://docs.pytest.org/en/latest/) - extends Python's builtin assertions and unittest module.
* [PyYAML](https://pyyaml.org/wiki/PyYAML) - For reading and writing YAML files.
* [NumPy](http://www.numpy.org/) - The fundamental package for scientific computing with Python. It contains among other things a powerful N-dimensional array object and useful linear algebra capabilities.
* [pandas](http://pandas.pydata.org/) - A library containing high-performance, data structures and data analysis tools. In  particular, pandas provides dataframes!
* [matplotlib](https://matplotlib.org/) - a 2D plotting library which produces publication quality figures in a variety of hardcopy formats and interactive environments.
* [ggplot](http://ggplot.yhathq.com/) - Another 2D plotting library, based on R's ggplot2 library.
* [Pillow](https://python-pillow.org/) - The Python Imaging Library adds image processing capabilities to your Python interpreter.
* [pyglet](https://bitbucket.org/pyglet/pyglet/wiki/Home) - A cross-platform application framework intended for game development.
* [Pygame](https://www.pygame.org/news) - A set of Python modules designed for writing games.
* [pytz](http://pytz.sourceforge.net/) - World Timezone Definitions for Python
