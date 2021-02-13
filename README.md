# MLAS Docs Generator

```bash
python -m venv env
. env/Scripts/activate
pip install mkdocs-material
pip install mkdocstrings
mkdocs serve
```


# Caveat

Mkdocs scans all of the *.py* files and it uses a Python handler to attempt to import
all of the modules. Technically the only 2 libaries needed to generate the documentation are

```bash
pip install mkdocs-material
pip install mkdocstrings
```

but, for some reason, unless every library is installed int he same python environment, the docs won't get generated. One workaround is below:

Therefore, the virtual python env in which the mkdocs is installed has to have all of the other modules imported in all of the *.py* files

* so for example if **pandas** is not installed and you have `import pandas as pd` in file1.py, then `mkdocs serve` won't work.
* One way to solve this is to use `sys.modules["pandas"] = mock()` in mkdoc.yml as explained in https://mkdocstrings.github.io/handlers/python/#mocking-libraries

## How to deploy to github actions:

After ensuring that ```mkdocs serve``` works as expected, create a file called **.github/workflows/ci.yml**
with
```
name: ci
on:
  push:
    branches:
      - master
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: 3.x
      - run: pip install mkdocs-material
      - run: pip install mkdocstrings
      - run: mkdocs gh-deploy --force```

and push the changes to Github, and it should automatically generate the corresponding GitHub Page with URL

https://Machine-Learning-Academy-of-Sciences.github.io/template-python-docs-generator/