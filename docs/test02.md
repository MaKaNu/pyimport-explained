---
layout: page
title: "Test 02"
permalink: /test02
---

Very similar approach like in [Test 01](#test-01) but this time, the `run.py` is located inside the package `my_package`.

This always results in a `ModuleNotFoundError`.

We can try different approaches:

<details><summary markdown="span">**bash**</summary>
```bash
cd test_02
python my_package/run.py | grep $USER
```
</details>

<details><summary markdown="span">**powershell**</summary>
```powershell
cd test_02
python my_package/run.py | Select-String $env:username
```
</details>

or

<details><summary markdown="span">**bash**</summary>
```bash
cd test_02/my_package
python run.py | grep $USER
```
</details>

<details><summary markdown="span">**powershell**</summary>
```powershell
cd test_02/my_package
python run.py | Select-String $env:username
```
</details>

both approaches will fail.

### Expected Result

```bash
Traceback (most recent call last):
  File "/home/matti.kaupenjohann/test/pyimport/test_02/my_package/run.py", line 1, in <module>
    from my_package.my_mod import main
ModuleNotFoundError: No module named 'my_package'
```
