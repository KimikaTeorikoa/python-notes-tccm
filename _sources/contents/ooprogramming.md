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
**Attributes** are *named elements associated to an object*. 
The way we invoke them is similar to using variables from a module 
that we have imported (e.g. `math.pi`). 
**Methods** are *functions intrinsic to a specific type of object*. 
For example, list objects have an
associated method called `append`:
```{code-cell} python
s = ['txema', 'david', 'kirill']
s.append('javier')
print (s)
```
## Classes
In addition to the intrinsic types built into Python, we can define
our own types of objects that may be useful for our needs. **Classes**
are *user-defined types* and their use provides incredibly rich 
functionality in Python. Because classes carry their own specific
attributes and methods, we can use them to conveniently pack a set of data
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
we use the `__init__` method (note the two underscore characters at the
beginning and end of `init`). 
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
When we instantiate an object, the `__init__` method is invoked
and whatever takes place inside will be part of our object.
We can pass parameters to the `__init__` method, which normally
receive the same names as the attributes of the class. For example,
```{code-cell} python
class Cup(object):
    """Represents a cup someone can drink from"""
    def __init__(self, volume=1., owner='Jeremy', content=None):
        self.volume = volume
        self.owner = owner
        self.content = content
```
and in this way we may access the values that are packaged in the
class
```{code-cell} python
my_bigger_cup = Cup(volume=10)
print (mycup.volume)
```
This second instance of the class is identical to the first, just
with a 10 times bigger volume. But you do not necessarily have to pass
values to the attributes, as they have default values.
As we have seen, the attributes mutable and can be assigned different 
values for different instances of the class.

There are other special methods like `__init__`, like for example
the `__str__` method, which returns a string representation of 
an object. For example, we could write something like
```python
    def __str__(self):
        if not self.content:
            return 'An empty %s unit cup owned by %s'%(self.volume, self.owner)
        else:
            return 'A %s unit cup owned by %s filled with '%(self.volume, self.owner, self.content)
```

Additionally, we can
include a number of methods in our class. Cups, for example, 
can be filled with coffee or tea
```{code-cell} python
class Cup(object):
    """Represents a cup someone can drink from"""
    def __init__(self, volume=1., owner='Jeremy', content=None):
        self.volume = volume
        self.owner = owner
        self.content = content
        
    def __str__(self):
        if not self.content:
            return 'An empty %s unit cup owned by %s'%(self.volume, self.owner)
        else:
            return 'A %s unit cup owned by %s filled with %s'%(self.volume, self.owner, self.content)
        
    def fill(self, liquid):
        self.content = liquid
    
    def drink(self):
        if not self.content:
            print ('You cannot drink from an empty cup')
        else:
            self.content = None
```
This more complete class offers some additional functionality.
We can create a new cup, initally empty
```{code-cell} python
my_new_cup = Cup()
print (my_new_cup)
```
then fill it with coffee
```{code-cell} python
my_new_cup.fill('coffee')
print (my_new_cup)
```
and drink from it
```{code-cell} python
my_new_cup.drink()
print (my_new_cup)
```
Our class of the will complain if we try to empty it again
```{code-cell} python
my_new_cup.drink()
```

## The Call special method 
Another special method, `__call__`, allows you to write a class
and call it like a function. It's a powerful feature that can 
make instances behave like callable objects.
Here's a simple example
```{code-cell} python
class Counter(object):
    def __init__(self):
        self.value = 0
    
    def increment(self):
        self.value += 1
    
    def __call__(self):
        self.increment()
        return self.value
```
As you see, we have written a `__call__` method that first
invokes the `increment` method and then returns a value.
Let's see it in action. First we create an instance of
the class
```{code-cell} python
my_counter = Counter()
```
and then we "call" it like a function a number of times
```{code-cell} python
print(my_counter())
print(my_counter())
print(my_counter())
```
If your class represents a mathematical function, then it
is good practice to add a `__call__` method to your class.
You can check whether an object has a `__call__` method 
using the build-in function `callable`
```{code-cell} python
print(callable(my_counter))
```
There are other special methods like `__init__`,
`__str__` or `__call__` but you will learn about them as you need.

## Copying instances of classes
You can generate as many instances of a class as you need,
and you can also **copy** instances of a class, but in the latter
case you must be a bit careful. We will illustrate this
with an example class called `ItemList`
```{code-cell} python
class ItemList(object):
    def __init__(self, items=[]):
        self.items = items
    
    def add_item(self, item):
        self.items.append(item)
        
    def remove_item(self, item):
        if item in self.items:
            self.items.remove(item)
    
    def get_items(self):
        return self.items
```
We will first create an instance of this class and fill it 
with fruits
```{code-cell} python
original_list = ItemList()
[original_list.add_item(x) for x in ["Apple", "Banana", "Orange"]]
```
Now we may want to make a copy of this list, and add some more stuff
```{code-cell} python
import copy
shallow_copy = copy.copy(original_list)
shallow_copy.add_item("Grapes")
```
However, this operation also unintentionally changes the original list
```{code-cell} python
print("Original List:", original_list.get_items())
print("Shallow Copy:", shallow_copy.get_items())
```
If we want to make an independent copy of the list we must
use `deepcopy` instead
```{code-cell} python
deep_copy = copy.deepcopy(original_list)
deep_copy.remove_item("Grapes")
print("Original List:", original_list.get_items())
print("Deep Copy:", deep_copy.get_items())
```
As you see, after having used `deepcopy` the original copy remains unchanged.

## Static methods and attributes
**Static attributes and methods** belong to a class rather than an
instance of the class. They are typically used for values or 
functions that are related to the class but do not require access 
to your specific instance of the class. 

Here we define a class `MathUtils` with a static attribute `pi`, 
representing the value of the mathematical constant $pi$ and
a static method that calculates the factorial of a number
recursively
```{code-cell} python
class MathUtils:
    pi = 3.14159 
    
    @staticmethod
    def factorial(n):
        if n == 0 or n == 1:
            return 1
        else:
            return n * MathUtils.factorial(n - 1)
```
We can hence access the value of $pi$
```{code-cell} python
print("Value of pi:", MathUtils.pi)
```
or calculate the factorial of an integer as
```{code-cell} python
num = 5
factorial_result = MathUtils.factorial(num)
print("The factorial of %g is %g"%(num, factorial_result))
```


## Inheritance
Sometimes you will find that there exists a natural hierarchy 
between your classes: dogs are for example, a specific type of
animal. Let's start writing a general class, called `Animal`
```{code-cell} python
class Animal:
    def __init__(self, name, species):
        self.name = name
        self.species = species
    
    def make_sound(self):
        pass  # This method will be overridden in subclasses
```
Continuing with our dog-as-a-type-of-animal example, we can write 
a new class for dogs thah inherits the methods of the existing class
```{code-cell} python
class Dog(Animal):
    def __init__(self, name):
        super().__init__(name, species="Dog")

    def make_sound(self):
        return "Woof!"
```
You may instead be a cat person, and still inherit from `Animal` 
```{code-cell} python
class Cat(Animal):
    def __init__(self, name):
        super().__init__(name, species="Cat")

    def make_sound(self):
        return "Meow!"

```
Then we can generate instances of our `Dog` and `Cat` classes
```{code-cell} python
dog = Dog("Buddy")
cat = Cat("Whiskers")

animals = [dog, cat]

for animal in animals:
    print(f"{animal.name} the {animal.species} says: {animal.make_sound()}")
```