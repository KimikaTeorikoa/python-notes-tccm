# Python Fundamentals
In this chapter, we will introduce you to the very basics
of computer programming with Python. We will first see
some basics that will make you understand how a Python 
program looks. Then we will go through how to 
write basic instructions for reading and writing
inside a computer program. We will also explain the types
of variables we can use. Finally we will introduce
the basics of writing functions.

## Introduction
Python is a **high-level programming language**,
like others you may have heard about, including
Fortran, C or C++. High-level
languages differ from low-level languages in that
the former can be easily understood by people, while
the latter are those that can be understood by machines. 
So when writing in a high-level language we normally
need to translate the actions in our code to 
machine-readable format.

If you have ever done any programming before using 
languages like Fortran, C or C++, you surely adopted
a workflow where you first wrote code and then 
compiled using another program called **compiler**.
That will not be the case with Python. One of the
key differences between Python and those other programming
languages is that Python is an **interpretive** language.
Hence you will not have to compile the code as you
modify it. The **Python interpreter** performs those 
actions for you. Because Python is not compiled, your
programs written in Python will not be as fast as they 
could be when written in Fortran or C.

Let's see how this works in practice, writing our first
program in Python. In your terminal, open a text editor
and write the following:

```python
#!/usr/bin/env python
# Our fisrt Python program
print ("Hello World!")
```
You will notice that the first couple of lines start with 
a hash symbol (#). This means that whatever follows will
not be read by the Python interpreter and is what we 
usually regard as a **comment**.
Now close the file, save it as `hello_world.py` and run 
the following command
```bash
$ python hello_world.py
```
Now check whether the program has done as you intended it to.

### Writing Python code: names and cases
In your programs you will usually be defining lots of different
variables. One of the things you must remember is that Python
is **case sensitive**, so
```python
a = 10
print (A)
```
will return an error (specifically, a `NameError`), as a variable
named `A` does not exist.

Also, it is convenient to choose **variable names** that
will be meaningful to you and any other potential user of your
program (often your future self). For example, if you are
calculating the area of a circle, it would make sense to
write something like this:
```python
area = pi*radius**2
```
Here we are using some stuff that you we have not covered yet,
but you surely understand why we are using the code snippet as
an example of using meaningful variable names. Using cryptic 
variable names will make everyone miserable, so it is a good 
investment to use names that seem sensible choices.

Also, in Python some possibilities are forbidden, like
starting a variable with a number. If you write code including 
something like:
```python
77david = 'myname'
```
and try to run it, you will get a `SyntaxError`. The same thing 
will happen if you try to use one of the many keywords in
Python. These include
```
and     del     from        not     while
as      elif    global      or      with
assert  else    if          pass    yield
break   except  import      print   class
in      raise   continue    is      return
def     for     lambda      try
```

Additionally, in Python there are naming conventions
that you should follow. These are described in
[PEP8](https://peps.python.org/pep-0008/#prescriptive-naming-conventions).
For example, variables are typically written in lowercase, 
and so are functions. On the other hand, classes, which 
we will learn about in the future, use the so called
CapWords style.

## Input / Output	
In our first program `hello_world.py` above, we have already 
written to something we call the "standard output", i.e. the 
display. In Python there are many different ways to read input 
into a program and to write your output. You can, for example,
prompt the user to write a set of input variables using the 
keyword for the program to read (this would be the "standard 
input") or make the program write the results of a calculation
to a file. Here we explore the basics of Input / Output operations.

### Opening and closing files
Suppose that there is a file called `myfile.txt` from which you 
want to read some contents. In order to do that, you will have to
write 
```python
f = open("myfile.txt", "r")
```
In this statement, we are using a **built-in function** called `open`.
The first argument of this function is the external filename (Python
will assume that the file does exist). The second argument indicates 
the processing **mode**. There are different modes available:
* `r`: read only mode
* `w`: write only mode
* `a`: append mode
* `r+`: read and write mode
*  `t`: text mode
* `b`: binary mode

Depending on the type of data in the file and what you intend to use 
the file for, you will choose one of these ways of opening the file. 
As a good programming habbit, remember to close files once you no 
longer need to access them:
```python
f.close()
```
Another way of opening files in Python is using **file iterators**, i.e.
employing the `with` statement, which works as
```python
with open("myfile.txt", "r") as f:
    ...
```
In this case you do not need to close the file yourself. 

### Reading and writing data into files 
Once you have opened a file, you will many times want to read its 
contents. You can do that line by line for the `myfile.txt` which 
you have opened and named as `f` in your program doing
```python
f.readlines()
```
Alternatively, if you want to write into your file, you would be
able to do the following
```python
f.write("hello world!\n")
```
where we are simply writing a text string.

## Data Types
Variables in Python can be of many different types,
including text strings, lists, integers, floats and
Boolean.
Assignment is simply made using the equal operator 
(`=`) in statements like
```python
a = 10
```
Because Python has **dynamic typing**, you do not 
have to declare variables. Python will assign
a type to each variable in your code. In order
to know the type of a given variable, you can use
the intrinsic function `type`.
```python
a = 10
type(a)
```
In the case above, you might want a to be defined
as a `float`. If that is the case, you can assign 
the type explicitly
```python
a = float(10)
```
In Python, you can sometimes combine different types
to perform arithmetic operations
```python
a = 10; b = 1.
c = a + b
print (c)
print (type(c))
```
:::{note}
In the past, there were problems with integer divisions,
as you would recover an `int`, but that is no longer
the case in Python 3, where they are converted into a float
```python
a = 10; b = 3
c = a/b
print (c)
print (type(c))
```
:::

### Arithmetic operations in Python 
Using floats and integers you can do all sorts
of computations in Python, very much like you 
would in a regular calculator. 
You can for example use operators like `+` and `-`,
which are called **unary operators**, because they
act on a single numeric value. You can
perform multiplications, using the operator `*`, 
divisions with `/`, and integer divisions with `//`.
Using `%` you will obtain the remainder of a division.
Also you can exponentiate using the operator `**`.

There are also some additional operations that you
may want to know of, like the `+=` addition assignment
or `-=` substraction assignment. You can also use
relational operators, like `<`, `>`, `<=`, `>=` or `==`,
to compare the values of two variables. For example,
```python
a = 10; b = 3
a < b
```
These operators will return either `True` or `False`.

### Strings	
### Vectors (lists?, Tuples?, Dictionaries?)	
### Matrices	
### Functions	

## Intrinsic functions (from Computational QM)	
### Using and writing functions
### Writing Python code: Indentation
In Python, the way that a program looks is 
very much determined by indentation. This 
differs from what we will find in other languages
like Fortran or C, where formatting is not so
important. When you write an `if` statement in
Python, you must respect the right indentation,
e.g.
```python
if x < 12:
    print (x)
```
And if not, the code will simply not run. 
Different levels of indentation start where 
we have colons (`:`), and these have to be 
indented with respect to the previous level
of indentation. Be 
careful not to add white spaces where they do not
belong and use consistently tabs or spaces
(4 spaces is the preferred option in PEP8). 
This may feel like a nuisance if you have
experience in some other programming language, but
will help orient yourself when reading code in the
long run.

### Environments	
