# MLAS Docs Generator

If you have would like to automatically generate

> `python -m venv env`

> `. .\env\Scripts\activate`

> `pip install mkdocs-material`

> `pip install mkdocstrings`

> `mkdocs serve`

> `mkdocs gh-deploy`

The automatically generated documentation for this repository is available at:

https://Machine-Learning-Academy-of-Sciences.github.io/template-python-docs-generator/

# How to avoid pip installing everything into the environment

Mkdocs scans all of the *.py* files and it uses a Python handler to attempt to import
all of the modules.

Therefore, the virtual python env in which the mkdocs is installed has to have all of the other modules imported in all of the *.py* files

* so for example if **pandas** is not installed and you have `import pandas as pd` in file1.py, then `mkdocs serve` won't work.
* One way to solve this is to use `sys.modules["pandas"] = mock()` as explained in https://mkdocstrings.github.io/handlers/python/#mocking-libraries