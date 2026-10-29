# Creating Python Packages
In this final chapter, we will introduce how to generate Python packages. 
Packages are a way to organize and distribute Python code. They can be used 
to share code with others, or to create reusable components for your own projects.
For more on how to write, distribute and install Python packages, we 
recommend reading the [Python Packaging User Guide](https://packaging.python.org/).
Here we will limit ourselves to a few general ideas that will get you started
and also will be useful to understand packages written by others.

## Directory structure
To generate a Python package, you will need to create a directory structure
and write a few files. The basic structure of a Python package is as follows:
```
my_package/
├── __init__.py
├── module1.py
├── module2.py
└── ...
```
Although it can be empty, the `__init__.py` file is essential for Python to recognize 
the directory as a package. It can also be used to import specific modules from 
the package.  Each module can contain any type of Python code, such as functions, 
classes, and variables. For example, the following `__init__.py` file would import 
the `module1` and `module2` modules from the `my_package` package:
```python
from .module1 import function1, class1
from .module2 import function2, class2
```
This would allow you to import these modules from anywhere in your code using
the following syntax:
```python
import my_package

# Call a function from the module1 module
my_package.function1()

# Create an instance of a class from the module2 module
my_package.class2()
```

If your package depends on other Python packages, you can specify these 
dependencies in the `setup.py` file. This will ensure that you have everything
you need for your code to run. To specify a dependency, you can use the 
`install_requires` keyword in the `setup.py` file. For example, the following
`setup.py` file would specify a dependency on the numpy package:
```python
from setuptools import setup

setup(
    name="my_package",
    version="1.0.0",
    install_requires=["numpy"],
)
```
As you can see, here we are making use of the 
[`setuptools`](http://pypi.python.org/pypi/setuptools) package.
When your package is installed, `numpy` will also be installed automatically.

### The modern alternative: `pyproject.toml`
You will find `setup.py` files in many existing packages, but nowadays the
recommended way of describing a package is a `pyproject.toml` file. Instead
of a Python script, it is a plain configuration file written in the
[TOML](https://toml.io/) format. It sits in the project folder, next to (not
inside) the package directory:
```
my_project/
├── pyproject.toml
├── README.md
└── my_package/
    ├── __init__.py
    ├── module1.py
    └── module2.py
```
The equivalent of the `setup.py` file above, with a few useful additions, is:
```toml
[build-system]
requires = ["setuptools>=61"]
build-backend = "setuptools.build_meta"

[project]
name = "my_package"
version = "1.0.0"
description = "A short description of what the package does"
readme = "README.md"
requires-python = ">=3.9"
dependencies = ["numpy"]

[project.scripts]
my_command = "my_package.module1:main"
```
The `[build-system]` table tells `pip` which tool builds the package (here,
again, `setuptools`). The `[project]` table contains the name, the version
and the dependencies, which play the role of `install_requires`. The optional
`[project.scripts]` table creates a command, `my_command`, that runs the function
`main()` in `my_package/module1.py`. This is how you turn your code into a program
you can run from the terminal.

To install the package, run the following from the `my_project/` folder:
```
pip install -e .
```
The `-e` ("editable") option means that changes you make to the code are used
straight away, without reinstalling. This is what you want while you are still
developing the package. Once installed, you can `import my_package` from any
folder, notebook or script.

You can include many other things in your package. We recommend writing a `README`
file, where you can describe what the package does, who are the developers
and provide some installation instructions. Additionally, it is often useful
to provide a [`LICENSE`](https://choosealicense.com/), 
so that it is clear to users which conditions apply to
use, modify and redistribute the code. For example, below you can see the
text that you should include if you want to use the short and simple permissive
MIT license
```
MIT License

Copyright (c) [year] [fullname]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Deployment
Once you have created your package structure and written your code, you can generate the distribution 
archives with the [`build`](https://build.pypa.io/) package. Install it
with `pip install build` and run the following from the `my_project/` folder:
```
python -m build
```
This works both with `pyproject.toml` and with `setup.py`. In older
instructions you may find the command `python setup.py sdist bdist_wheel`
instead, which is deprecated.

This will create two files in the `dist/` directory:
* `my_package-1.0.0.tar.gz`: This is the source distribution archive. It can be 
used to install the package on any system that has Python installed.
* `my_package-1.0.0-py3-none-any.whl`: This is the wheel distribution archive. 
It is a pre-compiled binary archive that can be installed on any system that 
has Python 3 installed.

To upload your package to the Python Package Index (PyPI), you can
use the following command:
```
twine upload dist/*
```
Here we are using the Twine utility for publishing the package. This
command will upload the source and wheel distribution archives to PyPI. 
Once your package is uploaded, it can be installed by anyone using the following
command:
```
pip install my_package
```

## Packaging with conda
In this course, we have been using the Anaconda Python distribution. 
Anaconda has its own package manager for Python. It can be used to install,
manage, and update Python packages. To package a Python package with Conda, 
you will need to create a `meta.yaml` file. This file describes the package 
and its dependencies. The basic structure of a meta.yaml file is as follows:
```python
package:
  name: my_package
  version: 1.0.0

build:
  number: 0

requirements:
  build:
    - python
    - setuptools
    - wheel

  run:
    - numpy
```
The `package` section specifies the name and version of the package.
The `build` section specifies the build number of the package. This 
number is incremented each time the package is rebuilt. The requirements 
section specifies the dependencies of the package for either building or
running it. 

Once you have created a `meta.yaml` file, you can build the package using
the following command:
```
conda build .
```
To install the package, you can use the following command:
```
conda install my_package
```
To publish a Conda package to Anaconda.org, you will need to install the 
anaconda-client package:
```
conda install anaconda-client
```
Once you have installed the anaconda-client package, you can log in to
Anaconda.org using the following command: 
```
anaconda login
```
To publish your package to Anaconda.org, you can use the following command:
```
anaconda upload my_package.tar.bz2
```
This will upload the Conda package to Anaconda.org. Once the package is 
uploaded, it can be installed by anyone using the following command:
```
conda install -c anaconda my_package
```

## Testing and continuous integration
It is important to test your package thoroughly before releasing it, and
to keep testing it every time you change it. You do this by writing a
*test suite*: a collection of small functions that check that your code
does what you expect.

### Writing tests with `pytest`
The most widely used testing framework in Python is
[`pytest`](https://docs.pytest.org/). Install it with `pip install pytest`.
Tests live in a `tests/` folder in your project, next to the package:
```
my_project/
├── pyproject.toml
├── README.md
├── my_package/
│   ├── __init__.py
│   └── module1.py
└── tests/
    └── test_module1.py
```
Test files must be called `test_*.py`, and each test is a function whose
name starts with `test_`. Inside it you use plain `assert` statements.
For example, if `module1.py` contains a function `add(a, b)`, the file
`tests/test_module1.py` could be:
```python
import pytest
from my_package.module1 import add

def test_add():
    assert add(1, 2) == 3

def test_add_floats():
    # floating point numbers should never be compared with ==
    assert add(0.1, 0.2) == pytest.approx(0.3)
```
To run all the tests, type the following from the `my_project/` folder:
```
pytest
```
`pytest` finds the test files by itself, runs every test and reports which
ones passed and which ones failed (and why). If any test fails, the command
exits with a non-zero status code, which is what automated tools use to
detect the failure.

Python also comes with its own testing framework,
[`unittest`](https://docs.python.org/3/library/unittest.html), where tests
are methods of a subclass of `unittest.TestCase`:
```python
import unittest

class MyTestCase(unittest.TestCase):
    def test_sum(self):
        self.assertEqual(1 + 2, 3)

if __name__ == '__main__':
    unittest.main()
```
These tests are run with `python -m unittest discover`. You will find
`unittest` in many existing packages, and `pytest` can also run them.

### Test coverage
The *coverage* of a test suite is the fraction of the lines of your code
that are executed when the tests run. Lines that are never executed are
never tested. With the `pytest-cov` plugin (`pip install pytest-cov`) you
can measure it as follows:
```
pytest --cov=my_package
```
This prints a table with the percentage of lines covered in each module.
Aim for high coverage, but remember that 100% coverage does not mean that
your code is correct: it only means that every line was run at least once.

### Continuous integration
Running the tests on your own computer is a good start, but it is easy to
forget, and your computer may have things installed that your users do not.
*Continuous integration* (CI) solves both problems: every time you push
changes to your repository, a clean machine in the cloud installs your
package from scratch and runs the test suite. If something breaks, you
find out immediately.

If your code is on GitHub, the simplest option is
[GitHub Actions](https://docs.github.com/en/actions). A CI *workflow* is a
YAML file inside the `.github/workflows/` folder of your repository. The
following `.github/workflows/tests.yml` runs the tests with four different
versions of Python on every push and every pull request:
```yaml
name: tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: ["3.10", "3.11", "3.12", "3.13"]
    steps:
      - uses: actions/checkout@v7
      - uses: actions/setup-python@v7
        with:
          python-version: ${{ matrix.python-version }}
      - name: Install the package and the test tools
        run: pip install -e . pytest pytest-cov
      - name: Run the tests
        run: pytest --cov=my_package
```
The `steps` are what you would type yourself on a new computer: get the
code, install Python, install the package and run `pytest`. A step either
runs a shell command (`run:`) or uses an *action* (`uses:`), a ready-made
step published by someone else in a GitHub repository. Here
[`actions/checkout`](https://github.com/actions/checkout) copies the code
of your repository into the cloud machine, which starts empty every time,
and [`actions/setup-python`](https://github.com/actions/setup-python)
installs the version of Python given in `with:`. The `@v7` at the end
fixes the major version of the action, so that a future release that
changes its behaviour does not break your workflow without warning. The
`matrix` repeats the whole job for each Python version, and
`${{ matrix.python-version }}` is replaced by each of them in turn. You
can follow the result of each run in the *Actions* tab of your repository
on GitHub.

In fact, the book you are reading is built in exactly this way: every time
we push a change, a GitHub Actions workflow
([`deploy.yml`](https://github.com/KimikaTeorikoa/python-notes-tccm/blob/master/.github/workflows/deploy.yml))
runs all the code in these notes and publishes the web page.

### Badges
The result of the CI is usually advertised with a *badge* at the top of
the `README.md` file of the repository. This is the live badge of the
workflow that builds this book:

![build](https://github.com/KimikaTeorikoa/python-notes-tccm/actions/workflows/deploy.yml/badge.svg)

A badge is just an image, so you add it to your `README.md` with a
Markdown line like this one:
```
![tests](https://github.com/<user>/<repository>/actions/workflows/tests.yml/badge.svg)
```
Many repositories show a whole row of badges, which tell a visitor at a
glance whether the code works and how to get it:

![tests](https://img.shields.io/badge/tests-passing-brightgreen)
![coverage](https://img.shields.io/badge/coverage-87%25-green)
![python](https://img.shields.io/badge/python-3.10%20%7C%203.11%20%7C%203.12%20%7C%203.13-blue)
![pypi](https://img.shields.io/badge/pypi-v1.0.0-blue)
![license](https://img.shields.io/badge/license-MIT-lightgrey)

These examples are static images made with [shields.io](https://shields.io),
which can also generate badges that update automatically (for example, with
the latest version of your package in PyPI).

### Other things CI can do for you
Running the tests is only the beginning. Some other common uses are:
* **Coverage reports**: services like [Codecov](https://about.codecov.io/)
  or [Coveralls](https://coveralls.io/) collect the coverage of every CI run,
  show which lines are not tested and provide a coverage badge.
* **Linting and formatting**: [`ruff`](https://docs.astral.sh/ruff/) checks
  your code for common mistakes and style problems in a fraction of a second.
  With [`pre-commit`](https://pre-commit.com/) these checks also run on your
  computer every time you commit.
* **Publishing**: a workflow can build your package with `python -m build`
  and upload it to PyPI every time you create a new release, using PyPI's
  [trusted publishing](https://docs.pypi.org/trusted-publishers/), so you
  never have to handle passwords or tokens.
* **Keeping dependencies up to date**: GitHub's
  [Dependabot](https://docs.github.com/en/code-security/dependabot) opens
  pull requests when new versions of your dependencies are released, and
  your CI tells you whether your code still works with them.
* **Documentation**: [Read the Docs](https://readthedocs.org/) builds and
  hosts the documentation of your package every time you push.
* **Conda packages**: if your package is in
  [conda-forge](https://conda-forge.org/), its CI builds the conda packages
  for all platforms for you.

Other platforms offer the same functionality. If your code is hosted on
GitLab, for example, the equivalent of GitHub Actions is
[GitLab CI/CD](https://docs.gitlab.com/ee/ci/), configured with a
`.gitlab-ci.yml` file.
