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
variables. It is convenient to choose **variable names** that
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
The first argument of this function is the filename, and the second
argument indicates the **mode**. There are different modes available:
* `r`: read only mode
* `w`: write only mode
* `a`: append mode
* `r+`: read and write mode
*  `t`: text mode
* `b`: binary mode

Depending on the data in the file or what you intend to use the file
for, you will choose one of these ways of opening the file. Remember
to close files once you no longer need to access them:
```python
f.close()
```

## Data Types	
### Integers	
### Floats	
### Strings	
### Vectors (lists?, Tuples?, Dictionaries?)	
### Matrices	
### Functions	

## Intrinsic functions (from Computational QM)	
### Using and writing functions
### Writing Python code: Indentation

### Environments	
