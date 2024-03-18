# Why use it?
---
### Pre-Commit Hooks
Git supports a variety of [hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks). Client-side pre-commit hooks run on your development machine before a commit actually happens to your local repo. These hooks live in your repo's `.git/hooks` directory. It is pre-populated with a variety of sample scripts. In practice these scripts can be any valid bash script. However, by necessity, these scripts live outside of Git's version control workflow which means that they aren't especially convenient or portable.
### pre-commit the tool
[pre-commit](https://pre-commit.com) is a tool designed to make it easy for developers to version control, run, and share pre-commit scripts. It runs a set of scripts defined by a `.yaml` file on changed files prior to a commit happening. If the scripts fail, it will prevent the commit from occurring.

# Installation
---
Information is based on [the official documentation](https://pre-commit.com/#installation) but uses [pipx](https://github.com/pypa/pipx) instead of `pip` because `pipx` installs the application and all of it's dependencies inside of a sandbox, so you do not have to worry about an installed application breaking your python environment.
### Macos/Linux/Windows
```sh
pipx install pre-commit
```
# Usage
---
Upon cloning a repo containing an existing `.pre-commit-config.yaml` file, or after creating one install hook scripts with:
```sh
pre-commit install
```
to see what the results of running against currently uncommited files:
```sh
pre-commit run
```

to see the results of a run against all files in the current repo:
```sh
pre-commit run --all-files
```

# Configuration
---
Configuration is handled by the file `.pre-commit-config.yaml` . a basic starting configuration can be found below.
## Starting config
**Note:** this config assumes a python project. Entries may change for projects in other languages but the basic structure remains the same
```yml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.0.1
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-case-conflict
      - id: check-json
      - id: pretty-format-json
        args: ['--autofix']
      - id: double-quote-string-fixer
      - id: check-yaml
  - repo: https://github.com/asottile/reorder_python_imports
    rev: v2.6.0
    hooks:
      - id: reorder-python-imports
  - repo: https://github.com/python-poetry/poetry
    rev: 1.5.1
    hooks:
    -   id: poetry-check
    -   id: poetry-lock
        args: [--no-update]
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.0.291
    hooks:
      - id: ruff
        args: [--respect-gitignore]
  - repo: https://github.com/psf/black
    rev: 23.9.1
    hooks:
      - id: black
        args: [-q, --check]
  - repo: local
    hooks: 
      - id: trufflehog 
        name: TruffleHog 
        description: Detect secrets in your data. 
        entry: bash -c 'docker run --rm -i -v "$PWD:/pwd" trufflesecurity/trufflehog:latest git file:///pwd --since-commit HEAD --fail --only-verified --json'
        language: system 
        stages: ["commit", "push"]