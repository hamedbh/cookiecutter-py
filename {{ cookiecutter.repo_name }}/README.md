# {{ cookiecutter.project_name }}

{{ cookiecutter.description }}

## Getting started

Having created this project with a cookiecutter you'll need to run `git init` to initialise it as a Git repo. The next steps are contained in the setup script, which will:

1. Create a Python virtual environment with Poetry.
2. Install the required packages as defined in `pyproject.toml`, including your local code under `src`.
3. Install the Git pre-commit hooks defined in `.pre-commit-config.yaml`.
4. Install nbstripout, which prevents notebook outputs being committed in version control.
5. Create an IPython kernel to use with notebooks, called {{ cookiecutter.repo_name }}.
6. Create the `.env` file to use for managing env vars.

To run the setup script:

```bash
./setup_project
```

Running that script should just be a one-off step.

## General principles

This template makes certain assumptions about how you'll organise and execute your project. It borrows heavily from [Cookiecutter Data Science](http://drivendata.github.io/cookiecutter-data-science/).

- The targets (datasets, models, plots, etc.) are defined and built using the `Makefile`. If you're new to [GNU Make](https://www.gnu.org/software/make/) it's very well-documented online. Karl Broman's [minimal make tutorial](https://kbroman.org/minimal_make/) is a great way to get started.
- The Python scripts are all under `src` and use the [Python package structure](https://packaging.python.org/en/latest/tutorials/installing-packages/).
- Data are stored in `data` and will not be managed through version control. Likewise for any models you build: they are stored in `models`.
- The project template uses the [ruff](https://docs.astral.sh/ruff/) package for linting and formatting. Running `make format` **will** reformat your code, in place, without asking. Run `poetry run ruff format --diff` to see what would be changed.

## Managing Python dependencies

Use Poetry to add dependencies to, or remove them from, the project.

```bash
# Add a dependency
poetry add polars
# Add a dev dependency
poetry add ruff -G dev
# Remove dependency
poetry remove polars
# Remove dev dependency
poetry remove ruff -G dev
```

## Project documentation

Add docs and guidance under the `references` directory. There is already a `METHODOLOGY.md` document there with section headings.

## Project targets

The targets are defined in `Makefile`: a first target, `data`, is there as an example. To view all available commands just call `make` from within the project.

## Python scripts

The script at `src/data/make_dataset.py` is useful as a starter, illustrating how to use the [click package](https://pypi.org/project/click/) to control and validate the arguments to your functions.

## Project structure

```
├── Makefile                        <- Makefile with commands like `make data`
├── README.md                       <- The top-level README for developers using this project.
├── data
│   ├── interim                     <- Intermediate data that has been transformed.
│   ├── processed                   <- The final, canonical data sets for modeling.
│   └── raw                         <- The original, immutable data dump.
│
├── models                          <- Local folder to keep serialised models
├── notebooks                       <- Jupyter notebooks. Naming convention is a number (for ordering),
│                                      the creator's surname, and a short `-` delimited description, e.g.
│                                      `1.0_smith_initial-data-exploration`.
│
├── references                      <- Data dictionaries, manuals, and all other explanatory materials
|   └── METHODOLOGY.md              <- Defines methodological decisions
│
├── outputs                         <- Generated analysis and results
│   └── figures                     <- Generated graphics and figures to be used in reporting
│
├── pyproject.toml                  <- Settings for the whole project
|
├── src                             <- Source code for use in this project.
│   ├── __init__.py                 <- Makes src a Python module
│   ├── locations.py                <- Includes constants for the path of various folders
│   │
│   ├── data                        <- Scripts to download or generate data
│   ├── features                    <- Scripts to turn raw data into features for modeling
│   ├── models                      <- Scripts to train models and make predictions
│
├── tests                           <- Code defining tests for code under `src`. Filenames need
|                                      to have a `test_` prefix to be run by the test runner
├── .pre-commit-config.yaml         <- Configuration for pre-commit hooks
├── setup_project                   <- shell script that prepares repo for development (see 
|                                      details above)
├── .gitignore                      <- Exclusions from source control
```

## Environment variables

The `setup_project` script creates a `.env` file, which you should update as needed, e.g. with API keys. Then you can refer to those variables in your Python scripts easily:

```python
import os
from dotenv import load_dotenv, find_dotenv

# find .env automagically by walking up directories until it's found
dotenv_path = find_dotenv()
# load up the entries as environment variables
load_dotenv(dotenv_path)
api_key = os.getenv["API_KEY"]
```

You can use dotenv in IPython. By default, it will use find_dotenv to search for a `.env` file:

```python
%load_ext dotenv
%dotenv
```

Please do not use environment variables for project paths. Instead, use `src/locations.py`.
