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
# Object Oriented Programming 
For as long as we have been working with Python, we have been using
**objects**. In fact, everything in Python is an object, which
makes using objects naturally inescapable. Specifically, when we 
introduced the different types of 
[variables](fundamentals.md#Data-Types)
that we can define, we saw that each of them was associated to 
specific **methods**, which varied depending of the data type.
Here, we will make explicit what we have been using intuitively
in previous chapters. We will also introduce **classes**, which 
are central to object-oriented programming in Python.

## Attributes and methods
We will start with some definitions.
There are two fundamental properties of objects, attributes and methods.
**Attributes** are named elements associated to an object. 
The way we invoke them is similar to using variables from a module 
that we have imported. 

**Methods** are functions intrinsic to a specific type of object. 
For example, list objects have an
associated method called `append`:
```{code-cell} python
s = ['txema', 'david', 'kirill']
s.append('javier')
print (s)
```
## Classes
In addition to the intrinsic types built into Python, we can define
our own type of objects that may be useful for our needs. **Classes**
are user-defined types and their use provides incredibly rich 
functionality in Python. Because classes carry their own specific
attributes and methods, we can conveniently pack a set of data
and corresponding functions operating on the data. Most of the time,
you can live without classes and simply write code using simpler
data structures. But if you start using classes, you will find
that they provide an extremely elegant framework to solve problems.

### A simple class example
We will start defining a simple class that we will call `Cup`. To
define the class we will use
```python
class Cup(object):
    """Represents a cup someone can drink from"""
```
Note that we are using CapWords for class definitions, following
[PEP8](https://peps.python.org/pep-0008/#class-names).
Cups usually are of some colour and have a volume that can be filled
with some liquid. Cups also normally have an owner.
These will be the cup attributes and we will assign an initial value 
to them when the class is initialized. In order to initialize a class,
we use the `__init__` method.
```{code-cell} python
class Cup(object):
    """Represents a cup someone can drink from"""
    def __init__(self):
        self.volume = 1.
        self.owner = 'Jeremy'
        self.content = None
```
In order to create an **instance** of this class, you can do
something as simple as 
```{code-cell} python
mycup = Cup()
```
and in this way we may access the values that are packaged in the
class
```{code-cell} python
print (mycup.volume)
```
The attributes are mutable and can be assigned different values 
for different instances of the class. Additionally, we can
include a number of methods in our class. Cups, for example, 
can be filled with coffee or tea
```{code-cell} python
class Cup(object):
    """Represents a cup someone can drink from"""
    def __init__(self):
        self.volume = 1.
        self.owner = 'Jeremy'
        self.content = None
        
    def fill(self, liquid):
        self.content = liquid
    
    def empty(self):
        if not self.content:
            print ('An empty cup cannot be emptied')
        else:
            self.content = None
```
This more complete class offers some additional functionality.
```{code-cell} python
my_new_cup = Cup()
print (my_new_cup.content)
my_new_cup.fill('coffee')
print (my_new_cup.content)
```

Once written, you can generate as many instances of a class 
as you want.


* Copying / Deep copying
* Inheritance: