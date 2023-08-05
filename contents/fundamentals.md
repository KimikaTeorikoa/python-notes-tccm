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
# Python Fundamentals
In this chapter, we will introduce you to the very basics
of computer programming with Python. We will first see
some general notions that will make you understand how a Python 
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
actions for you. But this comes with a caveat. 
Because Python is not compiled, your
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

## Names and cases
In your programs you will usually be defining lots of different
variables. One of the things you must remember is that Python
is **case sensitive**, so when you try
```{code-cell} python
a = 10
print (A)
```
things do not go well. Python returns an error (specifically, 
a `NameError`), as a variable named `A` does not exist.

Also, it is convenient to choose **variable names** that
will be meaningful to you and any other potential user of your
program (often your future self). For example, if you are
calculating the area of a circle, it would make sense to
write something like this:
```python
area = pi*radius**2
```
Here we are using some stuff that you we have not covered yet.
Also, we are assuming that you have given values to both `pi`
and `radius`. 
But you surely understand why we are using the code snippet as
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
we will learn about in the future, use the so-called
CapWords style.

## Input / Output	
In our first program `hello_world.py` above, we have already 
written to something we call the "standard output", i.e. the 
display, using the `print` function. 
In Python there are many different ways to read input 
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
Another way of opening files in Python is using **file iterators**.
You are using them when you open files using the 
`with` statement, which works as
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
f.readline()
```
You can bulk-read all the file using `readlines()` instead.

Alternatively, if you want to write into your file, you would be
able to do the following
```python
f.write("hello world!\n")
```
where we are simply writing a text string. As we go along, we
will greatly expand our understanding of Input/Output operations.

## Data Types
Variables in Python can be of many different types,
including text strings, lists, integers, floats and
Boolean. An highly consequential thing we must say, 
but we will not fully explain yet, is that in Python
variables take the form of **objects**, which are the
most fundamental notion in Python programming. For now,
we will just say that objects are *pieces of memory, 
with values and sets of associated operations*.

Assignment of a value to a variable
is simply made using the equal operator 
(`=`) in statements like
```python
a = 10
```
Because Python has **dynamic typing**, you do not 
have to declare variables. Python will assign
a type to each variable in your code. In order
to know the type of a given variable, you can use
the intrinsic function `type`.
```{code-cell} python
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
```{code-cell} python
a = 10; b = 1.
c = a + b
print (c)
print (type(c))
```
:::{note}
In the past, there were problems with integer divisions,
as you would always recover an `int`, but that is no longer
the case in Python 3, where they are converted into a float.
Try the following:
```python
a = 10; b = 3
c = a/b
print (c)
print (type(c))
```
:::

### Numeric types
In the few lines of code above, we have already
used the most straightforward types in Python, 
which are **integers**, which lack a decimal part,
and **floating-point** numbers.
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
```{code-cell} python
a = 10; b = 3
a < b
```
These operators will return either `True` or `False`.
This is what we call a **Boolean**.
We will discuss Booleans and logical operations in the
[next chapter](flowcontrol.md).

Something you must bear in mind when you are programming
is the finite machine precision with which your machine
works with. A case in point is the following:
```{code-cell} python
print (0.1 + 0.05)
```
Discouragingly, the result is not what one would expect. 
There is,
however, nothing wrong with that result. It is the consequence
of the way real numbers are stored in your machine, which 
results in **round-off or truncation errors**. Specifically,
floats are written using 53 bits of precision. Because 0.1 and
0.5 are truncated in floating-point representation, the result
is not exactly what you would expect. When writing a program,
you should think about whether this actually matters for the
problem at hand.

Another type of numeric that you may need are *complex* numbers.
In Python, you can define them using the character `j`.
```{code-cell} python
type(1 + 1j)
```

