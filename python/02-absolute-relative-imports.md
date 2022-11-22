# Absolute and Relative Imports

## Why do you have to import?
- Import helps in porting functionality from one file to another or get functionality from a module.
- If we pip install a file we still need to import it before using it.

A module is a python file with `.py` extension.
Package is collection of modules in a folder.

When you import something python has couple of places to look for
- First it will check in `sys.modules` cache, that is everything that is imported.
- Then checks in standard library
- `sys.path` list of directories usually includes current directory.

If it did not find in any of these locations then it will throw `ModuleNotFound`

## Ways of importing

`import csv` 
Imports the entire csv module.

`from flask import Flask`
Import specific functionality from a module

`import pandas as pd`
Import entire function as renaming it to an alias.

Import styling #python_import_styling
```
# Standard library imports first
import os
import datetime

# Third party imports next
from flask import Flask
from flask_rest import Api
from flask_sqlalchemy import SQLAlchemy

# Local imports
from Local_module import local_class
```

