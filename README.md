# Show and Explain how python packages work

This Repo tries to explain and show how python packaging is working.

Packaging is for a python beginner a very hard to understand topic and there are
many caveats and pseudo solutions a python beginner could struggle with

The following sections will describe the different tests.

To avoid issues between the tests, it is a good approach to start a new console for each test.

## Test 01

Very basic setup. We have one package `my_package` and inside one module 
`my_module.py`. The module includes one function main, which lists all available
modules at runtime, completely ripped of https://stackoverflow.com/a/42673938/10985257

Outside the package, a `run.py` scripts exists, which is the entry point for the test.

Test 01 works perfectly fine with no further actions. This might seem like good
approach, but might lead to other issues, which are better shown by [Test 02](#test-02).

To run the test manual just run

```bash
cd test_01
python run.py | grep $USER
```
### Excepted Result

```bash
my_package                     | <repo_path>/test_01/my_package/__init__.py
run                            | <repo_path>/test_01/run.py
```

## Test 02

Very similar approach like in [Test 01](#test-01) but this time, the `run.py` is located inside the package `my_package`.

This always results in a `ModuleNotFoundError`.

We can try different approaches:

```bash
cd test_02
python my_package/run.py | grep $USER
```

or

```bash
cd test_02/my_package
python run.py | grep $USER
```
both approaches will fail

### Excepted Result

```bash
Traceback (most recent call last):
  File "/home/matti.kaupenjohann/test/pyimport/test_02/my_package/run.py", line 1, in <module>
    from my_package.my_mod import main
ModuleNotFoundError: No module named 'my_package'
```

## Test 03

We still have the run script inside `my_package`, but this time we only import via relative import.
While this might seems to be solution, this might cause trouble further down the structure.
The import does not anticipate the actual package and it is basically a module-level and not a package-level import. 

To run Test 03:

```bash
cd test_03
python my_package/run.py | grep $USER
```


### Excepted Result

```bash
run                            | <repo_path>/test_03/my_package/run.py
```

### Comparison

By comparing the result with [Test 01](#excepted-result) the difference is directly present, we are seeing the `run.py` script but this time not the package.

## Test 04

Since all test until now results in not perfect solutions, we now want to try a different approach, which is sadly a bit more sophisticated, but leads in the direction, which solves our issues.

To have access to package which you want to develop we need to install our package.

To do this inside a save environment, we utilize a virtual environment. If you know what that is, perfect, if not just think about a place in the computer, which is not disturbed by other programs.

We now have added a new file called `setup.py` which is a small helper script, to install a package.

Take a look inside, it is not very complicated.

To install package and run the script:

```bash
cd test_04
python -m venv .venv
source .venv/bin/activate
pip install .
python my_package/run.py | grep $USER
deactivate
```

### Excepted Result

```bash
run                            | <repo_path>/test_04/my_package/run.py
my_package                     | <repo_path>/test_04/.venv/lib/python3.12/site-packages/my_package/__init__.py
pip                            | <repo_path>/test_04/.venv/lib/python3.12/site-packages/pip/__init__.py
```

### Comparison

We can now see that our package `my_package` is accessible via the virtual environment, but our script `run.py` is the actual script in our project structure. 
The additional pip can be ignored, since it will always be present if we use a virtual environment.


## Test 05

So why do we need the fifth test? Well, the solution of [Test 04](#test-04) seemed to solve all issues, but creates a new one if we actively develop our package.
To solve this issue we need to fix for development our install to command. We install the package as editable.

To install package in development and run the script:

```bash
cd test_05
python -m venv .venv
source .venv/bin/activate
pip install -e .
python my_package/run.py | grep $USER
```

### Excepted Result

```bash
run                            | <repo_path>/test_05/my_package/run.py
__editable___my_package_1_0_0_finder | <repo_path>/test_05/.venv/lib/python3.12/site-packages/__editable___my_package_1_0_0_finder.py
pip                            | <repo_path>/test_05/.venv/lib/python3.12/site-packages/pip/__init__.py
```

### Comparison

Now instead of the installed package, we have an editable package finder installation, which points at our development environment.

## Test 06

#TODO DESCRIPTION

```bash
run                            | <repo_path>/test_06/my_package/run.py
_virtualenv                    | <repo_path>/test_06/.venv/lib/python3.12/site-packages/_virtualenv.py
pip                            | <repo_path>/test_06/.venv/lib/python3.12/site-packages/pip/__init__.py
my_package                     | <repo_path>/test_06/my_package/__init__.py
```