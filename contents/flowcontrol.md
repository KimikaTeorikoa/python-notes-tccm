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

Another useful operator is `in`, which checks if a value is contained in a list,
tuple or dictionary.

For instance:
```python
1 in [1, 2, 3] # True
1 in [2, 3, 4] # False
```

Logical tests can be combined using the logical operators `and`, `or` and `not`. 
They work as follows:

For instance:
```python
True and False # False
True or False # True
not True # False
not False # True
```




## Loops (for while)

Loops are used to execute a block of code repeatedly.

## 	Iterators and generators

Iterators are objects that can be iterated upon.


## 	Comprehensions

Lists and dictionaries can be created in a very handy way.

## Error and exception handling


