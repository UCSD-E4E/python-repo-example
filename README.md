# python-repo-example
Example Python Package Repository.  This repository serves as an example of how to set up a Python repository for UCSD Engineers for Exploration.

## .vscode
This folder should contain at least a `launch.json` file that provides entry points into the package.  This could be entry points to example programs, typical debug entry points, etc.  Ideally, this will also contain a `settings.json` with folder specific VS Code settings.

All standard invocations that developers should be using MUST be saved into a `launch.json` entry.

## Python Packages
Almost all code should be organized into packages.  This facilitates easy code reuse.  See https://packaging.python.org/en/latest/ for more information on how to use packages in Python.

## tests
Tests should ideally be kept in an isolated folder.  This example uses `pytest`, see https://docs.pytest.org/en/8.3.x/ for information on how to use `pytest`.

## .gitignore
This is an important file to put into your `git` repositories.  This helps prevent `git` from including unnecessary files into the version control system, such as generated files, environment files, or log files.  Please upgrade this using https://gitignore.io

## Jupyter Notebooks
Jupyter Notebooks are a great way to add interactive reports or documentation.  There is an example here.

## README.md
This is a critical file to include.  This should be an introduction to your repository.  It should be a birds-eye view of what your repo is and how to use it, with links to the appropriate lower-level documentation.

## pyproject.toml
This is the standard way to package Python projects.  This is now structured using Poetry, see https://python-poetry.org/ for tool documentation.

See https://packaging.python.org/en/latest/tutorials/packaging-projects/ and https://docs.python.org/3/distutils/setupscript.html for more information about each tool.

## Installing for developers
Developers should do the following:
```
# Create a virtual environment
python -m venv .venv

# Activate the virtual environment
.venv/Scripts/activate.ps1   # for Windows PowerShell
.venv/Scripts/activate.bat   # for Windows Command Prompt
source .venv/bin/activate    # for bash

# Install in developer mode
poetry install
```

## Installing for end users
End users should do the following:
```
# Create a virtual environment
python -m venv .venv

# Activate the virtual environment
.venv/Scripts/activate.ps1   # for Windows PowerShell
.venv/Scripts/activate.bat   # for Windows Command Prompt
source .venv/bin/activate    # for bash

# Install
pip install .
```