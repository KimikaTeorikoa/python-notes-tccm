---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---
# Numpy

NumPy, which stands for **Numerical Python**, is a *package for
numerical computing in Python*. It is a library that provides support for **arrays**
(including multidimensional arrays), as well as various of mathematical
functions to operate on these arrays. With NumPy, scientific and mathematical
computations are simpler and faster.

One of the key advantages of NumPy is its efficiency. *Under the hood, it uses
optimized C and Fortran libraries*, making it much faster than pure Python
code for numerical operations. This speed enables quicker data analysis,
scientific computations, and other specialized tasks that involve numbers, 
arrays, or matrices.

Another benefit is its ease of use. Even though it’s a powerful tool,
NumPy’s syntax is designed to be straightforward and similar to native Python,
making it easy to learn and implement. NumPy also offers a robust set of 
functions to perform statistical analysis, linear algebra, Fourier transforms, 
and more. This makes it a versatile tool that can handle a wide variety of 
mathematical tasks, from simple calculations to complex scientific research. 

Because of its extensive utility, NumPy forms the base for other scientific 
libraries in Python. Moreover, the syntax of many machine learning libraries, 
like PyTorch and JAX is based on numpy. So, once you know NumPy it will be very 
easy to learn how to use these libraries as well.

## The basics

As any other library, NumPy has to be installed first. Since we are using
conda, it is as simple as:

```bash
conda install numpy
```
Now we can import it as:
```{code-cell} python
import numpy as np
```
The convention is to import numpy as `np`.
Now we can define our first NumPy array. This can be done in various ways: 

```{code-cell} python
# From a Python list
arr_1d = np.array([1, 2, 3, 4, 5])
print("From list: ", arr_1d)

# From a Python tuple
arr_tuple = np.array((1, 2, 3, 4, 5))
print("From tuple: ", arr_tuple)

# Using arange function to create an array from 0 to 4
arr_arange = np.arange(5)
print("Using arange: ", arr_arange)
```
Numpy arrays behave similar to python lists - you can slice them, access 
elements, use in for loops and list comprehensions etc.:
```{code-cell} python
# Creating a NumPy array
arr = np.array([0, 1, 2, 3, 4, 5])

# Slicing: Get elements from index 1 to 4
arr_slice = arr[1:5]
print("NumPy array slice:", arr_slice)

# Accessing elements: Get the element at index 2
arr_element = arr[2]
print("NumPy array element at index 2:", arr_element)

# Using in for loops
print("Iterating through NumPy array:")
for item in arr:
    print(item, end=' ')

# Using list comprehensions
arr_squared = np.array([x**2 for x in arr])
print("\nNumPy array squared:", arr_squared)
```

However, there are 
important differences:

- Although you can have lists of lists in Python, Numpy
allows you to create true multi-dimensional arrays.

- Numpy provides a host of built-in functions for operations
like addition, subtraction, multiplication, and much more. Python lists don't
offer this feature.

- Numpy arrays are more memory-efficient and faster for numerical
operations compared to Python lists.

- To use the operations mentioned above, all elements in the  arrays must be of 
the same type, unlike Python lists.

Let's go through all those differences step by step.

```{exercise}
:nonumber:
:class: dropdown

Create a NumPy array called `my_array` containing the numbers from 1 to 10. 
Then, print the elements in reverse order (from 10 down to 1).

Hint: You can use slicing to reverse the array.
```

## Multidimensional numpy arrays

First let's see how to create a 2D array:
```{code-cell} python
# Create a 2D array (3 rows x 3 columns)
two_d_array = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(two_d_array)
```
NumPy 2D array can be treated the same way as Python list of lists. For example,
to get the first row of the array:
```{code-cell} python
first_row = two_d_array[0]
print(first_row)
```
And to access the second element of the first row:
```{code-cell} python
element = two_d_array[0][1]
print(element)
```
However, NumPy provides a much more powerful syntax for multidimensional array
slicing. It generally follows the format 
`[row_start:row_end, col_start:col_end]`. Below are various examples to 
demonstrate slicing operations on a 2D NumPy array:
```{code-cell} python
element = two_d_array[0, 1]
print("Single element:", element)

first_column = two_d_array[:, 0]
print("First column:", first_column)

sub_matrix = two_d_array[0:2, 0:2]
print("Sub-matrix (first two rows and columns):")
print(sub_matrix)
```

```{exercise}
:nonumber:
:class: dropdown

Create a 5x5 NumPy array called `matrix` with random values. Then extract the 
first three elements of the second column of the matrix and print them.

Hint: use `np.random.rand` to generate a random matrix
```

