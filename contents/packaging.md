# Creating Python Packages
In this final chapter, we will introduce how to generate Python packages. 
Packages are a way to organize and distribute Python code. They can be used 
to share code with others, or to create reusable components for your own projects.

To generate a Python package, you will need to create a directory structure and write a few files. 
The basic structure of a Python package is as follows:
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
When your package is installed, `numpy` will also be installed automatically.

Once you have created your package structure and written your code, you can generate the distribution 
archives using the following command:
```python
python setup.py sdist bdist_wheel
```

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

## Testing your code
It is important to test your package thoroughly before releasing it. 
You can do this by writing a test suite. A test suite is a collection of
tests that are used to verify the functionality of your package.

You can use any Python testing framework to write a test suite. 
Some popular testing frameworks include unittest, pytest, and nose.
unittest is the default Python testing framework. It is a simple and 
easy-to-use framework that provides a number of features for writing 
and running tests. To write a unittest test, you need to create a 
subclass of the unittest.TestCase class. Each test is defined as a 
method of the subclass. The name of the test method must start with 
the prefix test_.

Within the test method, you can use the various assertion methods
provided by unittest to verify the expected behavior of your code. 
For example, the following test method uses the assertEqual() 
method to verify that the sum of two numbers is equal to a third number:
import unittest

```python
class MyTestCase(unittest.TestCase):
    def test_sum(self):
        self.assertEqual(1 + 2, 3)

if __name__ == '__main__':
    unittest.main()
```

Once you have written a test suite, you can run it using the following command:
```python
python -m unittest discover
```
This will run all of the tests in your test suite. If any of the tests fail, 
the command will exit with a non-zero status code.

You can calculate the test coverage for your package using the following command:
```
python -m coverage run -m unittest discover
python -m coverage report
```
This will generate a report that shows how much of your code is covered by your tests.



