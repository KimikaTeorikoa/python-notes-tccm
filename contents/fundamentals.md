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
compiled it using another program called **compiler**,
wich generated a binary, machine-readable file. 
It would look something like this

![compiling](https://hpc-wiki.info/mediawiki/hpc_images/8/8a/Compiler_Shematic.png)


That will *not* be the case with Python. One of the
key differences between Python and those other programming
languages is that Python is an **interpretive** language.
Hence you will not have to compile the code as you
modify it. The **Python interpreter** performs those 
actions for you. 

All of these comes with a caveat. 
Because Python is not compiled, your
programs written in Python will not be as fast as they 
could be when written in Fortran, C or C++.
Below you can see a comparison between speeds of various
programming languages 

![performance-speed](https://niklas-heer.github.io/speed-comparison/assets/latest/combined_results.png)

```{hint}
Clearly, Python is not the fastest language in town. There
are workarounds for this, like linking Python and C or Fortran
code, or using [Cython](https://cython.org/).
```

## Writing your first Python program
Let's see how running a simple Python program works in 
practice. Using your IDE or terminal, open a text editor
and write the following:

```python
#!/usr/bin/env python
# Our first Python program
print ("Hello World!")
```

Now let's examine what we have just written. 
You will notice that the first couple of lines 
that we have written start with a hash symbol (`#`). 
This means that whatever follows will not be read by the 
Python interpreter. This is what we usually regard as 
a **comment**. Then there is a `print` statement 
followed by a parentheses `()` with a piece of text
inside. And that is all there is to our first Python
program.

Now close the file, save it as `hello_world.py` and run 
the following command on your terminal
```bash
foo@bar:~$ python hello_world.py
```
Now check whether the program has done as you intended it to.

## Names and cases
In your programs you will usually be defining lots of different
variables. *Variables are names for values* and the naming of 
variables follow some conventions. For example, they can 
be formed by letters, numbers and only one symbol, the 
underscore `_`.

Something else you must remember is that Python
is **case sensitive**, so when you try to use 
a variable without regard to the case you used to 
assign it a value, things will not go well.
```{code-cell} python
a = 10
print (A)
```
As we see, Python returns an error (specifically, 
a `NameError`), as a variable named `A` does not exist.
The only variable that we assigned a value to is `a`, and
in Python `a` and `A` are different things.

```{hint}
Always try to read error messages from Python. They are
highly informative and often direct you to the exact line
where the problem is.
```

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

It is convenient to choose **variable names** that
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
display, using the `print` function. The `print` function
displays values as text.

 
In Python there are many other ways to write your output
and also to read input into a program. You can, for example,
make your program write the results of a calculation
to a file instead of to your screen, or prompt the user to 
write a set of input variables using the keyword for the 
program to read (this would be the "standard input"). 
Here we explore the basics of Input / Output operations.

### Opening and closing files
Suppose that there is a file in your working directory
 called `myfile.txt` from which you want to read its contents. 
In order to do that, you will have to write 
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
contents. You can do that *line by line* for the `myfile.txt` which 
you have opened and named as `f` in your program doing
```python
f.readline()
```
You can *bulk-read* all the file using `readlines()` instead.

Alternatively, if you want to write into your file, you will
first have to open for writing. Then, you will be able to write
into the file using the following statement
```python
f = open("test.txt")
f.write("hello world!\n")
f.close()
```
where we are simply writing a text string. As we go along, we
will greatly expand our understanding of Input/Output operations.

```{exercise}
:nonumber:
:class: dropdown
Do you remember our first Python program called `hello_world.py`?
In a IPython session or using a Jupyter-notebook, open that
file using both `open` and an iterator and write its contents
in your display. Pay attention to how these are written.
```

## Data Types
Variables in Python can be of many different types,
including **text strings**, **lists**, **integers**, **floats**
 and **Boolean**. In Python variables take the form of **objects**, 
although we will not explain what this highly consequential fact
 entails just yet. 
For now, we will just say that objects are *pieces of memory, 
with values and sets of associated operations*.

In Python, a variable is created when you assign a value to it.
Assignment of a value to a variable is simply made using the equal
 operator (`=`) in statements like
```python
a = 10
```
Because Python has **dynamic typing**, you do not have to declare 
variables. Python will assign a type to each variable in your code. 
In order to know the type of a given variable, you can use
the intrinsic function `type`. For the variable you just created
you can find the type using
```{code-cell} python
type(a)
```
In the case above, you might want `a` to be defined
as a float instead of an integer. If that is the case, you can assign 
the type explicitly
```python
a = float(10)
```
Alternatively, you can add a point at the end
```python
a = 10.
```
The result will be the same.

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
In the few lines of code above, we have used the most straightforward 
types in Python, **integers**, which lack a decimal part,
and **floating-point** numbers.
Using floats and integers you can do all sorts of computations in Python,
 very much like you would in a regular calculator. You can for example 
use operators like `+` and `-`, which are called **unary operators**, 
because they act on a single numeric value. You can perform multiplications,
 using the operator `*`, divisions with `/`, and integer divisions with `//`.
Using `%` you will obtain the remainder of a division. Also you can 
exponentiate using the operator `**`.

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
```{exercise}
:nonumber:
:class: dropdown

Create two integer or floating point variables, `a` and `b`, and 
assign them values. Perform the following operations and print the 
results:
* Addition of `a` and `b`.
* Subtraction of `b  from `a`.
* Multiplication of `a` and `b`.
* Integer division of `a` by `b`.
* Modulus (remainder) of `a` divided by `b`.
* Exponentiation of `a` raised to the power of `b`.
Check at every stage the types of the results.
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
multiplication means *repetition*. 

You can also perform
*membership* operators, to check whether an element is present
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

```{exercise}
:nonumber:
:class: dropdown

* Create a string variable `text` and assign it a text of your choice.
Use string methods to calculate the length of the string, 
convert the string to uppercase or lowercase and capitalize the first letter.

* Using string slicing, extract a substring from the middle of the `text` 
variable.

* Create two string variables, `str1` and `str2`, and assign them different 
text values. Concatenate `str1` and `str2` to create a new string.

* Use the `split()` method to split the text variable into a list of words.
```

### Lists, tuples and dictionaries
**Lists** are a very important type of **sequence**, which
in Python is a type of data structures that contain a 
collection of elements. In the last section, we have generated 
one such object
```python
['bread', ' butter', ' flour', ' milk']
```
which is of course a list of strings. 

Lists are defined when the list of elements is written inside square
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
```{exercise}
:nonumber:
:class: dropdown

 Create a list called fruits with three fruit names, and print the first and
 last elements of the fruits list. Add a new fruit to the list and 
remove a fruit. At every stage, print the length of the fruits list.

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

```{exercise}
:nonumber:
:class: dropdown

Create a dictionary called student with your name and age.
Print the student dictionary. Update the age to your current age.
Add your university as a new key.
Remove the "age" key. Print the updated student dictionary.
```