### Reshaping arrays

NumPy arrays can be reshaped into different shapes using the `reshape` method, 
which takes the new shape as argument.
Imagine you have a 1D array with 4 elements and you want to reshape it into a
2x2 2D array. You can do this as follows:
```{code-cell} python
a = np.array([1, 2, 3, 4])

# Reshape the array into a 2x2 matrix
b = a.reshape(2, 2)
print(b)
```

```{hint}
Many array methods, as `reshape`, are also available as functions in the numpy
module. For example, `np.reshape(a, (2, 2))` is equivalent to `a.reshape(2, 2)`.
```

The order of the elements in the reshaped array is by default first filling 
by row, as shown in the example above. Such a behaviour can be tuned
however with the `order` argument of the `reshape` method. The two possible
values are `order=C` (default) and `order=F` (for Fortran-like order), which
fill the reshaped array by column.

It is also possible to reshape a multidimensional array into a 1D array. In the
above example, we can reshape the 2x2 array `b` back into a 1D array with 
`b.reshape(4)`. Alternatively, you can use the `flatten` method to achieve the
same result.

```{exercise}
:nonumber:
:class: dropdown

Given the following vector containing the X,Y, and Z atomic coordinates of a water molecule:

`-2.34   2.71  0.00  -1.43  2.71  0.00  -2.71  3.58  0.28` 

Reshape it to a 3x3 matrix, containing the X, Y, and Z coordinates of each atom 
on each row.
```

## NumPy array built-in properties and functions
There are multiple properties on NumPy arrays that are not available for 
Python lists. For example:

- Shape: Tells us the shape of the array. A 2x3 array will have a shape of (2, 3).
```{code-cell} python
print(two_d_array.shape)
```

- Size: Gives us the total number of elements in the array.
```{code-cell} python
print(two_d_array.size)
```

- Dimensions: Tells us how many dimensions the array has.
```{code-cell} python
print(two_d_array.ndim)
```

- Data Type: Shows the type of data stored in the array.
```{code-cell} python
print(two_d_array.dtype)
```

Another important feature of NumPy arrays not available for Python lists is that
you can perform element-wise mathematical operations with them:
```{code-cell} python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print("Addition: ", a + b)
print("Subtraction: ", a - b)
print("Multiplication: ", a * b)
print("Division: ", a / b)
print("Square: ", a ** 2)
```

It is also possible to add (subtract, divide etc.) scalar value to all the 
elements of the array:
```{code-cell} python
a = np.array([1, 2, 3])
print(a + 10)
```

Another operation that is defined for NumPy arrays is `@` which works as a dot 
product for 1D arrays (vectors) and as a matrix product for 2D arrays 
(matrices):

```{code-cell} python
vector = np.array([1, 2])
matrix = np.array([[1, 0], [0, 2]])

print("vector vector", vector @ vector)
print("matrix vector: ", matrix @ vector)
print("matrix matrix: ")
print(matrix @ matrix)
```

A NumPy array can be converted to an array with another shape, but
the same size (number of elements) by the reshape method:

```{code-cell} python
print(np.arange(9).reshape(3, 3))
```

The arguments to the reshape method are the number of elements along the each 
new dimension. Since the total number of elements is defined by the original
array, number of elements along one of the dimensions can be inferred 
automatically by providing value of -1:

```{code-cell} python
print(np.arange(9).reshape(3, -1))
```

Finally, in NumPy you can easily do operations such as calculating maximum value
in the array or getting the sum of all values. These are called "aggregation
operations":

```{code-cell} python
a = np.arange(9)

print("Maximum: ", np.max(a))
print("Minimum: ", np.min(a))
print("Sum: ", np.sum(a))
print("Mean: ", np.mean(a))
```

```{exercise}
:nonumber:
:class: dropdown

Calculate the average of all integers less than 100 divisible by 8. 
```

## Performance
Now that we know the basics of NumPy arrays and what operations can be 
performed on them, let's see how NumPy compares to Python lists in 
terms of performance. For that we will be using `timeit` module from Python
standard library (so no new package has to be installed).

```{code-cell} python
import timeit
import numpy as np

def sum_of_squares_python_list():
    python_list = list(range(100000))
    return sum(item ** 2 for item in python_list) 
    
def sum_of_squares_numpy_array():
    numpy_array = np.arange(100000)
    return np.sum(numpy_array ** 2)
    
# Time the execution
python_time = timeit.timeit(sum_of_squares_python_list, number=10)
numpy_time = timeit.timeit(sum_of_squares_numpy_array, number=10)

print("Python list: ", python_time)
print("NumPy array: ", numpy_time)
```

