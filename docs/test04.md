---
layout: page
title: "Test 04"
permalink: /test04
---

Since all test until now results in not perfect solutions, we now want to try a different approach, which is sadly a bit more sophisticated, but leads in the direction, which solves our issues.

To have access to package which you want to develop we need to install our package.
To do this inside a save environment, we utilize a virtual environment. If you know what that is, perfect, if not just think about a place in the computer, which is not disturbed by other programs.
We now have added a new file called `setup.py` which is a small helper script, to install a package.

Take a look inside, it is not very complicated.

To install package and run the script:

<details><summary markdown="span">**bash**</summary>
```bash
cd test_04
python -m venv .venv
source .venv/bin/activate
pip install .
python my_package/run.py | grep $USER
```
</details>

<details><summary markdown="span">**powershell**</summary>
```powershell
cd test_04
python -m venv .venv
.venv/Script/Activate.ps1
pip install .
python my_package/run.py | Select-String $env:username
```
</details>

### Expected Result

```bash
run                            | <repo_path>/test_04/my_package/run.py
my_package                     | <repo_path>/test_04/.venv/lib/python3.12/site-packages/my_package/__init__.py
pip                            | <repo_path>/test_04/.venv/lib/python3.12/site-packages/pip/__init__.py
```

### Comparison

We can now see that our package `my_package` is accessible via the virtual environment, but our script `run.py` is the actual script in our project structure.
The additional pip can be ignored, since it will always be present if we use a virtual environment.
