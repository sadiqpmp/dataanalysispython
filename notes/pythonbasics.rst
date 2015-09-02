=============
Python basics
=============

.. contents::


Your first program
------------------

Launch your favorite environment:

	- **IPython** shell by typing "ipython" from a Linux/Mac terminal, or from the Windows cmd shell
	- **Python** shell by typing "python" from a Linux/Mac terminal, or from the Windows cmd shell
	- **Spyder** includes both **IPython** and **Python** as interactive shells
	- `Wakari.io`_ has a variety of shells, including **Ipython** and **Python**
	
Once you have started the interpreter (wait for ``>>>`` is you use pure Python, or ``In [1]:`` if you use IPython), type::

	>>> print('Hello world!')
	Hello world!

Let's play around and see what we can get without any knowledge of programming. Try some simple math calculations::

	>>> 2*2
	4
	>>> 2+3
	5
	>>> 4*(2+3)
	20
	>>> 1/2
	0.5
	>>> 1/3
	0.3333333333333333
	>>> 5-10
	-5
	>>> 0/0
	Traceback (most recent call last):
	  File "<stdin>", line 1, in <module>
	ZeroDivisionError: division by zero

Everything seems to work as expected. The last line produces some internal complaints - we will get back to it later.

We can define some variables and ask the shell who they are::

	>>> a = 2
	>>> type(a)
	<class 'int'>
	>>> b = .1
	>>> type(b)
	<class 'float'>
	>>> c = 'Hello'
	>>> type(c)
	<class 'str'>

Just to test the sanity of the language we can try adding up different variable types::

	>>> a + b
	2.1
	>>> c + c
	'HelloHello'
	>>> a + c
	Traceback (most recent call last):
	  File "<stdin>", line 1, in <module>
	TypeError: unsupported operand type(s) for +: 'int' and 'str'

Clearly, Python does not know how to add up integers to strings. Neither do we...

What if we call something that does not exist yet? ::

	>>> d
	Traceback (most recent call last):
	  File "<stdin>", line 1, in <module>
	NameError: name 'd' is not defined

Variable names can only contain numbers, letters (both upper and lower case), and underscores (_). They must begin with a letter or an underscore and are CaSe SeNsItIve. Some words are reserved in Python and so cannot be used for variable names.


Native Data Types
-----------------

Numbers
~~~~~~~

There are three numeric types:

	- integers (``int``)
	- floating point (``float``)
	- complex (``complex``)

Hopefully, we will not need the last one. But if you see something like ``3+5j`` or ``6-7J``, you know you are looking at ``complex`` type.

Note that if you want to define a ``float``, you have to use the dot (``.``), otherwise the output is an integer. For example, ::

	>>> type(1)
	<class 'int'>
	>>> type(1.)
	<class 'float'>
	>>> type(float(1))
	<class 'float'>
	>>> type(int(1.))
	<class 'int'>
	>>> type(0)
	<class 'int'>
	>>> type(0.)
	<class 'float'>
	>>> type(.0)
	<class 'float'>
	>>> type(0.0)
	<class 'float'>

This was extremely important in Python 2 and was the source of many inadvertent errors (try dividing 1 by 2 - you'd be surprised). With Python 3 not anymore, but the general advice of being explicit in what you mean is still there.

Division (``/``) always returns a ``float``. To do floor division and get an integer result (discarding any fractional result) you can use the ``//`` operator; to calculate the remainder you can use ``%``::

	>>> 17 / 3  # classic division returns a float
	5.666666666666667
	>>> 17 // 3  # floor division discards the fractional part
	5
	>>> 17 % 3  # the % operator returns the remainder of the division
	2
	>>> 5 * 3 + 2  # result * divisor + remainder
	17

Notice one way of commenting your code: just use ``#`` after the code and before any text.

Calculating powers is done with ``**`` operator. ::

	>>> 2**2
	4
	>>> 3**3
	27
	>>> 4**.5
	2.0


Booleans
~~~~~~~~

``bool`` type is essential for any programming logic. Normally, truth and falcity are defined as ``True`` and ``False``::

	>>> print(x)
	True
	>>> x = True
	>>> print(x)
	True
	>>> type(x)
	<class 'bool'>
	>>> y = False
	>>> print(y)
	False
	>>> type(y)
	<class 'bool'>

Additionally, all non-empty and non-zero values are interpreted by ``bool()`` function as ``True``, while all empty and zero values are ``False``::

	>>> print(bool(1), bool(1.), bool(-.1))
	True True True
	>>> print(bool(0), bool(.0), bool(None), bool(''), bool([]))
	False False False False False


Strings
~~~~~~~

Strings can be difined using both single (``'...'``) or double quotes (``"..."``). Backslash can be used to escape quotes. ::

	>>> 'spam eggs'  # single quotes
	'spam eggs'
	>>> 'doesn\'t'  # use \' to escape the single quote...
	"doesn't"
	>>> "doesn't"  # ...or use double quotes instead
	"doesn't"
	>>> '"Yes," he said.'
	'"Yes," he said.'
	>>> "\"Yes,\" he said."
	'"Yes," he said.'
	>>> '"Isn\'t," she said.'
	'"Isn\'t," she said.'

The ``print()`` function produces a more readable output, by omitting the enclosing quotes and by printing escaped and special characters::

	>>> '"Isn\'t," she said.'
	'"Isn\'t," she said.'
	>>> print('"Isn\'t," she said.')
	"Isn't," she said.
	>>> s = 'First line.\nSecond line.'  # \n means newline
	>>> s  # without print(), \n is included in the output
	'First line.\nSecond line.'
	>>> print(s)  # with print(), \n produces a new line
	First line.
	Second line.

If you don't want characters prefaced by ``\`` to be interpreted as special characters, you can use `raw strings` by adding an ``r`` before the first quote:

	>>> print('C:\some\name')  # here \n means newline!
	C:\some
	ame
	>>> print(r'C:\some\name')  # note the r before the quote
	C:\some\name

Python is very sensitive to code aesthetics (see `Style Guide`_). In particular, you shoud restrict yourself to 79 characters in one line! Use parenthesis to break long strings::

	>>> text = ('Put several strings within parentheses '
	            'to have them joined together.')
	>>> text
	'Put several strings within parentheses to have them joined together.'

Strings can be constructed using math operators and by converting numbers into strings via ``str()`` function::

	>>> 2 * 'a' + '_' + 3 * 'b' + '_' + 4 * (str(.5) + '_')
	'aa_bbb_0.5_0.5_0.5_0.5_'

Note that Python can not convert numbers into strings automatically. Unless you use ``print()`` function or convert explicitly.::

	>>> 'a' + 1
	Traceback (most recent call last):
	  File "<stdin>", line 1, in <module>
	TypeError: Can't convert 'int' object to str implicitly
	>>> 'a' + str(1)
	'a1'
	>>> print('a', 1)
	a 1


Lists
~~~~~

Lists are very convenient and simplest data containers. Here is how we store a collection of numbers in a variable::

	>>> a = [1, 3, 5]
	>>> a
	[1, 3, 5]
	>>> type(a)
	<class 'list'>

Lists are not restricted to be uniform in types of their elements::

	>>> b = [5, 2.3, 'abc', [4, 'b'], a, print]
	>>> b
	[5, 2.3, 'abc', [4, 'b'], [1, 3, 5], <built-in function print>]

Lists can be modified::

	>>> a[1] = 4
	>>> a
	[1, 4, 5]

Lists can be merged or repeated::

	>>> a + a
	[1, 4, 5, 1, 4, 5]
	>>> 3 * a
	[1, 4, 5, 1, 4, 5, 1, 4, 5]

You can add one item to the end of the list inplace::

	>>> a.append(7)
	>>> a
	[1, 4, 5, 7]

or add a few items::

	>>> a.extend([0, 2])
	>>> a
	[1, 4, 5, 7, 0, 2]

Note the difference::

	>>> a = [1, 3, 5]
	>>> b = [1, 3, 5]
	>>> a.append([2, 4, 6])
	>>> b.extend([2, 4, 6])
	>>> a
	[1, 3, 5, [2, 4, 6]]
	>>> b
	[1, 3, 5, 2, 4, 6]

If the end of the list is not what you want, insert the element after a specified position::

	>>> a.insert(1, .5)
	>>> a
	[1, 0.5, 4, 5, 7, 0, 2]

There are at least two methods to remove elements from a list::

	>>> x = ['a', 'b', 'c', 'b']
	>>> x.remove('b')
	>>> x
	['a', 'c', 'b']
	>>> x.remove('b')
	>>> x
	['a', 'c']
	>>> x.remove('b')
	Traceback (most recent call last):
	  File "<stdin>", line 1, in <module>
	ValueError: list.remove(x): x not in list

or::

	>>> y = ['a', 'b', 'c', 'b']
	>>> y.pop()
	'b'
	>>> y
	['a', 'b', 'c']
	>>> y.pop(1)
	'b'
	>>> y
	['a', 'c']

Here is how you sort a list without altering the original object, and inplace::

	>>> x = ['a', 'b', 'c', 'b', 'a']
	>>> sorted(x)
	['a', 'a', 'b', 'b', 'c']
	>>> x
	['a', 'b', 'c', 'b', 'a']
	>>> x.sort()
	>>> x
	['a', 'a', 'b', 'b', 'c']


Tuples
~~~~~~

On the first glance tuples are very similar to lists. The difference in definition is the usage of parentheses ``()`` (or even without them) instead of square brackets ``[]``::

	>>> t = 12345, 54321, 'hello!'
	>>> t
	(12345, 54321, 'hello!')
	>>> type(t)
	<class 'tuple'>
	>>> t = (12345, 54321, 'hello!')
	>>> t
	(12345, 54321, 'hello!')

The main difference is that tuples are *immutable* (impossible to modify)::

	>>> t[0] = 10
	Traceback (most recent call last):
	  File "<stdin>", line 1, in <module>
	TypeError: 'tuple' object does not support item assignment

Here are the reasons you want to use tuples:

	- Tuples are faster than lists. If you're defining a constant set of values and all you're ever going to do with it is iterate through it, use a tuple instead of a list.
	- It makes your code safer if you "write-protect" data that doesn't need to be changed.
	- Some tuples can be used as dictionary keys (specifically, tuples that contain immutable values like strings, numbers, and other tuples). Lists can never be used as dictionary keys, because lists are not immutable.

Dictionaries
~~~~~~~~~~~~

A dictionary is an unordered set of key-value pairs. There are some restrictions on what can be a key. In general, keys can not be mutable objects. Keys must be unique. Below are a few example of dictionary initialization::

	>>> empty_dict = dict()
	>>> empty_dict
	{}
	>>> empty_dict = {}
	>>> empty_dict
	{}
	>>> type(empty_dict)
	<class 'dict'>
	>>> grades = {'Ivan': 4, 'Olga': 5}
	>>> grades
	{'Ivan': 4, 'Olga': 5}
	>>> grades['Petr'] = 'F'
	>>> grades
	{'Ivan': 4, 'Petr': 'F', 'Olga': 5}
	>>> grades['Olga']
	5

Keys and values can be accessed separately if needed::

	>>> grades.keys()
	dict_keys(['Ivan', 'Olga'])
	>>> grades.values()
	dict_values([4, 5])


Sets
~~~~

A set is an unordered collection of unique values. A single set can contain values of any immutable datatype. Once you have two sets, you can do standard set operations like union, intersection, and set difference. Here is a brief demonstration::

	>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
	>>> basket
	{'orange', 'banana', 'pear', 'apple'}
	>>> type(basket)
	<class 'set'>
	>>> 'orange' in basket
	True
	>>> 'crabgrass' in basket
	False

Let's create a second set and see what we can do with both::

	>>> bag = {'banana', 'peach'}
	>>> basket - bag
	{'apple', 'orange', 'pear'}
	>>> basket | bag
	{'peach', 'orange', 'pear', 'banana', 'apple'}
	>>> basket & bag
	{'banana'}
	>>> basket ^ bag
	{'peach', 'apple', 'orange', 'pear'}

Indexing
--------

Python data containers (including strings and lists) can be `sliced` to access their specific parts. Counting in Python starts from zero. Keep this in mind when you want to access a specific character of a string::

	>>> word = 'Python'
	>>> word[0]  # character in position 0
	'P'
	>>> word[5]  # character in position 5
	'n'

Indices may also be negative numbers, to start counting from the right::

	>>> word[-1]  # last character
	'n'
	>>> word[-2]  # second-to-last character
	'o'
	>>> word[-6]
	'P'

Going beyond a single charcter::

	>>> word[0:2]  # characters from position 0 (included) to 2 (excluded)
	'Py'
	>>> word[2:5]  # characters from position 2 (included) to 5 (excluded)
	'tho'

Slice indices have useful defaults; an omitted first index defaults to zero, an omitted second index defaults to the size of the string being sliced.::

	>>> word[:2]  # character from the beginning to position 2 (excluded)
	'Py'
	>>> word[4:]  # characters from position 4 (included) to the end
	'on'
	>>> word[-2:] # characters from the second-last (included) to the end
	'on'

One could be interested only in even/odd characters in the string. In that case, we need a third index in the slice::

	>>> word[::2]
	'Pto'
	>>> word[1::2]
	'yhn'

Negative index in the third position of the slice reverses the count::

	>>> word[::-1]
	'nohtyP'
	>>> word[::-2]
	'nhy'

One way to remember how slices work is to think of the indices as pointing between characters, with the left edge of the first character numbered 0. Then the right edge of the last character of a string of n characters has index n, for example::

	 +---+---+---+---+---+---+
	 | P | y | t | h | o | n |
	 +---+---+---+---+---+---+
	 0   1   2   3   4   5   6
	-6  -5  -4  -3  -2  -1

Indexing with lists works in the same way. But on top of that, if your list contains other lists, or strings (or other **iterables**), then indexing becomes "layered"::

	>>> x = [[1, 3, 5], ['c', 'a', 'b']]
	>>> x[0][1]
	3
	>>> x[1][-2:]
	['a', 'b']


Control flow
------------

if/elif/else
~~~~~~~~~~~~

Writing conditional statements in Python is very easy. Start from ``if``, continue with ``elif``, and finish with ``else``. For example,

.. ipython::

	In [1]: if 2**2 == 4:
   	   ...:     print('Should be True')
   	   ...:     
	Should be True

Be careful to **respect the indentation depth**. The Ipython shell automatically increases the indentation depth after a column ``:`` sign; to decrease the indentation depth, go four spaces to the left with the Backspace key. Press the Enter key twice to leave the logical block.

.. ipython::

    In [1]: a = 10

    In [2]: if a == 1:
       ...:     print(1)
       ...: elif a == 2:
       ...:     print(2)
       ...: elif a == 3:
       ...:     print(3)
       ...: else:
       ...:     print('A lot')
       ...:
    A lot

Besides chceking for equality as in the previous examples, you can check for other statements evaluating to ``bool``. These are comparison operators: ``<, >, <=, =>``. Testing for equality of two objects is done with ``is`` operator::

	>>> a, b = 1, 1.
	>>> a == b
	True
	>>> a is b
	False

You can test whether an object belongs to a collection using ``in`` operator. Note that if a collection is of type ``dict``, then the search is done over dictionaries.::

	>>> a = [1, 2, 4]
	>>> 2 in a, 4 in a
	(True, True)
	>>> b = {'a': 3, 'c': 8}
	>>> 'c' in b
	True



Loops
~~~~~

If you do need to iterate over a sequence of numbers, the built-in function ``range()`` comes in handy. It generates arithmetic progressions:

.. ipython::

	In [7]: for i in range(4):
	   ...:     print(i)
	   ...:     
	0
	1
	2
	3

The ``for`` statement in Python differs a bit from what you may be used to in other programming languages. Rather than always iterating over an arithmetic progression of numbers (like in Pascal), or giving the user the ability to define both the iteration step and halting condition (as in C), Python's ``for`` statement iterates over the items of any sequence (a list or a string), in the order that they appear in the sequence.

.. ipython::

	In [6]: words = ['cat', 'window', 'bird']
	   ...: for w in words:
	   ...:     print(w, len(w))
	   ...:     
	cat 3
	window 6
	bird 4

Here is another example.

.. ipython::

	In [1]: for letter in 'Python':
	   ...:     print(letter)
	   ...:     
	P
	y
	t
	h
	o
	n

Coming back to ``range()`` function. It can have at most three arguments, ``range(first, last, step)``. Given this knowledge we can generate various sequences. Note that this function returns neither a list not a tuple. In fact, it is an object itself. In order to check what are the indices if we use ``range`` in a ``for`` loop, we can convert it to list using ``list()`` function. The reason behind this behavior is to save memory: ``range`` does not store the whole list, only its definition. ::

	>>> list(range(2, 10))
	[2, 3, 4, 5, 6, 7, 8, 9]
	>>> list(range(2, 10, 3))
	[2, 5, 8]
	>>> list(range(-2, -10, -3))
	[-2, -5, -8]

If you need to break out of the loop or skip an iteration, then you need to know two statements, ``break`` and ``continue``, respectively.

.. ipython::

	In [3]: a = [1, 0, 2, 4]
	   ...: for element in a:
	   ...:     if element == 0:
	   ...:         continue
	   ...:     print(1. / element)
	   ...:     
	1.0
	0.5
	0.25

or

.. ipython::

	In [4]: a = [1, 0, 2, 4]
	   ...: for element in a:
	   ...:     if element == 0:
	   ...:         break
	   ...:     print(1. / element)
	   ...:     
	1.0

Common use case is to iterate over items while keeping track of current index. Quick and dirty way to do this is:

.. ipython::

	In [5]: words = ('cool', 'powerful', 'readable')
	   ...: for i in range(0, len(words)):
	   ...:     print(i, words[i])
	   ...:     
	0 cool
	1 powerful
	2 readable

Yet, Python provides a much more elegant approach:

.. ipython::

	In [7]: for index, item in enumerate(words):
	   ...:     print(index, item)
	   ...:     
	0 cool
	1 powerful
	2 readable

Try iterating over dictionaries yourslef. You should find out that Python iterates over keys only. In order to have access to the whole pair, one should use ``items()`` method:

.. ipython::

	In [1]: grades = {'Ivan': 4, 'Olga': 5, 'Petr': 4.5}
	   ...: for key, val in grades.items():
	   ...:     print('%s has grade: %s' % (key, val))
	   ...:     
	Ivan has grade: 4
	Petr has grade: 4.5
	Olga has grade: 5

Here is how you might compute Pi:

.. ipython::

	In [1]: pi = 2
	   ...: for i in range(1, 1000):
	   ...:     pi *= 4*i**2 / (4*i**2 - 1)
	   ...: print(pi)
	   ...: 
	3.1408069608284657

Or if you want to stop after certain precision was achieved (a common use case), you might want to use ``while`` loop:

.. ipython::

	In [1]: pi, error = 2, 1e10
	   ...: while error > 1e-3:
	   ...:     pi *= 4*i**2 / (4*i**2 - 1)
	   ...:     error = abs(pi - 3.141592653589793)
	   ...: print(pi)
	   ...: 
	3.1405927760475945

List comprehensions
~~~~~~~~~~~~~~~~~~~

List comprehensions provide a concise way to create lists. Common applications are to make new lists where each element is the result of some operations applied to each member of another sequence or iterable, or to create a subsequence of those elements that satisfy a certain condition.

For example, assume we want to create a list of squares, like:

.. ipython::

	In [1]: squares = []
	   ...: for x in range(10):
	   ...:     squares.append(x**2)
	   ...: print(squares)
	   ...: 
	[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

As always, Python has a more elegant solution with the same result::

	>>> squares = [x**2 for x in range(10)]

List comprehensions can include more ``for`` statements and even ``if`` statements::

	>>> [(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
	[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]

which creates a list of pairs with distinct elements. Equivalenly, one could write this over several lines:

.. ipython::

	In [1]: combs = []
	   ...: for x in [1,2,3]:
	   ...:     for y in [3,1,4]:
	   ...:         if x != y:
	   ...:             combs.append((x, y))
	   ...: print(combs)

Below are a few more examples::

	>>> vec = [-4, -2, 0, 2, 4]
	>>> # create a new list with the values doubled
	>>> [x*2 for x in vec]
	[-8, -4, 0, 4, 8]
	>>> # filter the list to exclude negative numbers
	>>> [x for x in vec if x >= 0]
	[0, 2, 4]
	>>> # apply a function to all the elements
	>>> [abs(x) for x in vec]
	[4, 2, 0, 2, 4]
	>>> # call a method on each element
	>>> freshfruit = ['  banana', '  loganberry ', 'passion fruit  ']
	>>> [weapon.strip() for weapon in freshfruit]
	['banana', 'loganberry', 'passion fruit']
	>>> # create a list of 2-tuples like (number, square)
	>>> [(x, x**2) for x in range(6)]
	[(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]
	>>> # flatten a list using a listcomp with two 'for'
	>>> vec = [[1,2,3], [4,5,6], [7,8,9]]
	>>> [num for elem in vec for num in elem]
	[1, 2, 3, 4, 5, 6, 7, 8, 9]

Finally, we can transpose a "matrix" represented as a list of lists in the following several ways.

.. ipython::

	In [1]: matrix = [
	   ...:     [1, 2, 3, 4],
	   ...:     [5, 6, 7, 8],
	   ...:     [9, 10, 11, 12],
	   ...: ]

First, the longest but clearest:

.. ipython::

	In [1]: transposed = []
	   ...: for i in range(4):
	   ...:     transposed_row = []
	   ...:     for row in matrix:
	   ...:         transposed_row.append(row[i])
	   ...:     transposed.append(transposed_row)
	   ...: print(transposed)
	   ...: 
	[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]

Next uses one list comprehension:

.. ipython::

	In [1]: transposed = []
	   ...: for i in range(4):
	   ...:     transposed.append([row[i] for row in matrix])

Or, one single nested list comprehension::

	>>> [[row[i] for row in matrix] for i in range(4)]

And, finally, the most elegant (in the context of standard library) way::

	>>> list(zip(*matrix))
	[(1, 5, 9), (2, 6, 10), (3, 7, 11), (4, 8, 12)]
	

Functions
---------

.. todo:: Write **Functions** section

def, return, default values, keyword variables

Classes
-------

.. todo:: Write **Classes** section

def, methods, attributes, inheritance

Modules and Packages
--------------------

.. todo:: Write **Modules and Packages** section

import, ``__all__``, ``__main__``

Documenenting your code
-----------------------

.. todo:: Write **Documenenting your code** section

docstrings, numpydoc


.. _`Wakari.io`: https://www.wakari.io
.. _`Style Guide`: https://www.python.org/dev/peps/pep-0008/