# python-repo-example
Example Python Package Repository.  This repository serves as an example of how to set up a Python repository for UCSD Engineers for Exploration.

## .vscode
This folder should contain at least a `launch.json` file that provides entry points into the package.  This could be entry points to example programs, typical debug entry points, etc.  Ideally, this will also contain a `settings.json` with folder specific VS Code settings.

## Python Packages
Almost all code should be organized into packages.  This facilitates easy code reuse.  See https://packaging.python.org/en/latest/ for more information on how to use packages in Python.

## tests
Tests should ideally be kept in an isolated folder.  This example uses `pytest`, see https://docs.pytest.org/en/7.0.x/ for information on how to use `pytest`.

## .gitignore
This is an important file to put into your `git` repositories.  This helps prevent `git` from including unnecessary files into the version control system, such as generated files, environment files, or log files.

## Jupyter Notebooks
Jupyter Notebooks are a great way to add interactive reports or documentation.  There is an example here.

## *.code-workspace
This is created by going to `File`->`Save Workspace As` in VS Code.  This allows us to easily open the same development environment across computers and operating systems.  Use this as the root of your development environment.

You'll also notice here that there are some recommended extensions.  This allows everyone on your team to have a consistent toolchain for how to interact with your code.  See https://code.visualstudio.com/docs/editor/extension-marketplace#_workspace-recommended-extensions for instructions for how to configure these.

## README.md
This is a critical file to include.  This should be an introduction to your repository.  It should be a birds-eye view of what your repo is and how to use it, with links to the appropriate lower-level documentation.

## setup.py
This is the original way to package Python projects, which we probably still prefer.  However, in general, if you can, you should probably start using the newer packaging tools (`pyproject.toml`)

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
python -m pip install -e .[dev]
```
# Toolchains
## `conda`
`conda` should be used as the package and environment manager when we require `conda` only packages.

In this case, the following files should be present:
```
environment.yml
conda-win-64.lock
conda-osx-64.lock
conda-linux-64.lock
pyproject.toml
```

Remove the following files:
```
setup.py
```

An example `environment.yml`:
```
name: example_env
channels:
  - defaults
  - anaconda
  - conda-forge

dependencies:
  - python=3.9
  - conda-lock
  - pip
  - pip:
    - numpy
```
Note that it is required to include `conda-lock` in the dependencies.

To create this structure, first define `environment.yml` as you normally would.  Create the environment using `conda env create -f environment.yml`.  Once the environment is created successfully, run `conda activate {environment_name}`.  In the activated environment, run `conda-lock -k explicit`, which will create the `.lock` files.  Add and commit these.

To add a new package, add it into `environment.yml`.  Then, in the activated environment, do the following:
```
conda-lock -k explicit
conda update --file conda-{os}-64.lock
```

To create the environment once all the lock files are created, simply do the following:
```
conda create --file conda-{os}-64.lock
conda activate {env_name}
```
