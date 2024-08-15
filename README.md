# Cookiecutter Data Science

A logical, reasonably standardised, but flexible project structure for doing and sharing data science work.

## Guiding principles

- Keep projects consistent.
- Reduce friction when starting a project.
- Allow some flexibility, since not all projects are alike.
 
## Requirements
 - Python 3.5+
 - [Cookiecutter Python package](http://cookiecutter.readthedocs.org/en/latest/installation.html) >= 1.4.0. Install this with pip in the normal way:

``` bash
$ pip3 install cookiecutter
```

## Starting a new project
Simply run:

```bash
cookiecutter git@github.com:hamedbh/cookiecutter-py-datasci.git 
```

You'll then be prompted to enter certain info about your project:

- `project_name`: self-explanatory, a decent name for your project.
- `repo_name`: by default this will be `project_name` in lower case with spaces replaced by underscores.
- `author_name`: your name and/or that of your team.
- `description`: in a sentence or two, what the project is about.
- `python_version`: the path to the Python executable you want to use for this project. The default is `python3`.
- `virtualenv_location`: where you want your Python virtual environment to be. By default this is `./.venv`, i.e. it will be inside your project directory in a subdirectory called `.venv`.
