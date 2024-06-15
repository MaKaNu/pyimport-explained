---
layout: page
title: "Test 05"
permalink: /test05
---

So why do we need the fifth test? Well, the solution of [Test 04](#test-04) seemed to solve all issues, but creates a new one if we actively develop our package.
To solve this issue we need to fix for development our install to command. We install the package as editable.

To install package in development and run the script:

<details><summary markdown="span">**bash**</summary>
```bash
cd test_05
python -m venv .venv
source .venv/bin/activate
pip install -e .
python my_package/run.py | grep $USER
```
</details>

<details><summary markdown="span">**powershell**</summary>
```powershell
cd test_05
python -m venv .venv
.venv/Script/Activate.ps1
pip install -e .
python my_package/run.py | Select-String $env:username
```
</details>

### Excepted Result

```bash
run                            | <repo_path>/test_05/my_package/run.py
__editable___my_package_1_0_0_finder | <repo_path>/test_05/.venv/lib/python3.12/site-packages/__editable___my_package_1_0_0_finder.py
pip                            | <repo_path>/test_05/.venv/lib/python3.12/site-packages/pip/__init__.py
```

### Comparison

Now instead of the installed package, we have an editable package finder installation, which points at our development environment.