As you can see, NumPy is about two orders of magnitude faster than pure 
Python implementation.

(broadcasting)=
## Broadcasting
A very powerful feature of NumPy is array broadcasting. It allows to apply
mathematical operations to arrays with different shapes and dimensions. One 
example of broadcasting we have already seen - adding a scalar to a 1D array.
However, it is also possible to add a 1D array to a 2D one:
```{code-cell} python
a = np.array([[1, 2], [3, 4], [5, 6]])
b = np.array([1, 2])
print(a + b)
```

To use broadcasting, NumPy compares the shapes of the two arrays element-wise, 
starting with the trailing dimensions and working its way forward. The 
dimensions are compatible when:
- They are equal, or
- One of them is 1.

For our arrays a and b, their shapes are:

- a has shape (3, 2)
- b has shape (2,)

To compare these shapes for broadcasting, we align them from the last dimension:
```
    3, 2  (shape of a)
       2  (shape of b)
```
Both dimensions are equal, so they are compatible. If they weren't, you'd have 
to reshape one of the arrays for broadcasting to work.

Broadcasting basically "stretches" the smaller array to have the same shape as
the larger array. In our case, array b is "virtually" replicated along the 
second dimension to match the shape of array a:

```
Virtual b after broadcasting = [[1, 2],
                                [1, 2],
                                [1, 2]]
```

Note that broadcasting doesn't really replicate the data. It's a
"virtual" replication for the sake of the computation, making the operation
efficient.
Now, the addition occurs element-wise:
```
a = [[1, 2],  virtual_b = [[1, 2],
     [3, 4],               [1, 2],
     [5, 6]                [1, 2]]

c = a + virtual_b

  = [[1+1, 2+2],
     [3+1, 4+2],
     [5+1, 6+2]]
     
  = [[2, 4],
     [4, 6],
     [6, 8]]
```

The result is a 2D array `c` with the same shape `(3, 2)` as `a`, and it 
contains the sum of the corresponding elements from `a` and the virtually 
broadcasted `b`.

```{exercise}
:nonumber:
:class: dropdown
Create the following matrix using broadcasting:

[[0, 1, 2],
 [0, 1, 2],
 [0, 1, 2]]

Hint: you can create a matrix of zeros with `np.zeros`.
```


## Matrix Operations and the linalg Module
In this section, we'll explore some of the most common matrix operations that
NumPy offers. Particularly, we will take a look at some  functions from `linalg`
module which provides a wide range of functions for performing linear algebra
operations. These operations are essential for various scientific and
engineering applications.

### Matrix Multiplication
Matrix multiplication is a fundamental operation in linear algebra. NumPy makes
it easy to multiply matrices using the dot function or the @ operator, as you've
seen in the previous section. Let's revisit matrix multiplication with NumPy:

```{code-cell} python
# Create two matrices
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
result_dot = np.dot(A, B)
print("Matrix Multiplication using dot:\n", result_dot)

result_at = A @ B
print("Matrix Multiplication using @ operator:\n", result_at)
```

Both methods yield the same result, which is the product of matrices A and B.

### Matrix Inversion
Matrix inversion is another common operation in linear algebra. You can
calculate the inverse of a square matrix using NumPy's `inv` function from the
`linalg module`. However, not all matrices are invertible, so it's essential to
check for invertibility before attempting the inversion.

Here's how you can calculate the inverse of a matrix:

```{code-cell} python
def print_inverse(A, name):
    try:
        A_inv = np.linalg.inv(A)
        print(f"Matrix {name}:\n", A)
        print(f"Inverse of {name}:\n", A_inv)
    except np.linalg.LinAlgError:
        print(f"Matrix {name} is not invertible.\n") 

# Create a square matrix
M1 = np.array([[1, 2], [3, 4]])
M2 = np.array([[2, 3], [4, 6]])

print_inverse(M1, "M1")
print_inverse(M2, "M2")
```
Here we first define a function that would print a given matrix and it's
inverse. Then, we call this function on two matrices: one that is invertible
and one that is not. As yu can see, in the latter case the function informs us
that the inverse cannot be taken.

### Determinant and Eigenvalues
You can compute the determinant of a square matrix and its eigenvalues using
NumPy's `det` and `eig` functions. The determinant of a matrix provides valuable
information about its properties, and eigenvalues are crucial in various
applications, such as solving differential equations and analyzing dynamic
systems.

