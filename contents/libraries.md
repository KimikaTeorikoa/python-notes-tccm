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

To use third-party libraries, you'll need to install them first (usually via `pip` or `conda`). Once installed, you can import
them using the `import` statement:

   ```python
   import library_name
   ```

   For instance, to import the popular NumPy library for numerical operations:

   ```python
   import numpy as np  # Using the 'np' alias for convenience
   ```

   Using an alias like `np` is common for libraries with long names, as it makes code more readable.

**Specific Functions or Classes** 

If you only need specific functions or classes from a library, you can import them directly:

   ```python
   from library_name import function_name, class_name
   ```

   This approach allows you to use the imported items __without specifying the library name__.

   ```python
   from math import sqrt
   ```

   Now, you can use `sqrt()` directly without referencing the `math` module.


<!--## String Manipulation -->	
<!--## Numpy (different Section ?) -->	
<!--## Introduction	-->
<!--## Input/Output	-->
<!--## Arrays	-->
<!--## Operations -->