The idea will be follow the article from medium [Creating a dataset using an API with Python](https://towardsdatascience.com/creating-a-dataset-using-an-api-with-python-dcc1607616d) from this we will change code at will to fit more my personal style or just to try different things.

## Import Libraries 

There will be 3 main libraries to be use in this project:

* `request` this will help use to get content from the API usign the method `get()` and to decide the format of how are we getting this info using `json()` so we can handle the answer for he API using JSON.

* `json` with this library we can work with JSON 

* `pandas` this will help us to create the dataframes that later can be export to a .cvs file.

we will import `numpy` as well, ... just in case.

## Understanding the API

We want first to understand what is the information that the API is giving us, what type of data and what values, so for that we are going to start by calling the API and display the content.

first, the API end point is *https://wind-bow.glitch.me/twitch-api/channels/freecodecamp* this API doesn't require any authentication which will make the process easier 

```python 

import numpy as np
import pandas as pd
import requests
import json
