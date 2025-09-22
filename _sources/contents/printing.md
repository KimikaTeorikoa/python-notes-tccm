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

# Additional notes on I/O

At this point, we already acquired the basic skills to write a 
working Python code. An important part of the code is reading external
data and writing results. We already learned the basics on 
[Input/Output](fundamentals.io) and,
in this chapter, we give a closer look on how to print messages 
and results to the screen  and files with a proper format.

## The `print` function

The central function for printing in Python is `print`. It can be
used to print a single variable (of any kind) or a sequence of 
variables.

```python
print('Hello world!', 1.5, True, [1, 2, 3], sep=' | ', end='\n--\n')
```

Some keyword arguments can be used to modify the output. For example, 
we can specify the character(s) at the end of the line with the `end` 
keyword. The default value is the newline character `\n` (new line), 
so if we use `end=''` we will get subsequent statements printed in 
the same line. Another keyword that tune the output is `sep`, which
specifies the string use as separator between variables (if a sequence 
of variables is given). The default value is a space.

Another important keyword is `file`, which specifies the output
stream. The argument must be a file object, usually generated with the
`open` function. Note that the file should be writable (i.e., using
the keyword `w` on opening). The default value 
is `sys.stdout`, which is the standard output stream. 

```{exercise}
:nonumber:
:class: dropdown

Write a program that prints the numbers from 0 to 10 in the same line,
waiting 1 second between each number. 

*Hint*: use the `time.sleep` function to wait 1 second. 
You may also need to add the `flush=True` keyword to the `print` function
to avoid buffering the output.
```

Before closing this section, we will look at an alternative way to
print variables, i.e., through the `write` method of file objects.
One of the main differences with the `print` function is that the
`write` method does not add a newline character at the end.

```python
# Set file object to standard output
f = sys.stdout

# With write method
f.write('Hello world!\n')

# With print function
print('Hello world!', file=f)
```

## Formatting your output

Note that while we can print any variable with the `print` function 
it does not allow us to specify the format of the output (e.g., 
specify the number of decimals for a float). To do this, we need to 
generate a string that will contain the variables with the desired
format. We then pass such a string to the `print` function.

There are three ways to generate a string with variables:

- `format` method of the string.
- `f-strings` (formatted strings, since Python 3.6).
- String modulo operator (`%`).

In the two first cases, the string is a template that contains placeholders
for the variables identified by curly braces `{}`. The more general
syntax is `{<variableID>:<format>}`. The way `<variableID>` is 
specified depends on the method used to generate the string. Namely, 
the `format()` function contains the variables as arguments, and `<variableID>`
is the position of the variable in the argument list. If no identifier
is used, the variables are used in the order they appear in the 
argument list. The `f-strings` are defined with the `f`
modifier, i.e., `f"my_string"`. They are a bit more flexible, and allow to 
directly use a variable, or any valid Python expression as `<variableID>`. 

The third method uses the `%` character as placeholder within the string,
with syntax `%<format>`, where in this case `<format>` must be specified.
The variables to substitute are given after the string, using a tuple
if more than one is given.

```python
# Using the format method
print('The value of x is {} and the value of y is {}'.format(x, y))

# Using f-strings
print(f'The value of x is {x} and the value of y is {y}')

# Using string modulo operator (%)
print('The value of x is % and the value of y is %' % (x, y))
```

The `<format>` field is a string that specifies the format of the variable, 
with details such as the total width, the number of decimals or
the alignment. The most common syntax is `<align>W<type>`, where
`<align>` is the alignment (not available with `%` method, and optional
with the other two), `W` is the total width (and may also 
include the number of positions after the period for floats as `W.n`), and 
`<type>` is the format type. The most common types are:

* `s`: string (actually not necessary to specify, since it is the default)
* `d`: integer (again, not necessary)
* `f`: float in decimal format
* `e`: float in scientific notation
* `g`: float in scientific notation or decimal format, or integer, depending on the value

The alignment can be specified with the `<align>` part of the format, and the 
most usual options are: `<` (left aligned), `>` (right aligned), and `^`
(centered). The default is left alignment for strings, and right alignment
for numbers.

Let's take a look to the outcome of different formats for the same
variables.

```{code-cell} python
x,y = 1,2
print(f'The value of x is {x:<10d} and the value of y is {y:<10}')
print(f'The value of x is {x:^10.2f} and the value of y is {y:^10.2e}')
print(f'The value of x is {x:>10.2g} and the value of y is {y:>10.2e}')
```

```{exercise}
:nonumber:
:class: dropdown

Write a code snippet that prints two columns with the values of the
time and the position from $t=0$ to $t=10$ every $dt=0.2$, 
following the equation

$$
x(t) =  -1.5 + 2.0 t + \frac{1}{2} 0.5 t^2
$$

Use 2 decimals for the time and 4 for the position.
```

## Using specific libraries for I/O

Through this chapter, we have seen how to read and write files using
some python built-in functions. However, in many cases, you will find
that, while working with specific file formats, some libraries will do 
this task more conveniently. For example,
arrays can be read/written with [NumPy's specific functions](numpy.io), 
molecular structure with the [IO module of ASE](ase) and
data frames can be read and written with [Pandas](pandas).
You will see some examples of these libraries in the corresponding chapters.

