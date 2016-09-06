---
title: "Python Cheat Sheet"
description: "Python Cheat Sheet"
category: Programming
tags: [programming]
sidebar:
  nav: "new_side"
---


# Table of contents

* TOC
{:toc}


# Preliminaries
```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from pandas import DataFrame, Series
```

(<a href="#top">Back to top</a>)

It is also possible to write Python code which is compatible with Python 2.7 and 3.x at the same time, using Python __future__ imports. __future__ imports allow you to write Python 3 code that will run on Python 2, so check out the Python 3 tutorial.

# Single line comments start with a number symbol.

```python
""" Multiline strings can be written
    using three "s, and are often used
    as comments
"""
```

(<a href="#top">Back to top</a>)
<hr>

# 1. Primitive Datatypes and Operators

## You have numbers
```python
3  # => 3
```

(<a href="#top">Back to top</a>)
<hr>

## Math is what you would expect
```python
1 + 1  # => 2
8 - 1  # => 7
10 * 2  # => 20
35 / 5  # => 7
```

(<a href="#top">Back to top</a>)
<hr>

## Division is a bit tricky. It is integer division and floors the results automatically.
```python
5 / 2  # => 2
```

(<a href="#top">Back to top</a>)
<hr>

## To fix division we need to learn about floats.
```python
2.0     # This is a float
11.0 / 4.0  # => 2.75 ahhh...much better
```

(<a href="#top">Back to top</a>)
<hr>

## Result of integer division truncated down both for positive and negative.
```python
5 // 3     # => 1
5.0 // 3.0 # => 1.0 # works on floats too
-5 // 3  # => -2
-5.0 // 3.0 # => -2.0
```

(<a href="#top">Back to top</a>)
<hr>

## Note that we can also import division module(Section 6 Modules) to carry out normal division with just one '/'.
```python
from __future__ import division
11/4    # => 2.75  ...normal division
11//4   # => 2 ...floored division
```

(<a href="#top">Back to top</a>)
<hr>

## Modulo operation
```python
7 % 3 # => 1
```

(<a href="#top">Back to top</a>)
<hr>

## Exponentiation (x to the yth power)
```python
2**4 # => 16
```

(<a href="#top">Back to top</a>)
<hr>

## Enforce precedence with parentheses
```python
(1 + 3) * 2  # => 8
```

(<a href="#top">Back to top</a>)
<hr>

## Boolean Operators
Note "and" and "or" are case-sensitive

```python
True and False #=> False
False or True #=> True
```

(<a href="#top">Back to top</a>)
<hr>

## Note using Bool operators with ints
```python
0 and 2 #=> 0
-5 or 0 #=> -5
0 == False #=> True
2 == True #=> False
1 == True #=> True
```

(<a href="#top">Back to top</a>)
<hr>

## negate with not
```python
not True  # => False
not False  # => True
```

(<a href="#top">Back to top</a>)
<hr>

## Equality is ==
```python
1 == 1  # => True
2 == 1  # => False
```

(<a href="#top">Back to top</a>)
<hr>

## Inequality is !=
```python
1 != 1  # => False
2 != 1  # => True
```

(<a href="#top">Back to top</a>)
<hr>

## More comparisons
```python
1 < 10  # => True
1 > 10  # => False
2 <= 2  # => True
2 >= 2  # => True
```

(<a href="#top">Back to top</a>)
<hr>

## Comparisons can be chained!
```python
1 < 2 < 3  # => True
2 < 3 < 2  # => False
```

(<a href="#top">Back to top</a>)
<hr>

## Strings

### Strings are created with " or '
```python
"This is a string."
'This is also a string.'
```

(<a href="#top">Back to top</a>)
<hr>

### Strings can be added too!
```python
"Hello " + "world!"  # => "Hello world!"
```

(<a href="#top">Back to top</a>)
<hr>

### Strings can be added without using '+'
```python
"Hello " "world!"  # => "Hello world!"
```

