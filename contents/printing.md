# Additional notes on I/O

At this point, we already acquired the basic skills to write a 
working Python code, including flow control. We have also got
some basic knowledge on Input/Output in the Chapter on 
[Python fundamentals](fundamentals.md).
In this chapter, we give a closer look on how to print messages 
and results to the screen  and files with a proper format, as well 
as how to read data from files.

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
of variables is given). The default value is a space `' '.

Another important keyword is `file`, which specifies the output
stream. The argument must be a file object, generated with the
`open` function. Note that it should be writtable. The default value 
is `sys.stdout`, which is the standard output stream. 

```{exercise}
:nonumber:
:class: dropdown

Write a program that prints the numbers from 0 to 10 in the same line,
waiting 1 second between each number. 

Hint: use the `time.sleep` function to wait 1 second.
```

## Formatting your output

Note that while we can print any variable with the `print` function 
it does not allow us to specify the format of the output (e.g., 
specify the number of decimals for a float). To do this, we need to 
generate a string that will contain the variables with the desired
format. We then pass such a string to the `print` function.

There are two ways to generate a string with variables. The first
one is to use the `format` method of the string. The second one is
to use the `f-strings` (formatted strings) introduced in Python 3.6.
In both cases, the string is a template that contains placeholders
for the variables identified by curly braces `{}`. The more general
syntax is `{<variableID>:<format>}`. The way `<variableID>` is 
specified depends on the method used to generate the string. Namely, 
the `format` contains the variables as arguments, and `<variableID>`
is the position of the variable in the argument list. If no idenfier
is used, the variables are used in the order they appear in the 
argument list. The `f-strings` are strigs defined with the `f`
modifier, `f"my_string"`. They are a bit more flexible, and allow to 
directly use a variable, or any valid Python expression as `<variableID>`. 
Let's take a look to some equivalent ways to print two variables with these 
methods:

```python
# Using the format method
print('The value of x is {} and the value of y is {}'.format(x, y))
print('The value of x is {0} and the value of y is {1}'.format(x, y))
print('The value of x is {1} and the value of y is {0}'.format(y, x))

# Using f-strings
print(f'The value of x is {x} and the value of y is {y}')
```

The `<format>` is a string that specifies the format of the variable, 
with details such as the total width, the number of decimals, 
the alignment, etc. The most common syntax is `<align>W<type>`, where
`<align>` is the alignment (optional), `W` is the total width (and may also 
include the number of positions after the period for floats as `W.n`), and 
`<type>` is the type of the variable. The most common types are:

* `s`: string (actually not necessary to specify, since it is the default)
* `d`: integer (again, not necessary)
* `f`: float
* `e`: float in scientific notation
* `g`: float in scientific notation or decimal format, depending on the value

The alignment can be specified with the `<align>` part of the format, and the 
most usual options are: `<` (left aligned), `>` (right aligned), and `^`
(centered). The default is left aligned.

Let's take a look to some examples:

```python
print('The value of x is {:>10.2f} and the value of y is {:^10.2e}'.format(x, y))
print(f'The value of x is {x:>10.2f} and the value of y is {y:^10.2e}')
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

<!## Reading from files
<!
<!Once a file object is created with the `open` function, we can read
<!its content with different approaches. First we can use some
<!methods of the file object, such as:
<!
<!* `read`: reads the whole file as a single string
<!* `readline`: reads a single line (returns a string)
<!* `readlines`: reads the whole file as a list of lines (returns a list of strings)
<!
<!Note that both `read` and `readlines` read the whole file at once, so 
<!we may run into memory problems if the file is too large. The `readline`
<!needs to be called iteratively to read the whole file, line by line.
<!
<!Another approach is to iterate over the file object. Each iteration
<!returns a line of the file. I.e., this is similar to use the `readline`
<!over a loop, but looks more elegant. For example:
<!
<!```python
<!with open('myfile.txt', 'r') as f:
<!    for line in f:
<!        # do something with line, e.g., print it:
<!        print(line)
<!        
<!        # At each loop iteration, we can read additional lines
<!        # with the readline method
<!        line2 = f.readline()
<!```
<!
