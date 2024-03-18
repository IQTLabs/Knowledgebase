# Why use it?
### Dependency Pinning
Python Poetry simplifies multiple aspects of dependency management in Python. The most important job it will perform is dependency pinning. This means that instead of specifying your dependency as `httpx` (which is tacitly latest) it is specified as `httpx==0.23.3` Traditionally this has been painful in Python because you need to look up the version on PyPi (or whatever package repo you are using) and make an appropriate entry in the `requirements.txt` file. Instead with Poetry the command is a simple `poetry add httpx` which handles the lookup for you and makes an appropriate entry in the `pyproject.toml` file.
### Setup
Poetry also handles setup, replacing the deprecated and dangerous `setup.py` convention. So instead of running `python3 -m pip install .` which is tacitly running `setup.py` which contains an arbitrary set of python commands you would use `poetry install` which handles the installation declaratively and by default sandboxes each application into its own virtual environment.

# Installation
Information below comes from [the official documentation](https://python-poetry.org/docs/)

### Macos/Linux
```sh
curl -sSL https://install.python-poetry.org | python3 -
```

### Windows
```
(Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | py -
```
If using a shell that supports them, tab completions can be enabled using the instructions in the documentation.

# Configuration

It is strongly recommended to configure poetry to use virtualenvs inside of a project directory instead of in their default location. to set this configuration use the command:
```sh
poetry config virtualenvs.in-project true
```

# Usage
The following are some common usage patterns for poetry:

### Adding a dependency
**Latest:**
```sh
poetry add <dependency>
```
**Specific version:**
```sh
poetry add <dependency>==<version>
```
OR
```sh
poetry add <dependency>@<version>
```
Please note that version constraints can also be specified using [multiple notations](https://python-poetry.org/docs/dependency-specification/#version-constraints)

**As an optional Extra dpendency:**
```sh
poetry add -E <extra> <dependency>
```
A common use for this pattern is to define development or test 
### Removing a dependency
```sh
poetry remove <dependency>
```

### Installation
```sh
poetry install
```

### Running a script 
```sh
poetry run <script> <args>
```

### Update dependencies
```sh
poetry update
```
This will update the lockfile in accordance with the constraints specified in the `pyproject.toml`

### Regenerate the lockfile
```sh
poetry lock --no-update
```
As an example you might run unit tests using:
```sh
poetry run pytest ./
```