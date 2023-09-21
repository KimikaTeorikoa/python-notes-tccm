# Using libraries

Python is a versatile and powerful programming language known for its simplicity and readability. 
One of the primary reasons for Python's popularity is its extensive library ecosystem. In this sense, 
Python libraries are collections code and functions that can be easily imported into your programs. 
These libraries cover many functionalities, making possible to perform complex tasks without investing time
 on coding what has been coded already by someone else.

Using libraries has many advantages: 

**1. Code Reusability:** Python libraries contain well-tested and optimized code for various tasks, such as data 
manipulation, mathematical calculations, web development, and more. 

**2. Increased Productivity:** Libraries offer a wealth of functionality that accelerates development. You can access 
powerful tools, algorithms, and data structures without writing them from scratch.

**3. Community Support:** Python's vast and active community constantly develops and maintains libraries. This ensures that libraries stay up-to-date, reliable, and compatible with the latest versions of Python.

**4. Ecosystem Integration:** Many libraries are integrate with each other, allowing you to combine their capabilities. 
For example, you can use libraries like Matplotlib for data visualization along with Pandas for data analysis.

### How to Import Libraries in Python

Importing a library in Python is a straightforward process, involving the `import` statement. 

**Standard Library** 

Python comes with a rich standard library that covers fundamental functionalities. You can import standard library
modules like this:

   ```python
   import module_name
   ```

   For example, to import the `math` module for mathematical operations:

   ```python
   import math
   ```

   You can then use functions and classes from the `math` module, such as `math.sqrt()` for square root calculations.

**Third-Party Libraries** 

To use third-party libraries, you'll need to install them first (usually via `pip` or `conda`). Once installed, you can
import them using the `import` statement:

   ```python
   import library_name
   ```

   For instance, to import the popular NumPy library for numerical operations:

   ```python
   import numpy as np  # Using the 'np' alias for convenience
   ```

   Using an alias like `np` is common for libraries with long names, as it makes code more readable.

**Specific Functions or Classes** 

A quick way to include all the functions and classes in you code you may use:

```python
from library_name import *
```

   This approach allows you to use the imported items __without specifying the library name__.

On the other hand, if you only need specific functions or classes from a library, you can import them directly:

   ```python
   from library_name import function_name, class_name
   ```

For instance

   ```python
   from math import sqrt
   ```

   Now, you can use `sqrt()` directly without referencing the `math` module.

### Most common libraries in Python

Among the huge variety of libraries in the Python ecosystem, let us remark the most basic, which are commonly used in 
many transversed areas

#### sys 

The `sys` module provides access to some variables used or maintained by the interpreter and to functions that interact
strongly with the interpreter. It is always available. The `sys` module can be used to obtain information about the
Python runtime environment, such as the version of the interpreter, the command-line arguments passed to the program,
and the amount of free memory on the system. The `sys` module can also be used to control the behavior of the
interpreter, such as setting the recursion limit and exiting the interpreter.

##### Common uses of the sys module

* **Get information about the Python runtime environment:**
    * `sys.version`: Returns the version number of the Python interpreter.
    * `sys.argv`: Returns a list of the command-line arguments passed to the program.
    * `sys.gettotalrefcount()`: Returns the amount of free memory on the system.

* **Control the behavior of the interpreter:**
    * `sys.exit()`: Exits the Python interpreter.
    * `sys.setrecursionlimit()`: Sets the maximum depth of the Python interpreter stack.
    * `sys.stdout.write()`: Writes a string to standard output.
    * `sys.stdin.readline()`: Reads a line from standard input.

#### Example

```python
import sys

# Get the version number of the Python interpreter
print(sys.version)

# Exit the Python interpreter
sys.exit()
```

* #### os

The `os` module provides a portable way of using operating system dependent functionality. It provides functions for
creating and removing files and directories, navigating the file system, changing the current working directory, 
and more.

#### Common uses of the os module

* **Create and remove files and directories:**
    * `os.mkdir()`: Creates a new directory.
    * `os.rmdir()`: Removes a directory.
    * `os.open()`: Opens a file for reading or writing.
    * `os.close()`: Closes a file.
    * `os.remove()`: Removes a file.
* **Navigate the file system:**
    * `os.getcwd()`: Returns the current working directory.
    * `os.chdir()`: Changes the current working directory.
    * `os.listdir()`: Returns a list of the files and directories in the current directory.
    * `os.path.join()`: Joins two or more path components together.
* **Other common functions:**
    * `os.getenv()`: Gets the value of an environment variable.
    * `os.system()`: Executes a shell command.
    * `os.sleep()`: Suspends execution for a specified period of time.

#### Example

Here is an example of how to use the `os` module to create a new directory:

```python
import os

# Create a new directory called "my_dir"
os.mkdir("my_dir")
```

Here is an example of how to use the os module to read the contents of a directory:

```python
import os

# Get a list of the files and directories in the current directory
files_and_dirs = os.listdir()

# Print the list of files and directories
for file_or_dir in files_and_dirs:
    print(file_or_dir)
```

* #### `argparse` 

Writing user-friendly command-line interfaces (CLIs) is easy thanks to the `argparse` module. The `argparse`module also generates
help and usage messages, providing issue error when invalid arguments are given.

`argparse` is a Python standard library module that simplifies the process of creating powerful and user-friendly
command-line interfaces (CLIs) for your Python scripts or programs. It allows you to define and customize command-line
options, arguments, and help messages, making it easier for users to interact with your code through the terminal.

`argparse` offers several advantages:

1. **User-Friendly Interface:** It provides a user-friendly way for users to provide input to your scripts or programs
via the command line. 
2. **Validation and Error Handling:** `argparse` automatically performs validation and error handling for the
command-line arguments. It checks for required arguments, valid choices, and data types.
3. **Flexibility:** You can define various types of arguments, including positional arguments, optional arguments
(flags), and arguments with values. 
4. **Documentation Generation:** `argparse` can automatically generate help messages and documentation for your script
based on the argument definitions you provide.

In order to create an CLI we first need to use the __ArgumentParser__ class of the `argparse` module.

```python
import argparse

parser=argparse.ArgumentParser(description=’Hello world! This is my custom command-line program’, 
usage=’%(prog)s [options]’)
```

The __description__ parameter describes the program to help the user understand. In contrast,
the parameter __usage__ gives the user a usage message when they run any command with the “help” flag.

To add more parameters to the parser, we can add them using the `add_argument()` method.

```python
parser.add_argument(argument_default=None);
parser.add_argument(epilog=’Information displayed at the end of the help message);
```

The __argument_default__ sets the default value for all arguments. The __epilog__
which displays a text at the end of the help message.

Once it is done, the command line arguments are parsed using the __parse_args()__ method.

#### Basic Usage

A basic example of how to use `argparse` in a Python script

```python
import argparse

# Create an ArgumentParser object
parser = argparse.ArgumentParser(description='A simple command-line tool.')

# Add positional argument(s)
parser.add_argument('input_file', help='Input file name')

# Add optional argument(s)
parser.add_argument('--output', '-o', help='Output file name')

# Parse the command-line arguments
args = parser.parse_args()

# Access the values of the arguments
input_file = args.input_file
output_file = args.output
```

To run the script we type

```python
python script.py input.txt --output output.txt
```

where `input.txt` is provided as the value for the input_file positional argument.
and `--output` stands for an optional argument, being `output.txt` is provided as its value.

* #### `shutil

<!--## String Manipulation -->	
<!--## Numpy (different Section ?) -->	
<!--## Introduction	-->
<!--## Input/Output	-->
<!--## Arrays	-->
<!--## Operations -->