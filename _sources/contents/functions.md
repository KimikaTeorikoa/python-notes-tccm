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
it will make sense to **abstract** some of the computations that you are doing
and isolate them into a separate piece of code, called a **function**.
Functions are useful for a number of reasons:
* They make your code more *readable*.
* Using functions you may *shorten* your code, avoiding repetitive actions.
* They make your code easier to *debug*.
* Functions may be *reused* in different programs.

## Built-in functions
In fact, we have been using functions since the beginning of our
journey with Python. The functions that can be used in any moment
in time just by typing them are called **built-in functions**.
The first one we used is the `print()`function. Incidentally, since
we have used it, we can check what type of object `print()` is
```{code-cell} python
print (type(print))
```
There are many other built-in functions, 
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
def my_function(arg1, arg2, ...):
    # A number of actions that take place inside the function
    ...
    return value1, value2
```
As you see, to write a function we must first use the `def` statement,
after which come the name of your function, with parenthesis, and its function
arguments, `arg1` and `arg2`, will follow. Then starts an indented block 
that can be as long
as required. The function usually will end with a `return` statement, 
which can return one or multiple values, or nothing at all. We call this type
of function with no returns **void function**.  When we write one of
them  we can omit the `return` statement altogether.

Functions must be defined before they are used. This will normally mean
that the function is written *above* the main code we are running.
If one function calls another function, then it does not matter which
order they appear as long as the code is not executed. For example,
in this code, 
```{code-cell} python
def call_tell_me_yes():
    tell_me_yes()
    
def tell_me_yes():
    print ("yes")
    
call_tell_me_yes()
```
it does not matter that the first function is calling the second
function, as both are defined at runtime.

## Scope of variables
It is important to note that whatever happens outside the function
is visible to the function, but not the other way around. 
Variables defined in the main program are said to have **global scope**.
But variables defined inside the function have **local scope**,
so whatever happens in a function remains inside the function. To
make variables global in scope you can declare them as a **global** or
return them as a result. To make a variable `x`inside a function global,
you just need to type
```python
def my_function(arg):
    global x 
    # Perform a number of actions
    ...
```

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
`d` is local in scope, it is not part of the **namespace** known to the main
code.

## Types of arguments
So far we have used arguments in the simplest of ways. There
can be functions without arguments, in which case the function
call would be done with an empty parenthesis. 
```{code-cell} python
def say_hello():
    print ('Hello!')
    
say_hello()
```

Also, arguments can
be of different types. Check the following example
```{code-cell} python
def power_of_n(x,n):
    return x**n
    
print (power_of_n(2, 3))
```
Here, both arguments `x` and `n` must be 
passed in all function calls. Failure to state a value for one of them
argument would return a `SyntaxError`.

However, we can write a function in a different way, if, for example,
one of the arguments has a typical value
```{code-cell} python
def power(x, n=2):
    return x**n
    
print ("n = 2 (default); result = %i"%power(2))
print ("n = 3 (non-default); result = %i"%power(2,3))
```
In this case, the function has a different behaviour for 
the argument `n`, which has a default value of 2
if it is not explicitly defined. 

In the last function above, `n` is a **keyword argument**,
because it has a name. When using keyword arguments, you
do not have to remember the order we call them.
For example
```{code-cell} python
def power(x=None, n=2):
    return x**n
    
print (power(x=2, n=3))
print (power(n=3, x=2))
```

When functions can accept an **arbitrary number of arguments**, you
can mark them with an asterisk `*`. For example, to sum
of numbers, irrespective of how many there are, you could write
```{code-cell} python
def sum_args(*args):
    result = 0
    for v in args:
        result += v
    return result
    
print (sum_args(1, 2))
print (sum_args(1, 2, 3))
```

Additionally, we may want to have an arbitrary number of keyword
arguments. In this case, you invoke the function using two
asterisks `**` instead of just one and call your function using
```python
def my_fun(*args, **kwargs):
    for i in args:
        # do something
        ...
    for k, v in kwargs:
        # do something else
        ...
```
You see that the `kwargs` are being unwrapped like a **dictionary**.

## Anonymous functions
In Python there is an alternative way of defining functions that
does not require the syntax we have used so far (with a `def` 
statement). You can instead use a `lambda` statement and use
a following syntax:
```python
my_function = lambda arg, [arg2, [arg3, ...]]: expression
```
An example of this type of function to calculate powers would be
```{code-cell} python
power = lambda x,y: x**y
print (power(2,3))
```
You see that we have compressed into a single line what we were doing 
before using a few more. As you probably guessed, anonymous functions
are particularly useful as one-liners, but may become cumbersome
to use for more sofisticated actions.

## Documenting functions
An important detail that we have left to the side so far is the need
to write documentation for your functions. In Python, function
(and module, and class) documentation comes in the form of **docstrings**. 
As you may expect, there are detailed recommendations on how to write
docstrings. You can find them in [PEP 257](https://peps.python.org/pep-0257/).
One of them is that we use triple quotes (`"""`) to write docstrings.

In summary, if we stick to functions for now, docstrings can consist on 
a **single line** --these are typical for very obvious actions--.
```python
def print_dog():
    """ Prints man's best friend """
    print ("dog")
```
Or, they can be longer, if there is need for greater detail. Typically,
**multi-line docstrings** start with a summary line, which is followed
by a blank line, and then the rest of the required documentation.
This often includes a description of the function arguments and returns.
Here is an example that we borrow from PEP 257
```python
def complex(real=0.0, imag=0.0):
    """Form a complex number.

    Keyword arguments:
    real -- the real part (default 0.0)
    imag -- the imaginary part (default 0.0)
    """
    if imag == 0.0 and real == 0.0:
        return complex_zero
    ...
```

Above, we saw that functions are objects too, hence having attributes.
The documentation becomes one of the function attributes, called
`__doc__`. For example, you can do the following
```{code-cell} python
def tell_me_your_name(*args):
    """Prompts user for name """
    print ("What's your name?")
    
print (tell_me_your_name.__doc__)
```

## Advanced topics
* Functional programming: `map`, `filter`
* Recursion