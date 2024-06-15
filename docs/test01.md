---
layout: page
title: "Test 01"
permalink: /test01
---

Very basic setup. We have one package `my_package` and inside one module
`my_module.py`. The module includes one function main, which lists all available
modules at runtime, completely ripped of <https://stackoverflow.com/a/42673938/10985257>

Outside the package, a `run.py` scripts exists, which is the entry point for the test.

Test 01 works perfectly fine with no further actions. This might seem like good
approach, but might lead to other issues, which are better shown by [Test 02](#test-02).

To run the test manual just run

<details><summary markdown="span">**bash**</summary>
```bash
cd test_01
python run.py | Select-String $USER
```
</details>

<details><summary markdown="span">**powershell**</summary>
```bash
cd test_01
python run.py | Select-String $env:username
```
</details>

### Excepted Result

```bash
my_package                     | <repo_path>/test_01/my_package/__init__.py
run                            | <repo_path>/test_01/run.py
```
