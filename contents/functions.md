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

# Functions	
We have already explored many things that can be done using Python, and
specifically in the [previous chapter](flowcontrol.md), how to do
them over and over again. Sometimes, as your code gets more complicated
it will make sense to **abstract** some of the things that you are doing
and isolate them into a separate piece of code, called a **function**.

## Built-in functions
In fact, we have been using functions since the beginning of our
journey with Python. The functions that can be used in any moment
in time just by typing them are called **built-in functions**.
The first one we used is the `print()`function. There are many others, 
like `abs()`, `all()`, `any()`, `dir()`, `enumerate()`, `int()`, 
`len()`, `range()` or `type()`. A complete list of built-in 
functions can be found in the [Python official
documentation](https://docs.python.org/3/library/functions.html#built-in-functions).

As you see functions are always invoked with a parenthesis `()`
where we include the function **arguments**. These arguments
are the set of variables we pass on to a function for it to work with.
When we call a function, we typically expect something back. 
In the case of the `print()` function we expect output in the `stdout`.
In many other cases, what the function **returns** is sent into
one or more variables
```python
y = my_function(x, a, b)
```
In the example above, we have a function called `my_function()` which
receives three arguments (`x`, `a` and `b`) and returns some data
into `y`.

## Writing functions
But in addition to the built-in functions that are always available,
you can write your own functions. The basic syntax is as follows:
```python
def my_function(argument1, argument2, ...):
    # A number of actions that take place inside the function
    ...
    return value1, value2
```
As you see, to write a function we must first use the `def` statement,
after which the name of your function, with parenthesis, and its function
arguments, will follow. Then starts an indented block that can be as long
as required. The function usually will end with a `return` statement, 
which can return one or multiple values, or nothing at all. In that case,
you can omit the `return` statement altogether.

## Scope of variables
It is important to note that whatever happens outside the function
is visible to the function, but not the other way around. 
Variables defined in the main program are said to have **global scope**.
But variables defined inside the function have **local scope**,
so whatever happens in a function remains inside the function. To
make variables global in scope you can declare them as a **global** or
return them as a result.

Let's look carefully at the following example
```{code-cell} python
def test_scope(val):
    print ("a = %i"%a)
    print ("b = %i"%val)
    c = a + val
    d = a - val
    return  c

a = 10
b = 20
c = test_scope(b)
print ("c = %i"%c)
print ("d = %i"%d)

```
Let's analyze what just happened. First, we are defining a function, 
`test_scope()` that takes an argument called `val`. Then, in the main
piece of code, we are defining three variables `a`, `b` and `c`. 
The first variable `a` is known to the function, even if it is not passed 
as an argument explicitly. Because it is in the main code, its scope is
global. The second variable `b` is passed to the function
but named as `val` internally (the function would still know who is `b`).
Finally, `c` is returned by the function as the sum of the other
two variables. However, when trying to print the other variable calculated
by the function (`d = a - val`), we are getting a `NameError`. Because
`d` is local in scope, it is not part of the namespace known to the main
code.

## Types of arguments
### Environments	
