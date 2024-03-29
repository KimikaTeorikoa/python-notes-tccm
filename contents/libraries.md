# Using libraries
As we have already said, Python is known for its simplicity and readability. 
One of the primary reasons for Python's popularity is its extensive library 
ecosystem. Python libraries are collections of code and functions that can
 be easily imported into your programs. These libraries cover many 
functionalities, making possible to perform complex tasks without investing time
 on coding what has been coded already by someone else.

Using libraries has many advantages: 

1. **Code Reusability:** Python libraries contain well-tested and optimized
 code for various tasks, such as data manipulation, mathematical calculations,
 web development, and more. 

2. **Increased Productivity:** Libraries offer a wealth of functionality 
that accelerates development. You can access powerful tools, algorithms, and
 data structures without writing them from scratch.

3. **Community Support:** Python's vast and active community constantly develops
 and maintains libraries. This ensures that libraries stay up-to-date, 
reliable, and compatible with the latest versions of Python.

4. **Ecosystem Integration:** Many libraries are integrate with each other, 
allowing you to combine their capabilities. For example, you can use libraries 
like Matplotlib for data visualization along with Pandas for data analysis.

## Importing libraries
Importing a library in Python is a straightforward process, involving the `import` statement. 


Python comes with a rich **standard library** that covers fundamental functionalities. 
You can import standard library modules like this:

```python
import module_name
```

For example, to import the `math` module for mathematical operations:

```python
import math
```