Here's how you can calculate the determinant and eigenvalues of a matrix:

```{code-cell} python
# Create a square matrix
D = np.array([[2, 1], [1, 3]])

# Calculate the determinant
det_D = np.linalg.det(D)
print("Determinant of D:", det_D)

# Calculate eigenvalues and eigenvectors
eigenvalues, eigenvectors = np.linalg.eig(D)
print("Eigenvalues of D:", eigenvalues)
print("Eigenvectors of D:\n", eigenvectors)
```

### Solving a System of Linear Equations

NumPy's `linalg` module also provides a convenient way to solve systems of
linear equations of the form `Ax = b`, where `A` is a matrix, `x` is a vector of
unknowns, and `b` is a vector of constants. Solving such systems is a common
task in various fields, including engineering and physics.

Here's an example of how to use `numpy.linalg.solve` to solve a system of linear
equations:

```{code-cell} python
# Define the coefficient matrix A and the constants vector b
A = np.array([[2, 1], [1, 3]])
b = np.array([5, 8])

# Solve the system of linear equations Ax = b
x = np.linalg.solve(A, b)

print("Solution x:", x)
```
In this example, we have a system of two linear equations:

```
2x + y = 5
x + 3y = 8
```
The `numpy.linalg.solve` function takes the coefficient matrix A and the constants
vector b as input and returns the solution vector x. The solution x represents
the values of the unknown variables that satisfy all the equations in the
system.

You can use this method to efficiently solve larger systems of linear equations
as well, making it a powerful tool for numerical simulations and data analysis.


These are just a few examples of the many linear algebra operations you can
perform with NumPy and its `linalg` module. Understanding and utilizing these
operations is crucial for a wide range of scientific and engineering tasks.


```{exercise}
:nonumber:
:class: dropdown
Create a random 5x5 matrix and show that a product of this matrix with its 
inverse is an identity matrix.
```

(numpy.io)=
## Input/Output
In real applications, you often want to read some numeric data from an external
file or write out the results. NumPy provides useful functions to make
this process simple.

### Reading files with `numpy.loadtxt`

Suppose you have a text file called `data.txt` with the following content:
```
1.0 2.0 3.0
4.0 5.0 6.0
7.0 8.0 9.0
```
You can load this data into a NumPy array like this:
```python
import numpy as np
data = np.loadtxt('data.txt')
print(data)
```

```
[[1. 2. 3.]
 [4. 5. 6.]
 [7. 8. 9.]]
```

```{hint}
Note that when using `loadtxt`, you don't need to care about file objects or
opening and closing the file. NumPy takes care of that for you.
```

Often values in the text files are separated by some delimiter and have some 
additional information in the first few lines (header):
```
# This is a header line 1
# This is a header line 2
1.0,2.0,3.0
4.0,5.0,6.0
7.0,8.0,9.0
```

You can skip the header and specify the delimiter like so:
```python
data = np.loadtxt('data_with_header.txt', skiprows=2, delimiter=',')
print(data)
```

```
[[1. 2. 3.]
 [4. 5. 6.]
 [7. 8. 9.]]
```

### Writing files with `numpy.savetxt`
To save a NumPy array to a text file, it's quite straightforward. Suppose you 
have the following NumPy array:

```python
my_array = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
```

You can save it to a file like this:

```python
np.savetxt('my_array.txt', my_array)
```

The text file my_array.txt will look like this:

```
1.000000000000000000e+00 2.000000000000000000e+00 3.000000000000000000e+00
4.000000000000000000e+00 5.000000000000000000e+00 6.000000000000000000e+00
7.000000000000000000e+00 8.000000000000000000e+00 9.000000000000000000e+00
```

You can also specify the delimiter, format, and even add a header:
```python
np.savetxt('my_array_with_header.txt', my_array, delimiter=',', fmt='%d', 
           header='This is my data')
```

The text file `my_array_with_header.txt` will have:
```
# This is my data
1,2,3
4,5,6
7,8,9
```

```{exercise}
:nonumber:
:class: dropdown
Import `my_array_with_header.txt` from the previous example into a spreadsheet,
change the values, save and then read the updated file using `np.loadtxt`. 
```

## NumPy documentation
Here we covered only the most essential concepts of NumPy, but there is much 
more to it. To deepen your understanding and unlock the full power of this 
incredible library, it is strongly recommended that you take a look at the 
official NumPy documentation, especially the beginner's guide available at 
https://numpy.org/doc/stable/user/absolute_beginners.html
