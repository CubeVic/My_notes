## Installing Virtualenv

Assuming python 3 it is already installed as well as `pip` we can start in this way:

```
pip install virtualenv
```

![virtual_eniroments_001](../images/virtual_environments_001.png)

## Creating the Virtual Environment 

Now we can select the directory where we are going to save the virtual environment, in this example we will use the directory "/Users/victoraguirre/Documents/026.workspace_Python", and we can provide a name for it ( virtual environment), in this case i will choose `virtualEnv000`

```
virtualenv -p python3 /Users/victoraguirre/Documents/026.workspace_Python/virtualEnv000
```

![virtual_enviroment_002](../images/virtual_environments_002.png)

## Activate environments

now a Folder with the name of the environment it is going to be created, the first step to activate the environment will be to navigate to that folder

![virtual_environments](../images/virtual_environments_003.png)

and later call the `activate` file that is inside the `bin` directory 

``` 
// on Mac
cd /Users/victoraguirre/Documents/026.workspace_Python/virtualenv
source bin/activate

// On windows
call /Users/victoraguirre/Documents/026.workspace_Python/virtualenv
source bin/activate.bat
```

![virtual_environments_004](../images/virtual_environments_004.png)

As part of this exercise I will install Flask inside this virtual environment

## Install packages and create a file

now lets install flask

```
pip install flask
```

here the basic code for a page in flash

![virtual_environments_005](../images/virtual_environments_005.png)

now running 

```
python app.py
```

we have the server running ans the website up ( default IP http://127.0.0.1:5000)

![virtual_environments_006](../images/virtual_environments_006.png)

![virtual_environments_007](../images/virtual_environments_007.png)

## Deactivate environment

Now, to stop the environment we just need to type `deactivate`

![virtual_environments_008](../images/virtual_environments_008.png)
