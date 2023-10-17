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
Now that we have learnt the different types of data that
we can use in Python programs, it is time to start working
with them in **statements** that perform actions. Using flow 
control, we may be able to repeat something written in a 
statement for a number of iterations or act in one
way or another depending on the fulfillment of a condition.

## A note on indentation
In Python, the way that a program looks is 
very much determined by **indentation**. This 
differs from what we will find in other languages
like Fortran or C, where formatting is not so
important. In this chapter we will use indentation
exhaustively, because as you will see it is essential
for flow control.

Let's look at an `if` statement in
Python:
```python
if x < 12:
    print (x)
```
As you can see, we have indented the `print`
statement four positions to the right.
Had we not done this, the code simply would not run. 

```{exercise}
:nonumber:
:class: dropdown

Explore what happens when you do not respect
indentation. Can you use more or less spaces?
Can you write the code in a single line?
```

Different levels of indentation start where 
we have colons (`:`), and these have to be 
indented with respect to the previous level
of indentation. Be 
careful not to add white spaces where they do not
belong and use consistently tabs or spaces
(4 spaces is the preferred option in 
[PEP8](https://peps.python.org/pep-0008/#indentation)). 


```{hint}
This may feel like a nuisance if you have
experience in some other programming language, but
will help orient yourself when reading code in the
long run.
```

## Conditionals (if statements)
In many cases, we want to execute a piece of code
depending on the results of one or more conditions. 
We will call this type of statement **logical tests**.
This is one of the main control flow structures in Python and 
most other programming languages. 

The basic syntax in Python is as follows:
```python
if condition1:
    # Actions that take place if condition1 is True
    ...
elif condition2:
    # Actions that take place if condition2 is True
    ...
else:
    # Actions that take place if none of the above is True
    ...
```

### Logical tests and conditional operators

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

```{exercise}
:nonumber:
:class: dropdown

Write a code that uses non-booleans in logical tests, and check
how are they evaluated. You can follow the scheme below:

```python
if variable:
    print("This variable evaluates to True")
else:
    print("The variable evaluates to False")
```


## Loops (for / while)

Loops play a crucial role in automating repetitive tasks. Many times, we
will want to do the same thing over and over. Occasionally, we may want to 
stop when a condition is or is not fulfilled. In these situations, loops become
 essential tools for processing data and performing calculations. 

Imagine you have a list of numbers, and you want to calculate their sum. 
```python
numbers = [1, 2, 3, 4, 5]
```
To find the sum of these numbers, you could manually add them up:
```python
numbers = [1, 2, 3, 4, 5]
Sum = numbers[0] + numbers[1] + numbers[2] + numbers[3] + numbers[4]
```

However, what if you had a list with hundreds or thousands of numbers? 
Performing this calculation manually would be 
impractical. This is precisely where loops come into play.

### For loops

Let's explore a `for` loop in Python to calculate the sum of numbers in a list.
 The for loop iterates over each element
in the list and accumulates the sum.

```python
numbers = [1, 2, 3, 4, 5]
total_sum = 0  # Initialize the sum

for num in numbers:
    total_sum = total_sum + num  # Add each number to the sum
    
print("The sum of numbers is:", total_sum)
```

Here, the `for` loop allows us to automate the process of summing the elements in the list, 
making it efficient and scalable. Note that the indentation is required and the colon at the end of the line.

The `range()` function is often used in conjunction 
with `for` loops to create a sequence of numbers that you can iterate through. The `range()` function generates a sequence
of numbers based on the parameters you provide. It has three possible forms:

- `range(stop)`: Creates a sequence from 0 up to (but not including) the `stop` value
- `range(start, stop)`: Creates a sequence from start up to (but not including) the stop value.
- `range(start, stop, step)`: Creates a sequence from start up to (but not including) the stop value, 
with a specified step size.

You then use a `for` loop to iterate over the elements in the generated sequence. In each iteration of the loop, 
a variable takes on the value of the current element in the sequence.

Here's a basic example:

```python
for i in range(5):
    print(i)
```

In this example, the `range(5)` generates a sequence from 0 to 4, and the for loop iterates through these values.

```python
0
1
2
3
4
```

**While loops**

Now, we consider a scenario where you want to find the sum of numbers until a certain condition is met. 
For instance, you want to find the sum of numbers until the cumulative sum exceeds 10.

```python
numbers = [1, 2, 3, 4, 5]
total_sum = 0
index = 0

while total_sum <= 10:
    total_sum = total_sum + numbers[index]
    index = index + 1

print("The sum of numbers until the cumulative sum exceeds 10 is:", total_sum)
```

```{warning}
Take care when using `while` loops, as they can easily lead to infinite loops.
```

```{exercise}
:nonumber:
:class: dropdown

Write a code snippet that calculates and prints the sum of all even numbers from 1 to
 a given positive integer using both a for loop and a while loop. 
Compare the results obtained from both loops.

```


## 	Iterators and generators

**Iterators** and **generators** are both mechanisms in Python for working with sequences of data. They allow you to iterate through a collection of items one at a time. 
They both allow you to loop through a sequence of values, but they differ in how they are implemented and when they generate values.

### Iterators

An iterator is an object that represents a *stream of data*. 
It allows you to traverse a sequence of elements one at a time without loading the entire sequence into memory. 
In Python, an iterator is implemented using two methods: `__iter__()` and `__next__()`
.
   - `__iter__()`: Returns the iterator object itself and is called when you create an iterator from an iterable object (e.g., a list or a custom class).
   
   - `__next__()`: Retrieves the next element from the iterator and raises the `StopIteration` exception when there are no more elements.

Below is an example of a simple iterator:
```python
lista = ['Charles', 'John', 'Python', 'pato', 3]
a = iter(lista)
print(a)
print(next(a))

while True:
    try:
        print(next(a)) # fetch the the position in the array
    except: 
        break # exit the loop on error
```

You can also create your own custom iterators by defining **classes**
 with `__iter__()` and `__next__()` methods, or you can use built-in Python functions like `iter()` and `next()` with iterable objects.

```python
class Doublen:
    def __init__(self, start, end):
        self.current = start
        self.end = end

    def __iter__(self):
        return self

    def __next__(self):
        if self.current > self.end:
            raise StopIteration
        x=2*self.current
        self.current += 1
        return x

my_iterator = Doublen(1, 8)
print(my_iterator)

for ii in my_iterator:
    print(ii)
```
The output will be

```python
<__main__.Doublen object at 0x106b4de10>
2
4
6
8
10
12
14
16
```
We will look in greater detail into how to write your own classes in the
[Object Oriented Programming](ooprogramming.md) chapter.

### Generators
A generator is a concise way to create iterators. 
The main difference is that a generator is a function that contains one or more `yield` statements. 
When you call a generator function, it returns a generator object, which you can use to iterate through the values produced by the `yield` statements.
Generator functions use the `yield` keyword to yield values one at a time, and they automatically retain their execution state between calls.

You may create a generator function by defining a function with one or more `yield` statements. 
When you call this function, it doesn't execute immediately but returns a generator object. 
You can then iterate through the values by
calling the generator's `__next__()` method or using a `for` loop.

```python
def number_generator(start, end):
    current = start
    while current < end:
        yield current
        current = current + 1
        
my_generator = number_generator(1, 5)
print(my_generator)
for num in my_generator:
    print(num)
```

In summary, both iterators and generators allow you to work with sequences of data, but generators provide a more concise and memory-efficient way to create iterators, especially for situations where data generation is dynamic or resource-intensive.

## 	Comprehensions

Lists and dictionaries can be created in a very compact way using comprehensions.
The list is created based on another list, dictionary or iterable object. 
A condition can be added to filter the elements that are included in the new list.
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

```{exercise}
:nonumber:
:class: dropdown

Write a list comprehension that generates a list of squares for even numbers from 1 to 10.

```

## Error and exception handling

While running your code, some errors are bound to occur. 
For example, when you divide
a value by zero or when you try to open a non-existing file... 
Python raises a specific object that identifies the error. 
These are called **exceptions**. 
Exceptions are a crucial mechanism for dealing with errors, unexpected behavior, and exceptional cases in Python programs.
For instance, the `ZeroDivisionError` exception is raised
when trying to divide by zero.

```{code-cell} python
1/0
```
And `FileNotFoundError` is raised when trying to open a non-existing file.
```{code-cell} python
f = open('missing_file.txt')
```

As shown above, when an exception is raised, the code stops running and an informative error 
message is printed. 
Some context information is also provided, e.g. the call stack, which shows
the sequence of function calls that led to the error.

Built-in exceptions are listed in the [Python documentation](https://docs.python.org/3/library/exceptions.html#bltin-exceptions).
Some of the most commonly raised exception classes are:

- `ZeroDivisionError`: raised when trying to divide by zero.
- `NameError`: raised when a variable is not defined.
- `TypeError`: raised when an operation or function is applied to an object of inappropriate type.
- `ValueError`: raised when a built-in operation or function receives an argument that has the 
   right type but an inappropriate value.
- `IndexError`: raised when trying to access an element in a list using an invalid index.
- `OSError`: raised when a system function returns a system-related error, including I/O failures such as “file not found” or “disk full”.
- `KeyError`: raised when a dictionary key is not found.
- `FileNotFoundError`: raised when trying to open a non-existing file.
- `ImportError`: raised when an import statement fails.
- `SyntaxError`: raised when there is an error in Python syntax.
- `IndentationError`: raised when indentation is not correct.

Errors raised while running the code can be caught and handled using the `try` and `except` statements.
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

As you see, when an exception is handled, the code continues running
without crashing the program.
However, we may be missing some information from the original error message.
In this type of situations we may use a slightly different syntax:
```python
try:
    file = open("non_existent_file.txt", "r")
    content = file.read()
    file.close()
except FileNotFoundError as e:
    print(f"An error occurred: {e}")
```
As you see, using `except <ExceptionType> as e` we are catching the exception and 
printing the original error message.

The `try` block contains the code that might raise an exception,
and it can be followed by multiple `except` statements to handle different
types of exceptions with specific actions. 
If no exception is specified, the `except` statement
will handle any exception. 

In the example below, we handle a division by zero error and a
name error specifically, and then any other exception:

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
    # Executed if the exception ExceptionName1 is raised
    ...
except ExceptionName2:
    # Executed if the exception ExceptionName2 is raised
    ...
except:
    # Executed if any other exception is raised
    ...
else:
    # Executed if no exception is raised
    ...
finally:
    # Always executed, regardless of whether an exception is raised or not
    ...
```


We can also raise exceptions in our code using the `raise` statement, using one of the built-in exceptions or a custom exception (we are not going to cover custom exceptions in this course).
For instance:

```{code-cell} python
x = -1
if x < 0:
    raise ValueError("x cannot be negative")
```