(<a href="#top">Back to top</a>)
<hr>

### ... or multiplied
```python
"Hello" * 3  # => "HelloHelloHello"
```

(<a href="#top">Back to top</a>)
<hr>

### A string can be treated like a list of characters
```python
"This is a string"[0]  # => 'T'
```

(<a href="#top">Back to top</a>)
<hr>

### String formatting with %
Even though the % string operator will be deprecated on Python 3.1 and removed later at some time, it may still be good to know how it works.

```python
x = 'apple'
y = 'lemon'
z = "The items in the basket are %s and %s" % (x,y)
```

(<a href="#top">Back to top</a>)
<hr>

### A newer way to format strings is the format method.
This method is the preferred way

```python
"{} is a {}".format("This", "placeholder")
"{0} can be {1}".format("strings", "formatted")
```

(<a href="#top">Back to top</a>)
<hr>

## You can use keywords if you don't want to count.

```python
"{name} wants to eat {food}".format(name="Bob", food="lasagna")
```

(<a href="#top">Back to top</a>)
<hr>

## None is an object
```python
None  # => None
```

(<a href="#top">Back to top</a>)
<hr>

## Don't use the equality "==" symbol to compare objects to None
Use "is" instead

```python
"etc" is None  # => False
None is None  # => True
```

(<a href="#top">Back to top</a>)
<hr>

## The 'is' operator tests for object identity. This isn't

* very useful when dealing with primitive values, but is
* very useful when dealing with objects.

## Any object can be used in a Boolean context.
The following values are considered falsey:

* - None
* - zero of any numeric type (e.g., 0, 0L, 0.0, 0j)
* - empty sequences (e.g., '', (), [])
* - empty containers (e.g., {}, set())
* - instances of user-defined classes meeting certain conditions
* see: https://docs.python.org/2/reference/datamodel.html#object.__nonzero__

All other values are truthy (using the bool() function on them returns True).

```python
bool(0)  # => False
bool("")  # => False
```

(<a href="#top">Back to top</a>)
<hr>


# 2. Variables and Collections

## Python has a print statement
```python
print "I'm Python. Nice to meet you!" # => I'm Python. Nice to meet you!
```

(<a href="#top">Back to top</a>)
<hr>

## Simple way to get input data from console

```python
input_string_var = raw_input("Enter some data: ") # Returns the data as a string
input_var = input("Enter some data: ") # Evaluates the data as python code
```

(<a href="#top">Back to top</a>)
<hr>

Warning: Caution is recommended for input() method usage<br>
Note: In python 3, input() is deprecated and raw_input() is renamed to input()

## No need to declare variables before assigning to them.

```python
some_var = 5    # Convention is to use lower_case_with_underscores
some_var  # => 5
```

(<a href="#top">Back to top</a>)
<hr>

## Accessing a previously unassigned variable is an exception.
See Control Flow to learn more about exception handling.

```python
some_other_var  # Raises a name error
```

(<a href="#top">Back to top</a>)
<hr>

## if can be used as an expression
Equivalent of C's '?:' ternary operator

```python
"yahoo!" if 3 > 2 else 2  # => "yahoo!"
```

(<a href="#top">Back to top</a>)
<hr>

### Lists

## Lists store sequences

```python
li = []
```

(<a href="#top">Back to top</a>)
<hr>

### You can start with a prefilled list
```python
other_li = [4, 5, 6]
```

(<a href="#top">Back to top</a>)
<hr>

### Add stuff to the end of a list with append

```python
li.append(1)    # li is now [1]
li.append(2)    # li is now [1, 2]
li.append(4)    # li is now [1, 2, 4]
li.append(3)    # li is now [1, 2, 4, 3]
```

(<a href="#top">Back to top</a>)
<hr>

### Remove from the end with pop

```python
li.pop()        # => 3 and li is now [1, 2, 4]
```

(<a href="#top">Back to top</a>)
<hr>

### Let's put it back

```python
li.append(3)    # li is now [1, 2, 4, 3] again.
```

(<a href="#top">Back to top</a>)
<hr>

### Access a list like you would any array

```python
li[0]  # => 1
```

(<a href="#top">Back to top</a>)
<hr>

### Assign new values to indexes that have already been initialized with =

```python
li[0] = 42
li[0]  # => 42
li[0] = 1  # Note: setting it back to the original value
```

(<a href="#top">Back to top</a>)
<hr>

### Look at the last element

```python
li[-1]  # => 3
```

(<a href="#top">Back to top</a>)
<hr>

### Looking out of bounds is an IndexError

```python
li[4]  # Raises an IndexError
```

(<a href="#top">Back to top</a>)
<hr>

### You can look at ranges with slice syntax.

(It's a closed/open range for you mathy types.)

```python
li[1:3]  # => [2, 4]
```

(<a href="#top">Back to top</a>)
<hr>

### Omit the beginning

```python
li[2:]  # => [4, 3]
```

(<a href="#top">Back to top</a>)
<hr>

### Omit the end

```python
li[:3]  # => [1, 2, 4]
```

(<a href="#top">Back to top</a>)
<hr>

### Select every second entry

```python
li[::2]   # =>[1, 4]
```

(<a href="#top">Back to top</a>)
<hr>

### Reverse a copy of the list

```python
li[::-1]   # => [3, 4, 2, 1]
```

(<a href="#top">Back to top</a>)
<hr>

###Use any combination of these to make advanced slices li[start:end:step]


### Remove arbitrary elements from a list with "del"
```python
del li[2]   # li is now [1, 2, 3]
```

(<a href="#top">Back to top</a>)
<hr>

### You can add lists
```python
li + other_li   # => [1, 2, 3, 4, 5, 6]
```

(<a href="#top">Back to top</a>)
<hr>

Note: values for li and for other_li are not modified.

### Concatenate lists with "extend()"
```python
li.extend(other_li)   # Now li is [1, 2, 3, 4, 5, 6]
```

(<a href="#top">Back to top</a>)
<hr>

### Remove first occurrence of a value
```python
li.remove(2)  # li is now [1, 3, 4, 5, 6]
li.remove(2)  # Raises a ValueError as 2 is not in the list
```

(<a href="#top">Back to top</a>)
<hr>

### Insert an element at a specific index
```python
li.insert(1, 2)  # li is now [1, 2, 3, 4, 5, 6] again
```

(<a href="#top">Back to top</a>)
<hr>

### Get the index of the first item found
```python
li.index(2)  # => 1
li.index(7)  # Raises a ValueError as 7 is not in the list
```

(<a href="#top">Back to top</a>)
<hr>

### Check for existence in a list with "in"
```python
1 in li   # => True
```

(<a href="#top">Back to top</a>)
<hr>

### Examine the length with "len()"
```python
len(li)   # => 6
```

(<a href="#top">Back to top</a>)
<hr>

## Tuples

### Tuples are like lists but are immutable.

```python
tup = (1, 2, 3)
tup[0]   # => 1
tup[0] = 3  # Raises a TypeError
```

(<a href="#top">Back to top</a>)
<hr>

### You can do all those list thingies on tuples too

```python
len(tup)   # => 3
tup + (4, 5, 6)   # => (1, 2, 3, 4, 5, 6)
tup[:2]   # => (1, 2)
2 in tup   # => True
```

(<a href="#top">Back to top</a>)
<hr>

### You can unpack tuples (or lists) into variables

```python
a, b, c = (1, 2, 3)     # a is now 1, b is now 2 and c is now 3
d, e, f = 4, 5, 6       # you can leave out the parentheses
```

(<a href="#top">Back to top</a>)
<hr>

### Tuples are created by default if you leave out the parentheses

```python
g = 4, 5, 6             # => (4, 5, 6)
```

(<a href="#top">Back to top</a>)
<hr>

### Now look how easy it is to swap two values

```python
e, d = d, e     # d is now 5 and e is now 4
```

(<a href="#top">Back to top</a>)
<hr>


## Dictionary

### Dictionaries store mappings

```python
empty_dict = {}
```

(<a href="#top">Back to top</a>)
<hr>

### Here is a prefilled dictionary

```python
filled_dict = {"one": 1, "two": 2, "three": 3}
```

(<a href="#top">Back to top</a>)
<hr>

### Look up values with []

```python
filled_dict["one"]   # => 1
```

(<a href="#top">Back to top</a>)
<hr>

### Get all keys as a list with "keys()"

```python
filled_dict.keys()   # => ["three", "two", "one"]
```

(<a href="#top">Back to top</a>)
<hr>

Note - Dictionary key ordering is not guaranteed.
Your results might not match this exactly.

### Get all values as a list with "values()"

```python
filled_dict.values()   # => [3, 2, 1]
```

(<a href="#top">Back to top</a>)
<hr>

Note - Same as above regarding key ordering.

### Iterate over keys, values
```python
for word, count in sorted(count_words(filename).items()):
    print word, count
```
### join dictionary keys into string
```python
'<br/>'.join(['%s:: %s' % (key, value) for (key, value) in d.items()])
```

### Check for existence of keys in a dictionary with "in"

```python
"one" in filled_dict   # => True
1 in filled_dict   # => False
```

(<a href="#top">Back to top</a>)
<hr>

### Looking up a non-existing key is a KeyError

```python
filled_dict["four"]   # KeyError
```

(<a href="#top">Back to top</a>)
<hr>

### Use "get()" method to avoid the KeyError

```python
filled_dict.get("one")   # => 1
filled_dict.get("four")   # => None
```

(<a href="#top">Back to top</a>)
<hr>

### The get method supports a default argument when the value is missing

```python
filled_dict.get("one", 4)   # => 1
filled_dict.get("four", 4)   # => 4
```

(<a href="#top">Back to top</a>)
<hr>

note that filled_dict.get("four") is still => None
(get doesn't set the value in the dictionary)

### set the value of a key with a syntax similar to lists

```python
filled_dict["four"] = 4  # now, filled_dict["four"] => 4
```

(<a href="#top">Back to top</a>)
<hr>

### "setdefault()" inserts into a dictionary only if the given key isn't present

```python
filled_dict.setdefault("five", 5)  # filled_dict["five"] is set to 5
filled_dict.setdefault("five", 6)  # filled_dict["five"] is still 5
```

(<a href="#top">Back to top</a>)
<hr>

## Sets

### Sets store ... well sets (which are like lists but can contain no duplicates)

```python
empty_set = set()
```

(<a href="#top">Back to top</a>)
<hr>

### Initialize a "set()" with a bunch of values

```python
some_set = set([1, 2, 2, 3, 4])   # some_set is now set([1, 2, 3, 4])
```

(<a href="#top">Back to top</a>)
<hr>

### order is not guaranteed, even though it may sometimes look sorted

```python
another_set = set([4, 3, 2, 2, 1])  # another_set is now set([1, 2, 3, 4])
```

(<a href="#top">Back to top</a>)
<hr>

### Since Python 2.7, {} can be used to declare a set

```python
filled_set = {1, 2, 2, 3, 4}   # => {1, 2, 3, 4}
```

(<a href="#top">Back to top</a>)
<hr>

### Add more items to a set

```python
filled_set.add(5)   # filled_set is now {1, 2, 3, 4, 5}
```

(<a href="#top">Back to top</a>)
<hr>

### Do set intersection with &

```python
other_set = {3, 4, 5, 6}
filled_set & other_set   # => {3, 4, 5}
```

(<a href="#top">Back to top</a>)
<hr>

### Do set union with |

```python
filled_set | other_set   # => {1, 2, 3, 4, 5, 6}
```

(<a href="#top">Back to top</a>)
<hr>

### Do set difference with -

```python
{1, 2, 3, 4} - {2, 3, 5}   # => {1, 4}
```

(<a href="#top">Back to top</a>)
<hr>

### Do set symmetric difference with ^

```python
{1, 2, 3, 4} ^ {2, 3, 5}  # => {1, 4, 5}
```

(<a href="#top">Back to top</a>)
<hr>

### Check if set on the left is a superset of set on the right

```python
{1, 2} >= {1, 2, 3} # => False
```

(<a href="#top">Back to top</a>)
<hr>


### Check if set on the left is a subset of set on the right

```python
{1, 2} <= {1, 2, 3} # => True
```

(<a href="#top">Back to top</a>)
<hr>

### Check for existence in a set with in

```python
2 in filled_set   # => True
10 in filled_set   # => False
```

(<a href="#top">Back to top</a>)
<hr>

# 3. Control Flow

## Let's just make a variable
```python
some_var = 5
```

(<a href="#top">Back to top</a>)
<hr>

## If
Here is an if statement. Indentation is significant in python! prints "some_var is smaller than 10"

```python
if some_var > 10:
    print "some_var is totally bigger than 10."
elif some_var < 10:    # This elif clause is optional.
    print "some_var is smaller than 10."
else:           # This is optional too.
    print "some_var is indeed 10."
```

(<a href="#top">Back to top</a>)
<hr>

## For
```python
"""
For loops iterate over lists
prints:
    dog is a mammal
    cat is a mammal
    mouse is a mammal
"""
for animal in ["dog", "cat", "mouse"]:
    # You can use {0} to interpolate formatted strings. (See above.)
    print "{0} is a mammal".format(animal)

"""
```

(<a href="#top">Back to top</a>)
<hr>

## Range

```python
"range(number)" returns a list of numbers
from zero to the given number
prints:
    0
    1
    2
    3
"""
for i in range(4):
    print i

"""
"range(lower, upper)" returns a list of numbers
from the lower number to the upper number
prints:
    4
    5
    6
    7
"""
for i in range(4, 8):
    print i

"""
```

(<a href="#top">Back to top</a>)
<hr>

## While
While loops go until a condition is no longer met.
prints:
    0
    1
    2
    3
"""
x = 0
while x < 4:
    print x
    x += 1  # Shorthand for x = x + 1
```

(<a href="#top">Back to top</a>)
<hr>

## Handle exceptions with a try/except block
Works on Python 2.6 and up:

```python
try:
    # Use "raise" to raise an error
    raise IndexError("This is an index error")
except IndexError as e:
    pass    # Pass is just a no-op. Usually you would do recovery here.
except (TypeError, NameError):
    pass    # Multiple exceptions can be handled together, if required.
else:   # Optional clause to the try/except block. Must follow all except blocks
    print "All good!"   # Runs only if the code in try raises no exceptions
finally: #  Execute under all circumstances
    print "We can clean up resources here"
```

(<a href="#top">Back to top</a>)
<hr>

### Instead of try/finally to cleanup resources you can use a with statement
```python
with open("myfile.txt") as f:
    for line in f:
        print line
 ```

(<a href="#top">Back to top</a>)
<hr>       
        
# 4. Functions

## Use "def" to create new functions

```python
def add(x, y):
    print "x is {0} and y is {1}".format(x, y)
    return x + y    # Return values with a return statement
```

(<a href="#top">Back to top</a>)
<hr>

## Calling functions with parameters

```python
add(5, 6)   # => prints out "x is 5 and y is 6" and returns 11
```

(<a href="#top">Back to top</a>)
<hr>

## Another way to call functions is with keyword arguments

```python
add(y=6, x=5)   # Keyword arguments can arrive in any order.
```

(<a href="#top">Back to top</a>)
<hr>

## You can define functions that take a variable number of positional args, which will be interpreted as a tuple by using *

```python
def varargs(*args):
    return args

varargs(1, 2, 3)   # => (1, 2, 3)
```

(<a href="#top">Back to top</a>)
<hr>


## You can define functions that take a variable number of keyword args, as well, which will be interpreted as a dict by using **

```python
def keyword_args(**kwargs):
    return kwargs
```

(<a href="#top">Back to top</a>)
<hr>

## Let's call it to see what happens

```python
keyword_args(big="foot", loch="ness")   # => {"big": "foot", "loch": "ness"}
```

(<a href="#top">Back to top</a>)
<hr>

## You can do both at once, if you like

```python
def all_the_args(*args, **kwargs):
    print args
    print kwargs
"""
all_the_args(1, 2, a=3, b=4) prints:
    (1, 2)
    {"a": 3, "b": 4}
"""
```

(<a href="#top">Back to top</a>)
<hr>

## When calling functions, you can do the opposite of args/kwargs! Use * to expand positional args and use ** to expand keyword args.
```python
args = (1, 2, 3, 4)
kwargs = {"a": 3, "b": 4}
all_the_args(*args)   # equivalent to foo(1, 2, 3, 4)
all_the_args(**kwargs)   # equivalent to foo(a=3, b=4)
all_the_args(*args, **kwargs)   # equivalent to foo(1, 2, 3, 4, a=3, b=4)
```

(<a href="#top">Back to top</a>)
<hr>

## you can pass args and kwargs along to other functions that take args/kwargs by expanding them with * and ** respectively
```python
def pass_all_the_args(*args, **kwargs):
    all_the_args(*args, **kwargs)
    print varargs(*args)
    print keyword_args(**kwargs)
```

(<a href="#top">Back to top</a>)
<hr>

## Function Scope
```python
x = 5

def set_x(num):
    # Local var x not the same as global variable x
    x = num # => 43
    print x # => 43

def set_global_x(num):
    global x
    print x # => 5
    x = num # global var x is now set to 6
    print x # => 6

set_x(43)
set_global_x(6)
```

(<a href="#top">Back to top</a>)
<hr>
## Python has first class functions
```python
def create_adder(x):
    def adder(y):
        return x + y
    return adder

add_10 = create_adder(10)
add_10(3)   # => 13
```

(<a href="#top">Back to top</a>)
<hr>
## There are also anonymous functions
```python
(lambda x: x > 2)(3)   # => True
(lambda x, y: x ** 2 + y ** 2)(2, 1) # => 5
```

(<a href="#top">Back to top</a>)
<hr>
## There are built-in higher order functions
```python
map(add_10, [1, 2, 3])   # => [11, 12, 13]
map(max, [1, 2, 3], [4, 2, 1])   # => [4, 2, 3]

filter(lambda x: x > 5, [3, 4, 5, 6, 7])   # => [6, 7]
```

(<a href="#top">Back to top</a>)
<hr>
## We can use list comprehensions for nice maps and filters
```python
[add_10(i) for i in [1, 2, 3]]  # => [11, 12, 13]
[x for x in [3, 4, 5, 6, 7] if x > 5]   # => [6, 7]
```

(<a href="#top">Back to top</a>)
<hr>

# 5. Classes

## We subclass from object to get a class.

```python
class Human(object):
    # A class attribute. It is shared by all instances of this class
    species = "H. sapiens"

    # Basic initializer, this is called when this class is instantiated.
    # Note that the double leading and trailing underscores denote objects
    # or attributes that are used by python but that live in user-controlled
    # namespaces. You should not invent such names on your own.
    def __init__(self, name):
        # Assign the argument to the instance's name attribute
        self.name = name

        # Initialize property
        self.age = 0


    # An instance method. All methods take "self" as the first argument
    def say(self, msg):
        return "{0}: {1}".format(self.name, msg)

    # A class method is shared among all instances
    # They are called with the calling class as the first argument
    @classmethod
    def get_species(cls):
        return cls.species

    # A static method is called without a class or instance reference
    @staticmethod
    def grunt():
        return "*grunt*"

    # A property is just like a getter.
    # It turns the method age() into an read-only attribute
    # of the same name.
    @property
    def age(self):
        return self._age

    # This allows the property to be set
    @age.setter
    def age(self, age):
        self._age = age

    # This allows the property to be deleted
    @age.deleter
    def age(self):
        del self._age
```

(<a href="#top">Back to top</a>)
<hr>


## Instantiate a class

```python
i = Human(name="Ian")
print i.say("hi")     # prints out "Ian: hi"

j = Human("Joel")
print j.say("hello")  # prints out "Joel: hello"
```

(<a href="#top">Back to top</a>)
<hr>
## Call our class method

```python
i.get_species()   # => "H. sapiens"
```

(<a href="#top">Back to top</a>)
<hr>
## Change the shared attribute

```python
Human.species = "H. neanderthalensis"
i.get_species()   # => "H. neanderthalensis"
j.get_species()   # => "H. neanderthalensis"
```

(<a href="#top">Back to top</a>)
<hr>
## Call the static method

```python
Human.grunt()   # => "*grunt*"
```

(<a href="#top">Back to top</a>)
<hr>
## Update the property

```python
i.age = 42
```

(<a href="#top">Back to top</a>)
<hr>
## Get the property

```python
i.age # => 42
```

(<a href="#top">Back to top</a>)
<hr>
## Delete the property

```python
del i.age
i.age  # => raises an AttributeError
```

(<a href="#top">Back to top</a>)
<hr>

# 6. Modules

## You can import modules

```python
import math
print math.sqrt(16)  # => 4
```

(<a href="#top">Back to top</a>)
<hr>
## You can get specific functions from a module

```python
from math import ceil, floor
print ceil(3.7)  # => 4.0
print floor(3.7)   # => 3.0
```

(<a href="#top">Back to top</a>)
<hr>
## You can import all functions from a module. Warning: this is not recommended
```python
from math import *
```

(<a href="#top">Back to top</a>)
<hr>
## You can shorten module names

```python
import math as m
math.sqrt(16) == m.sqrt(16)   # => True
```

(<a href="#top">Back to top</a>)
<hr>
## you can also test that the functions are equivalent

```python
from math import sqrt
math.sqrt == m.sqrt == sqrt  # => True
```

(<a href="#top">Back to top</a>)
<hr>

Python modules are just ordinary python files. You can write your own, and import them. The name of the module is the same as the name of the file. <br>
You can find out which functions and attributes defines a module.

```python
import math
dir(math)
```

(<a href="#top">Back to top</a>)
<hr>

# 7. Advanced

## Generators

### Generators help you make lazy code

```python
def double_numbers(iterable):
    for i in iterable:
        yield i + i
```

(<a href="#top">Back to top</a>)
<hr>
A generator creates values on the fly.
Instead of generating and returning all values at once it creates one in each iteration.  This means values bigger than 15 wont be processed in double_numbers.<br>
Note xrange is a generator that does the same thing range does.
Creating a list 1-900000000 would take lot of time and space to be made. xrange creates an xrange generator object instead of creating the entire list like range does.

We use a trailing underscore in variable names when we want to use a name that would normally collide with a python keyword

```python
xrange_ = xrange(1, 900000000)
```

(<a href="#top">Back to top</a>)
<hr>
### will double all numbers until a result >=30 found

```python
for i in double_numbers(xrange_):
    print i
    if i >= 30:
        break
```

(<a href="#top">Back to top</a>)
<hr>

## Decorators

### in this example beg wraps say Beg will call say. If say_please is True then it will change the returned message
```python
from functools import wraps


def beg(target_function):
    @wraps(target_function)
    def wrapper(*args, **kwargs):
        msg, say_please = target_function(*args, **kwargs)
        if say_please:
            return "{} {}".format(msg, "Please! I am poor :(")
        return msg

    return wrapper


@beg
def say(say_please=False):
    msg = "Can you buy me a beer?"
    return msg, say_please

```

(<a href="#top">Back to top</a>)
<hr>
