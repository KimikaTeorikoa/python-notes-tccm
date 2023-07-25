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

Conditional statements are used to execute a block 
of code depending on the results of one or more logical tests. The basic syntax 
is as follows:
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

### Logical tests and conditional operators
At this point, some words on logical tests and conditional operators are in order.
Logical tests are expressions that evaluate to `True` or `False` 
and correspond to variables of type `bool`. 
Conditional expressions are built using conditional operators. 
The most common ones are `==` (equal), `!=` (not equal), `>` (greater than), 
`<` (less than), `>=` (greater than or equal to), `<=` (less than or equal to).

For instance:
```python
1 == 2 # False
1 != 2 # True
1 < 2 # True
1 > 2 # False
```

:::{note}
There is another operator, `is`, that is similar to `==` but checks if two variables
are the same **object** (point to the same address in memory). 
In general, for two different variables with the same value ,this operator evaluates to `False`.
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

So, in general, we use `==` to compare values and `is` to compare objects.
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

Lists and dictionaries can be created in a very handy way.

## Error and exception handling