### Text strings
The variable type we normally use to store text characters
in Python are **strings**. In fact, we have already written 
one such variable in our `hello_world.py` program above. 
Strings are generated using single `'` or double quotes `"`
around a set of characters. It is usually good to pick 
a rule and stick to [either single or double 
quotes](https://peps.python.org/pep-0008/#string-quotes).

Python provides a number of intrinsic functions and operators
that are specific to string manipulation. For example, if
you want to know the length of a string, you can use the
`len` function.
```{code-cell} python
myname = 'david'
print (len(myname))
```

Additionally, addition and multiplication work in a special
way when applied to strings. For example,
```{code-cell} python
string1 = "hello"
string2 = "world"
space = " "
print (string1 + space + string2)
```
Also,
```{code-cell} python
verse1 = "Good morning\n"
verse2 = "Nothing to do to save his life call his wife in"
print (5*verse1 + verse2)
```
Hence, addition for strings means *concatenation*, while
multiplication means *repetition*. You can also perform
membership operators, to check whether an element is present
in a string.
```{code-cell} python
'a' in 'Antonio'
```

Another interesting thing you can do with strings that
was not possible with `int` or `float` is **indexing**. You 
can access the *i*-th element of a string using
```python
string[i]
```
where you must remember that Python uses **zero-based
indexing**. Hence, the 1st element in a string is 
accessed using the index 0, and so on. You can also
access characters in a string backwards, using 
negative numbers.
We can also perform **slicing** operations, which 
extract sections (or slices) of the string
```{code-cell} python
val = 'spam'
print (val[2:4])
```

There is an interesting property of strings, which
is called **immutability**. While you can redefine a
string, you cannot change it. For example, you can
do
```python
s = 'spam'
s = 'ham'
```
but if you try
```{code-cell} python
s = 'spam'
s[0] = 'h'
```
you will obtain a `TypeError`. What you can do instead
is 
```{code-cell} python
s = 'h' + s[2:]
print (s)
```
This construction generates a new string using the old string,
but importantly, it does not change the old string.

There are many other interesting manipulations that
we can do with text strings, using **type-specific methods**.
Strings are, for example, searchable
```{code-cell} python
s = 'david'
s.find('d')
```
and you can generate new strings making intuitive changes
like making uppercase what was lowercase
```{code-cell} python
s = 'peter'
s.upper()
```
You can also split a string into parts, based on a given
element.
hable
```{code-cell} python
s = 'bread, butter, flour, milk'
s.split(',')
```
But this takes us directly into the next type of variable
we want to consider.

### Lists, tuples and dictionaries
**Lists** are a very important type of **sequence**, which
in Python is a type of data structures that contain a 
collection of elements. In the last section, we have generated 
one such object
```python
['bread', ' butter', ' flour', ' milk']
```
which is of course a list of strings. Lists are defined
when the list of elements is written inside square
brackets (`[ ]`). If you were using parenthesis instead,
(`( )`) then you would be defining what we call a **tuple**.
Finally, there are **dictionaries**, which are defined
using curly brackets (`{ }`).

Lists and tuples can contain all sorts of data types. You
can for example combine numerics and strings.
```python
mylist = ["I", "am", 30, "years", "old"]
```
Also, you can easily convert between lists and tuples
```python
mytuple = tuple(mylist)
```
The main difference between lists and tuples is that the
latter are immutable, while you are allowed to change
lists.

Operators work with lists and tuples like they did with
strings. Addition is concatenation and multiplication is
repetition. For example,
```{code-cell} python
['one', 'two'] + ['three', 'four']
```
or 
```{code-cell} python
(1, 2)*3
```
Membership operators are also similar to what we saw for
lists
```{code-cell} python
1 in [10, 20, 30]
```
As are the slicing operations, which are again accessing
elements of the list using zero-based indexing
```{code-cell} python
decades = list(range(10, 110, 10))
print (decades[2:-2])
```
Here we are using something called a `range` object,
which we are using to build a list. The syntax is worth
discussing: using `range(start, stop, step)` we enumerate 
integers from the 
first argument (`start`), to the second argument (`stop`), 
in steps of size given by the third argument (`step`).

You can interrogate lists using intrinsic functions.
For example, you can find how many elements there are
in a list using `len()` 
```{code-cell} python
names = ['pedro', 'jose', 'felipe', 'mariano']
print (len(names))
```
and you can sort its contents with `sorted()`
```{code-cell} python
names = ['pedro', 'jose', 'felipe', 'mariano']
print (sorted(names))
print (names)
```
which, as you sure have noticed, sorts strings
alphabetically.

To finalize we will say that as objects, lists
have associated **methods** that are particularly
useful. For example, you can easily add an element
to a list 
```{code-cell} python
names = ['pedro', 'jose', 'felipe', 'mariano']
names.append('yolanda')
print (names)
```
remove elements from a list
```{code-cell} python
names = ['pedro', 'jose', 'felipe', 'mariano']
names.remove('pedro')
print (names)
```
reverse the order of the elements
```{code-cell} python
names = ['pedro', 'jose', 'felipe', 'mariano']
names.reverse()
print (names)
```
or sort them. Remember that before we have used the function
`sorted()`. There is an equivalent method:
```{code-cell} python
numbers = [30, 1,  100]
numbers.sort()
print (numbers)
```

**Dictionaries** are a more sofisticated type of sequence,
with elements having multiple entries called **keys** and
their corresponing **values**. Their structure is hence
```python
mydict = {key1: val1, key2: val2, key3: val3}
```
There is great flexibility in terms of what can be a key
or a value
```python
presidents = {'Adolfo': [1976, 1977, 1979], 'Leopoldo': [1981], \
              'Felipe': [1982, 1986, 1989, 1993]}
```
You can access dictionaries in many different ways, for
example using the `items()`, `keys()` or `values()` method
```{code-cell} python
presidents = {'Adolfo': [1976, 1977, 1979], 'Leopoldo': [1981], \
              'Felipe': [1982, 1986, 1989, 1993]}
print (presidents.items())
print (presidents.keys())
print (presidents.values())
```
In the next few lessons we will put all these data structures 
to good use.