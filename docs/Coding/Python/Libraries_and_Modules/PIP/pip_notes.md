![pip](images/pip_logo.png){: .center }

`pip` is a package installer python, it can be use to install packages fro the python packages index.

1. [Documentation](https://pip.pypa.io/en/stable/user_guide/)
2. [PyPI](https://pypi.org/project/pip/)
3. [GitHub](https://github.com/pypa/pip)

##Check if `pip` is install

pip is already installed in python 2 and python 3, but we can double check the version in the following way: 

```bash
python -m pip --version
```

## Installation 

There are two was to install packages using `pip` one will be for machines with access to a network and other without access

```
python -m pip <pip arguments>
```

### With access to a network

We can install packages like:

```
python -m pip install SomePackage
```

Normally we will be able to use: 

```
pip install SomePackage
```

### Without access to network

We can download the packages from PyPI or obtained elsewhere, and installed in the following way:

```
python -m pip install SomePackages-1.0-py2.py3-none-any.whl
```

### Installation of specific version of the packages

```
python -m pip install SomePackage            # latest version
python -m pip install SomePackage==1.0.4     # specific version
python -m pip install 'SomePackage>=1.0.4'     # minimum version
```



## Get packages installed
to get a list of packages and versions install in a machine we can use 

```
pip freeze  > requirements.txt
```

with the previous command we will get all the packages and save it in the document requirements.txt file

## Uninstall packages

For uninstall packages:
```
pip uninstall SomePackages
```
to uninstall all the packages

```
pip freeze | xargs pip uninstall -y
```
or

```
pip uninstall -r requirements.txt
```
it will ask if we want to uninstall one by one.
to uninstall everything 

```
pip uninstall -r requirements.txt -y
```
