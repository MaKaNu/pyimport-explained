---
layout: page
title: "Test 03"
permalink: /test03
---

We still have the run script inside `my_package`, but this time we only import via relative import.
While this might seems to be solution, this might cause trouble further down the structure.
The import does not anticipate the actual package and it is basically a module-level and not a package-level import.

To run Test 03:

<details><summary markdown="span">**bash**</summary>
```bash
cd test_03
python my_package/run.py | grep $USER
```
</details>

<details><summary markdown="span">**powershell**</summary>
```powershell
cd test_03
python my_package/run.py | Select-String $env:username
```
</details>

### Expected Result

```bash
run                            | <repo_path>/test_03/my_package/run.py
```

### Comparison

By comparing the result with [Test 01](/test01) the difference is directly present, we are seeing the `run.py` script but this time not the package.
