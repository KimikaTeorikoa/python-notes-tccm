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

# Control structures

## A note on indentation
In Python, the way that a program looks is 
very much determined by indentation. This 
differs from what we will find in other languages
like Fortran or C, where formatting is not so
important. In this chapter we will use indentation
exhaustively, because as you will see it is essential
for flow control. 
When you write an `if` statement in
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
(4 spaces is the preferred option in 
[PEP8](https://peps.python.org/pep-0008/#indentation)). 
This may feel like a nuisance if you have
experience in some other programming language, but
will help orient yourself when reading code in the
long run.

## Conditionals (if)

In many cases, we want to execute a piece of code
depending on the results of one or more conditions (which we will call logical tests).
This is actually one of the main control flow structures in Python (and most
programming languages). The basic syntax in Python is as follows:
```python
if condition1:
    # A number of actions that take place if condition1 is True
    ...
elif condition2:
    # A number of actions that take place if condition2 is True
    ...
else:
    # A number of actions that take place if none of the above is True
    ...
```

**Logical tests and conditional operators**

At this point, some words on logical tests and conditional operators are in order.
Logical tests are expressions that evaluate to `True` or `False` 
and correspond to variables of type `bool` (Booleans, as seen in the 
[previous chapter](fundamentals.md)).

Logical tests are built using conditional operators. 
The most common ones are `==` (equal), `!=` (not equal), `>` (greater than), 
`<` (less than), `>=` (greater than or equal to), `<=` (less than or equal to).
As you would expect, these comparison operators give the following results:

```python
1 == 2 # False
1 != 2 # True
1 < 2 # True
1 > 2 # False
```

:::{note}
There is another operator, `is`, that is similar to `==` but checks if two variables
are the same **object** (point to the same address in memory). 
In general, for two different variables with the same value, this operator evaluates to `False`.
For instance, if we compare two different float variables with the same value.

```python
x = 1.0
y = 1.0
x == y # True
x is y # False
```

But this is not always the case for integers, because Python caches the most commonly used
integers, so that they are the same object in memory.

```python
x = 1
y = 1
x == y # True
x is y # True

# But with larger integers this is not the case:
x = 1554223641
y = 1554223641
x == y # True
x is y # False
```

So, in general, we use `==` to compare values (i.e., what we normally intend to do) and `is` to compare objects.
:::

Another useful operator is `in`, which checks if a value is contained in a list,
tuple or dictionary.

For instance:
```python
1 in [1, 2, 3] # True
1 in [2, 3, 4] # False
```

Logical tests can be combined using the logical operators `and`, `or` and `not`. 
They work as follows:

```python
True and False # False
True or False # True
not True # False
not False # True
```

Finally, it is also worth mentioning that some non-boolean values can be evaluated
as `True` or `False`. For instance, the number `0` is evaluated as `False`, while
any other number is evaluated as `True`. Similarly, the empty string `""` is evaluated
as `False`, while any other string is evaluated as `True`. An empty list also evaluates
as `False`, while any other list evaluates as `True`.
Such equivalences can be made explicit using the `bool` function.

```python
bool(0) # False
bool(1) # True
bool("") # False
bool("Hello") # True
bool([]) # False
bool([1, 2, 3]) # True
```


## Loops (for while)

Loops are used to execute a block of code repeatedly.

## 	Iterators and generators

Iterators are objects that can be iterated upon.


## 	Comprehensions

Lists and dictionaries can be created in a very compact way using comprehensions.
The list is created based on another list, dictionary or iterable object, and
a condition can be added to filter the elements that are included in the new list.
The syntax is as follows:

```python
new_list = [expression for item in iterable if condition == True]
```

For instance, we can create a list with the squares of the numbers from 1 to 10
as follows:

```python
squares = [x**2 for x in range(1, 11)]
```

We can also create a list with the squares of the even numbers from 1 to 10
as follows:

```python
squares = [x**2 for x in range(1, 11) if x % 2 == 0]
```
Comprehensions can also be used to create dictionaries. For instance, we can create

```python
squares = {x: x**2 for x in range(1, 11)}
```

Note that we need to iterate over keys and values. This can also be done generating 
a list of tuples in-place. For instance, we can create a dictionary that maps letters
to their position in the alphabet as follows:

```{code-cell} python
letters = { chr(j):i for (i,j) in enumerate(range(65,65+26), start=1) }
print('A:',letters['A'])
print('Z:',letters['Z'])
```

In the above example, `enumerate` is a built-in function that returns a list of tuples
(actually an iterator)
over a sequence of values (in this case, another iterator, `range`), together with 
their index (starting from 1 as specified with the `start` argument). The `chr()` function
converts an integer to the corresponding ASCII character.


## Error and exception handling

While running the code, some errors may occur, e.g. divide by zero, trying to open
a non-existing file... Python raises a specific object that identifies the error. 
These are called exceptions. 

For instance the `ZeroDivisionError` exception is raised
when trying to divide by zero.

```{code-cell} python
1/0
```

And `FileNotFoundError` is raised when trying to open a non-existing file.

```{code-cell} python
f = open('missing_file.txt')
```

As shown above, when an exception is raised, the code stops running and an informative error 
message is printed. Some context information is also provided, e.g. the call stack, which shows
the sequence of function calls that led to the error.

Built-in exceptions are listed in the [Python documentation](https://docs.python.org/3/library/exceptions.html#bltin-exceptions).
Some of the most commonly raised exceptions are:

- `ZeroDivisionError`: raised when trying to divide by zero.
- `NameError`: raised when a variable is not defined.
- `TypeError`: raised when an operation or function is applied to an object of inappropriate type.
- `ValueError`: raised when a built-in operation or function receives an argument that has the 
   right type but an inappropriate value.
- `IndexError`: raised when trying to access an element in a list using an invalid index.
- `KeyError`: raised when a dictionary key is not found.
- `FileNotFoundError`: raised when trying to open a non-existing file.
- `ImportError`: raised when an import statement fails.
- `SyntaxError`: raised when there is an error in Python syntax.
- `IndentationError`: raised when indentation is not correct.

Errors raised while running the code can be handled using the `try` and `except` statements.
The basic syntax is as follows:

```python
try:
    # Code that may raise an exception
    ...
except ExceptionName:
    # Code that is executed if the exception ExceptionName is raised
```

For instance, we can handle a division by zero error as follows:

```python
try:
    1/0
except ZeroDivisionError:
    print("Division by zero!")
```

The `try` statement can be followed by multiple `except` statements, to handle different
types of exceptions specifically. If no exception is specified, the `except` statement
will handle any exception. For instance, we can handle a division by zero error, a
name error, specifically, and then any other exception as follows:

```{code-cell} python
try:
    print(x)
except ZeroDivisionError:
    print("Division by zero!")
except TypeError:
    print("Incorrect type!")
except:
    print("Something else went wrong!")
    # In this case we had a NameError, but we don't handle it specifically
```

Moreover, `else` and `finally` statements can also be added to the
`try` statement. The `else` statement is executed if no exception is raised, and the
`finally` statement is always executed, regardless of whether an exception is raised or not.
The general syntax is as follows:

```python
try:
    # Code that may raise an exception
    ...
except ExceptionName1:
    # Code that is executed if the exception ExceptionName1 is raised
    ...
except ExceptionName2:
    # Code that is executed if the exception ExceptionName2 is raised
    ...
except:
    # Code that is executed if any other exception is raised
    ...
else:
    # Code that is executed if no exception is raised
    ...
finally:
    # Code that is always executed, regardless of whether an exception is raised or not
    ...
```

We can also raise exceptions in our code using the `raise` statement, using one of the built-in
exceptions or a custom exception (we are not going to cover custom exceptions in this course).
For instance:

```{code-cell} python
x = -1
if x < 0:
    raise ValueError("x cannot be negative")
```