You can then use functions and classes from the `math` module, such as `math.sqrt()` 
for square root calculations. To learn what is available in the standard library 
you can go to the [official Python documentation](https://docs.python.org/3/library/index.html).
To use **third-party libraries**, you'll need to install them first (more on this at the end of this chapter). 


Once installed, you can import them using the `import` statement.
For instance, to import the popular NumPy library for numerical operations:

```python
import numpy as np  
```

Using an **alias** like `np` is common for libraries with long names, as it 
makes code more readable.

A quick way to include all the functions and classes in you code you may use:
```python
from library_name import *
```
This approach allows you to use the imported items *without specifying the library
 name*. Although you are likely to find this syntax in your programming journey,
it is not recommended.

On the other hand, if you only need specific functions or classes from a library, 
you can import them directly:
```python
from library_name import function_name, class_name
```

For instance

   ```python
   from math import sqrt
   ```

   Now, you can use `sqrt()` directly without referencing the `math` module.

## Useful modules from the standard library 
Among the huge variety of libraries in the Python ecosystem, let us remark some of
the most basic, which are commonly used in many areas

### `sys` 
The `sys` module provides access to some variables used or maintained by the
 interpreter and to functions that interact strongly with the interpreter. 
It is always available. The `sys` module can be used to obtain information 
about the Python runtime environment, such as the version of the interpreter, 
the command-line arguments passed to the program, and the amount of free memory
 on the system. The `sys` module can also be used to control the behavior of the
interpreter, such as setting the recursion limit and exiting the interpreter.

Some useful calls are

* **Get information about the Python runtime environment:**
    * `sys.version`: Returns the version number of the Python interpreter.
    * `sys.argv`: Returns a list of the command-line arguments passed to the program.
    * `sys.gettotalrefcount()`: Returns the amount of free memory on the system.

* **Control the behavior of the interpreter:**
    * `sys.exit()`: Exits the Python interpreter.
    * `sys.setrecursionlimit()`: Sets the maximum depth of the Python interpreter stack.
    * `sys.stdout.write()`: Writes a string to standard output.
    * `sys.stdin.readline()`: Reads a line from standard input.

Below is an example of the use of the `sys` module.

```python
import sys

# Get the version number of the Python interpreter
print(sys.version)

# Exit the Python interpreter
sys.exit()
```

```{exercise}
:nonumber:
:class: dropdown


Write a program using `sys.argv` to access command-line arguments 
passed by the user.

```


### `os`
The `os` module provides a portable way of using operating system dependent 
functionality. It provides functions for creating and removing files and directories,
 navigating the file system, changing the current working directory, 
and more.

Some common uses are:

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

```{exercise}
:nonumber:
:class: dropdown

Create a new directory and remove it using os.mkdir() and os.rmdir().
 Handle potential exceptions like FileExistsError and OSError.
```

### `shutil`
The ability to work with files is a mandatory skill when using Python. Proficiency in file
manipulation, which includes tasks like copying, creating, and updating files through code, enables automation. Here we briefly explain the strength of `shutil` to manage this issues,
which you may use in the same way you would use your favourite shell in the command
line. 

First of all we need to import the `shutil` library
```python
import shutil
```
Some of the useful functionalities include `copy()`, `copy2()`, `copystat()`,
 `which()`, `copytree()`, among others. 

The `shutil.copy()` function in Python is used to duplicate the contents 
of a source file to either a destination file or  directory. While the file's
 permission mode is preserved during the copying process, other metadata such
 as the file's creation and modification timestamps are not retained.
It's important to note that the source must be a file, but the destination can be 
either a file or a directory. If the destination is a directory, the file will
 be copied into the directory while retaining its original filename.
Additionally, ensure that the final destination is writable. If the destination is 
an existing file, it will be replaced by the source file; otherwise, a new file 
will be created. The syntax is as follows
```python
shutil.copy(src, dest, *, follow_symlinks = True)
```
where
* `src`: represents the source file path
* `dest`: represents the path of the destination 
* `follow_symlinks`: This is an optional parameter, specific to the case where
instead of files we are finding a symbolic link.

Below we show an example of `shutil.copy`

```python
print("The destination directory contents before",os.listdir('./Apurv/Work'))
src = './Docs/A.txt'
dest = './Docs/Work'

print(shutil.copy(src,dest))

print("The destination directory contents after",os.listdir('./Apurv/Work'))
```

and the output

```python
The destination directory contents before ['Hi']
./Docs/Work\A.txt
The destination directory contents after ['A.txt', 'Hi']
```

The `shutil.copy2()` function in Python is designed to duplicate the 
contents of a source file to a specified destination, whether it's a file 
or a directory. This function shares similarities with shutil.copy(), 
but it goes a step further by attempting to preserve the original file's 
metadata during the copying process.

Python also offers the `shutil.copyfile()` function, which serves the
 purpose of duplicating the contents of a source file into a designated 
destination file. During this process, the file's metadata is not transferred. 
It's important to note that both the source and the destination must be 
file paths, and the destination must have write permissions. If the destination
 file already exists, it will be replaced by the source file; otherwise, 
a new file will be generated. If the source and destination files are identical,
 the `SameFileError` exception is thrown. 

The syntax is similar to `shutil.copy()` and `shutil.copy2()`
```python
import os, shutil

src = './Docs/A.txt'
dest = './Docs/Work/B.txt'

final = shutil.copyfile(src,dest)
print("Destination: ",final)
```
Resulting in 
```python
Destination:  ./Docs/Work/B.txt
```
If we move to directories, we find very useful tools as `shutil.copytree()` and 
`shutil.rmtree()`.  The `shutil.copytree()` function is used to replicate an 
entire directory tree that originates from a  specified source and place it 
into a target destination directory. This process is conducted recursively, 
ensuring that all contents within the source directory are copied. The syntax 
is as follows
```python
shutil.copytree(src, dest, symlinks = False, ignore = None, copy_function = copy2, ignore_dangling_symlinks = False)
```
where
* `src`: represents the source file path
* `dest`: represents the path of the destination 

`shutil.copytree()` returns the path of the newly created file. 

To remove a directory we may use the `shutil.rmtree()` function.

### `argparse` 
Writing user-friendly command-line interfaces (CLIs) is easy thanks to the
 `argparse` module. The `argparse`module also generates help and usage messages,
 providing issue error when invalid arguments are given. It allows you to define
 and customize command-line options, arguments, and help messages, making it easier
 for users to interact with your code through the terminal.

`argparse` offers several advantages:

1. **User-Friendly Interface:** It provides a user-friendly way for users to 
provide input to your scripts or programs via the command line. 
2. **Validation and Error Handling:** `argparse` automatically performs 
validation and error handling for the command-line arguments. It checks for 
required arguments, valid choices, and data types.
3. **Flexibility:** You can define various types of arguments, including
 positional arguments, optional arguments (flags), and arguments with values. 
4. **Documentation Generation:** `argparse` can automatically generate help messages
 and documentation for your script
based on the argument definitions you provide.

In order to create an CLI we first need to use the `ArgumentParser` class of 
the `argparse` module.

```python
import argparse

parser = argparse.ArgumentParser(description=’my custom command-line program’, 
    usage = ’%(prog)s [options]’)

```
The `description` parameter describes the program to help the user understand.
 In contrast, the parameter `usage` gives the user a usage message when they 
run any command with the `help` flag.

To add more parameters to the parser, we can add them using the `add_argument()`
 method.
```python
parser.add_argument(argument_default=None);
parser.add_argument(epilog=’Information displayed at the end of the help message);
```
The `argument_default` sets the default value for all arguments. The `epilog`
which displays a text at the end of the help message. Once it is done, the command
 line arguments are parsed using the `parse_args()` method.

A basic example of how to use `argparse` in a Python script is presented below
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
where `input.txt` is provided as the value for the `input_file`
 positional argument and `--output` stands for an optional argument,
 being `output.txt` is provided as its value.

## Installing third party libraries
To install libraries in Python, you can use two commonly used 
package managers: pip and conda. Using pip 
([Python Package Manager](https://pip.pypa.io))
you just have to open your command-line or terminal and run
the following command:
```bash
python -m pip install library_name 
```
or alternatively
```bash
pip install library_name
```
When you invoke these commands, pip will fetch packages from [Python 
Package Index](https://pypi.org/), a repository of software for the 
Python programming language where anyone can upload packages.
You can specify the specific version of the package you are interested
in by typing 
```bash
pip install library_name==version_number
```
Using pip you can also install packages from a Github repository 
```bash
python -m pip install git+https://github.com/pypa/library_name.git@main
```
or from a file
```bash
python -m pip install library_name.tar.gz
```
Uninstalling packages is equally easy. You just have to type
```bash
python -m pip uninstall sampleproject
```

Because in this course we are using the Anaconda Python distribution,
it is also useful for you to know that you can use its package manager
to install libraries. Simply do
```shell
conda install library_name
```
You can find more information about this very powerful tool 
[here](https://docs.conda.io/projects/conda/en/stable/).

### Virtual environments in Conda
At some point you may be working with multiple projects at
the same time and the libraries or library versions
you require for some of them may create conflicts with others.
In order to isolate the sets of libraries that you install
for specific projects, you may want to take advante to
conda's virtual environments. 

You can create a new virtual environment with the following 
command:
```shell
conda create --name myenv
```
Once you have created an environment, you 
can activate it using:
```shell
conda activate myenv
```
Once activated, you can install packages into the virtual
 environment using `conda install` or `pip`.
To deactivate the virtual environment and return to the base 
environment, use:
```shell
conda deactivate
```
You can clone an existing environment to create a new one with the same dependencies:
```shell
conda create --name myenv_clone --clone myenv
```
You can list all your created environments with:
```shell
conda env list
```
To delete an environment, use:
```shell
conda env remove --name myenv
```

```{exercise}
:nonumber:
:class: dropdown

Create a new Conda environment named "myenv" with Python 3.8.
Inside "myenv," install numpy, pandas and matplotlib.
Clone "myenv" into "newenv" and inside "newenv," upgrade 
the version of numpy to the latest version.
Check the version of numpy in "newenv."
Compare this version with the one in "myenv."
```
