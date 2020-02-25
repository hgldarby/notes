# Think Python Docs

## Variables, expressions and statements

- The type function below returns the type of the input provided, also called the **argument**. Examples

  ```python
  >>> type('Hello, World')
  <type, 'str'>
  >>> type(17)
  <type 'int'>
  ```

## Functions

- A function "takes" an argument and "returns" a result

- Conversion of types can be done using eg:

  ```python
  >>> int(-2.3)
  -2
  >>> float(32)
  32.0
  >>> str(3.14159)
  '3.14159'
  ```

- A **module** is a file that contains a collection of related functions

- Inside each function, arguments are assigned to variables called **parameters** eg:

  ```python
  def print_twice(bruce)
  	print(bruce)
      print(bruce)
  ```

- This assigns the argument to a parameter "bruce"
- When you create a variable inside a function, it becomes **local** which means it only exists inside that function.
- Functions can be used to remove repetitive code, therefore making the codebase smaller.

## Conditionals and recursion

- Modulus operator "%" yields the remainder when dividing

- A boolean expression, i.e. `5 == 5` is an expressions which returns either **True** or **False**

- "True" and "False" are both of type **bool**

- "==" is a **relational operator**

- **Logical operators** are "and", "or" and "not"

- **Conditional Statements** give the ability to check conditions and change the behaviour of the program accordingly, e.g.

  ```python
  >>> if x > 0:
      	print('x is positive')
  ```

- The boolean expression after if is called the **condition**

- `if` statements is **alternative execution** where there are two possibilities and the condition determines which is executed.

- In the case above an `if` statement is needed and an `else` statement is needed

- **Chained conditionals** contain situations which have more than one possibility.

- in this case an `if` statement is needed, a number of `elif` or "else if" statements are needed and an `else` statement is needed. e.g:

  ```python
  >>>if x < y:
  	print('x is less than y')
  >>>elif x > y:
  	print('x is greater than y')
  >>>else:
  	print('x and y are equal')
  ```

- One conditional can be written within another to create **Nested Conditionals**.

  An example of this could be:

  ```python
  >>>if x == y:
      print('x and y are equal')
  >>>else:
      if x < y:
          print('x is less than y')
  >>>else:
  print('x is greater than y')
  ```

- Recursive functions can be created which can either call another function or call themselves.
- Infinite Recursion is not a good idea as python will return an error message.

## Fruitful Functions

- Some functions generate values which we usually assign to a variable or use as part of an expression

- An example of a fruitful function is:

  ```python
  >>> def area(radius):
          temp = math.pi * radius**2
          return temp
  ```

- Temporary values such as "temp" above make debugging an easier task.

- The function above could also be written more concisely, this is demonstrated below:

  ```python
  >>> def area(radius):
      	return math.pi * radius**2
  ```

- When dealing with or creating increasingly complex problems, **Incremental Development** has a distinct advantage to full development.
- When undertaking **Incremental Development**, if issues arise within the process, debugging won't be such a long process as the pieces of code to debug will be shorter.
- Using this approach means that testing can also be an incremental process. 
- This means that more tests can be created and more confidence is built within that piece of code as we are assuring that each piece of code works as we expect it should.
- Calling a function within another function is called **Composition**
- **Boolean functions** return Booleans which can be useful for hiding complex tests within functions.
- The built-in function `isinstance` is used to check the type of an argument. For example if we say `n = 4` then a check we can do is `isinstance(n, int)` which will return a boolean depending on whether or not the argument is an integer.

## Iteration

- Equality is a symmetric relation but assignment is not. For example, in Python `a = 7` is allowed but `7 = a` is not.

- Most common form of multiple assignment is an **update** where the new value depends on the old, e.g `x = x + 1`

- Before you can update a variable you have to **initialise** it. This is usually done with a simple assignment. For example:

  ```python
  >>> x = 0
  >>> x = x + 1
  ```

- Updating a variable by adding 1 is called an **increment**, subtracting 1 is called a **decrement**.

- The **while** statement can be used like so:

  ```python
  def countdown(n):
      while n > 0:
          print n
          n = n-1
      print 'Blastoff!'
  ```

- You can read this as though it was English. It reads, "while n is greater than 0, display the value of n, then reduce the value by 1. When n = 0, display the word Blastoff!".

- More formally, here is the flow execution:

  - 1. Evaluate the condition, yielding `True` or `False`
    2. If the condition is false, exit the `while` statement and continue execution at the next statement
    3. If the condition is true, execute the body and then go back to step 1.

- This type of flow is called a **loop** because the third step loops back around to the top.

- Sometimes you don’t know it’s time to end a loop until you get half way through the body. In that case you can use the `break` statement to jump out of the loop.

- An example of this is shown here:

  ```python
  while True:
      line = raw_input('> ')
      if line == 'done':
          break
      print(line)
  print('Done!')
  ```

- An **algorithm** is a mechanical process for solving a category of problems.

## Strings

- A string is a sequence of characters.

- Characters can be accessed one at a time with the bracket operator e.g.

  ```python
  >>> fruit = 'banana'
  >>> letter = fruit[1]
  ```

- The expression, "1", inside the brackets is called the **index**

- If you try to print `letter` you would get `a`. This is because in computer science, the index is an offset from the beginning of the string. The first letters index is actually `0`.

- Performing `letter = fruit[0]` gives `letter = b`.

- `len` is a built in function that returns the number of characters in a string.

  ```python
  >>> fruit = 'banana'
  >>> length = len(fruit)
  ```

  In this case `length = 6`.

- To get the last letter in the string you would have to perform:

  ```python
  >>> last = fruit[length - 1]
  ```

  Alternatively you can use:

  ```python
  >>> last = fruit[-1]
  ```

  which returns the last letter. With `-2` it will return the second to last etc.

- **Traversal** of a string with a for loop can be done as such:

  ```python
  >>> for char in fruit:
      	print(char)
  ```

  This says, for each character in 'banana' print the character.

- A segment of a string is called a **Slice**. Selecting a slice is similar to selecting a character. Use the [n:m] operator to select a slice

  e.g.

  ```python
  >>> fruit = 'banana'
  >>> fruit[1:3]
  'an'
  >>> fruit[:3]
  'ban'
  >>> fruit[3:]
  'ana'
  >>> fruit[3:3]
  ''
  ```

  If you omit the first index 'n' from [n:m], the slice starts from the beginning of the string. 

  If you omit the last index 'm' from [n:m], the slice ends at the end of the string.

  making n and m the same returns an empty string apart from [:] which returns the whole string.

- Strings are an **immutable** datatype. This means you cannot change the existing string.

- String **methods** exist and return a value. For example, the method `upper` takes the string and returns a new string with all uppercase letters.

- The word **in** is a boolean operator that takes two strings and returns True if the first appears as a substring in the second.

  e.g.

  ```python
  >>> 'a' in 'banana'
  True
  ```

- Relational operations can be used in strings, e.g. `==`, `>`, `<` etc

- Uppercase letters come before lowercase letters so:

  ```python
  >>> 'Pineapple' < 'banana'
  ```

  Is correct.

## Lists

- A **list** is a sequence of values of any kind.

- Lists are **mutable** meaning the existing list can be changed.

  e.g.

  ```python
  >>> numbers = [17, 123]
  >>> numbers[1] = 5
  >>> print numbers
  [17, 5]
  ```

- Traversing a list can be done in the same way as strings, e.g.:

  ```python
  >>> L = [1,2,3,4]
  >>> for item in L:
      	print(item)
  ```

- To update the elements or write new ones you need the indices. A common way to do this is shown below:

  ```python
  for i in range(len(numbers)):
  	numbers[i] = numbers[i] * 2
  ```

- Using `+` on lists concatenates them, e.g:

  ```python
  >>> a = [1, 2, 3]
  >>> b = [4, 5, 6]
  >>> c = a + b
  >>> print(c)
  [1, 2, 3, 4, 5, 6]
  ```

- The `*` operator repeats the list a given number of times, e.g:

  ```python
  >>> [0] * 4
  [0, 0, 0, 0]
  ```

- Slices works in the same way for lists as it does for strings. Refer to the strings section if needed to refresh the memory.

- List method **append** adds a new element to the end of a list

  ```python
  >>> t = ['a', 'b', 'c']
  >>> t.append('d')
  >>> print(t)
  ['a', 'b', 'c', 'd']
  ```

- **extend** takes a list as an argument and appends all of the elements

  ```python
  >>> t1 = ['a', 'b', 'c']
  >>> t2 = ['d', 'e']
  >>> t1.extend(t2)
  >>> print(t1)
  ['a', 'b', 'c', 'd', 'e']
  ```

  This leaves t2 unmodified.

- **sort** arranges the elements of the list from low to high

  ```python
  >>> t = ['d', 'c', 'e', 'b', 'a']
  >>> t.sort()
  >>> print(t)
  ['a', 'b', 'c', 'd', 'e']
  ```

- Adding up numbers in a list can be done using accumulation i.e.

  ```python
  total += x
  total = total + x
  ```

  These both do the same thing.

- You can also use **sum** and give the list as an argument.

- Deleting an element can be done using **pop** method:

  ```python
  >>> t = ['a', 'b', 'c']
  >>> x = t.pop(1)
  >>> print(t)
  ['a', 'c']
  >>> print(x)
  b
  ```

  This method modifies the list and returns the element that was removed.

- Using the **del** operator just deletes the element and doesn't return it.

- Removing more than one element can be done using the del operator with a slice index

  ```python
  >>> t = ['a', 'b', 'c', 'd', 'e', 'f']
  >>> del(t[1:5])
  >>> print(t)
  ['a', 'f']
  ```

- Converting string to a list of characters can be done like this:

  ```python
  >>> s = 'spam'
  >>> t = list(s)
  >>> print(t)
  ['s', 'p', 'a', 'm']
  ```

- Splitting by word as apposed to character can be done using **split**

  ```python
  >>> s = 'pining for the fjords'
  >>> t = s.split()
  >>> print(t)
  ['pining', 'for', 'the', 'fjords']
  ```

- **join** is the inverse of split

  ```python
  >>> t = ['pining', 'for', 'the', 'fjords']
  >>> delimiter = ' '
  >>> delimiter.join(t)
  'pining for the fjords'
  ```

- If we execute

  ```python
  a = 'banana'
  b = 'banana'
  ```

  We know `a` and `b` refer to strings but we don't know if it is the same string.

- to check `a` and `b` refer to the same string we can use the **is** operator

  ```python
  >>> a = 'banana'
  >>> b = 'banana'
  >>> a is b
  True
  ```

  When creating two lists however,

  ```python
  >>> a = [1, 2, 3]
  >>> b = [1, 2, 3]
  >>> a is b
  False
  ```

- in this second case the lists are **equivalent** as they have the same elements but not **identical** as they are not the same object
- If two objects are identical, they are also equivalent, but if they are equivalent, they are not necessarily identical.

- An example of a **reference** is shown below

  ```python
  >>> a = [1, 2, 3]
  >>> b = a
  >>> b is a
  True
  ```

  as both `a` and `b` refer to the same object

- An object with more than one reference is said to be **aliased**
- If the object is mutable, a change made with one alias affects the other.
- Best practice is to avoid aliasing when working with mutable objects.

## Dictionaries

- A dictionary is effectively a mapping between a set of indices which are called **keys** and **values**.

- Each key maps to a value

- The association of a key and value is called a **key-value pair** or sometimes an **item**.

  ```python
  >>> eng2sp = dict()
  >>> print(eng2sp)
  {}
  ```

- To add an item to the dictionary perform the following operation

  ```python
  >>> eng2sp['one'] = 'uno'
  ```

  This means that eng2sp is now

  ```python
  >>> print(eng2sp)
  {'one': 'uno'}
  ```

- The output format is also an input format. We can create a new dictionary like such

  ```python
  >>> eng2sp = {'one': 'uno', 'two': 'dos', 'three': 'tres'}
  ```

- Printing eng2sp returns the dictionary but the order may be different as the order of a dictionary is unpredictable.

- The elements in a dictionary are never indexed with integer indices. Instead keys are used to look up the corresponding values.

  ```python
  >>> print(eng2sp['two'])
  'dos'
  ```

- If the key isn't in the dictionary you get a KeyError exception.

- Using `len` on a dictionary returns the number of key-value pairs.

  ```python
  >>> len(eng2sp)
  3
  ```

- The `in` operator also works. It tells you whether something appears as a key in the dictionary.
- To determine if a value is in the dictionary we first use the `values` method followed by the `in` operator.
- The `in` operator uses a search algorithm for lists and the longer the list is, the longer the search time.
- For dictionaries, Python uses **hashtables** which means that no matter how many items are in the dictionary, the `in` operation takes about the same amount of time.

- A **hash** is a function that takes a value (of any kind) and returns an integer (hash value).
- Dictionaries use these hash values to store and lookup key-value pairs
- As lists and dictionaries are mutable, they cannot be used as keys but can be used as values.

- **Global** variables exist in the special frame `__main__`

- Unlike local variables which disappear when the function ends, global variables persist from one function call to the next.

- To use within a function you have to **declare** the global variable, e.g:

  ```python
  been_called = False
  
  def example2():
  	global been_called
  	been_called = True
  ```

- The line `global been_called` says that in this function I want to use the global variable, don't create one.

## Tuples

- Tuples are immutable.

- To create a tuple use one of the following commands:

  ```python
  >>> t = (1,2,3,4)
  >>> t1 = tuple()
  ```

- If the argument of the second command is a sequence (string, list or tuple), the result will be a tuple with the elements of the sequence, e.g:

  ```python
  >>> t = tuple('lupins')
  >>> print(t)
  ('l', 'u', 'p', 'i', 'n', 's')
  ```

- Most list operators work on tuples

- The slice operator selects a range of elements

- A tuple cannot be modified but you can replace one tuple with another

- `divmod` a built in function takes two arguments and returns a tuple of two values, the quotient and remainder. These can be stored as a tuple:

  ```python
  >>> t = divmod(7, 3)
  >>> print(t)
  (2, 1)
  ```

- **Tuple assignment** can also be used as such:

  ```python
  >>> quot, rem = divmod(7, 3)
  >>> print(quot)
  2
  >>> print(rem)
  1
  ```

- A parameter name that begins with * **gathers** arguments into a tuple, e.g create function printall

  ```python
  def printall(*args):
  	print(args)
  ```

  Use `printall` and pass three arguments and the result is shown below:

  ```python
  >>> printall(1, 2.0, '3')
  (1, 2.0, '3')
  ```

- The compliment of gather is **scatter**. An example of why this is useful is shown.

  ```python
  >>> t = (7, 3)
  >>> divmod(t)
  TypeError: divmod expected 2 arguments, got 1
  ```

  The above breaks because the tuple is taken as one argument

  ```python
  >>> divmod(*t)
  (2, 1)
  ```

  This works as the tuple is scattered into two arguments.

- `zip` is a built in function that takes two or more sequences and "zips" them together into a list of tuples where each tuple contains one element from each sequence. For example:

  ```python
  >>> s = 'abc'
  >>> t = [0, 1, 2]
  >>> zip(s, t)
  [('a', 0), ('b', 1), ('c', 2)]
  ```

- If you need to traverse the elements of a sequence and their indices, use `enumerate` e.g:

  ```python
  for index, element in enumerate('abc'):
  	print(index, element)
  ```

- Dictionaries have a method called `items` which returns a list of tuples, where each tuple is a key-value pair. For example:

  ```python
  >>> d = {'a':0, 'b':1, 'c':2}
  >>> t = d.items()
  >>> print(t)
  [('a', 0), ('c', 2), ('b', 1)]
  ```

- Going the other way, a list of tuples can be used to create a dictionary

  ```python
  >>> t = [('a', 0), ('c', 2), ('b', 1)]
  >>> d = dict(t)
  >>> print(d)
  {'a': 0, 'c': 2, 'b': 1}
  ```

- Using `zip` with `dict` allows us to do things such as this

  ```python
  >>> d = dict(zip('abc', range(3)))
  >>> print(d)
  {'a': 0, 'c': 2, 'b': 1}
  ```

- The dictionary method `update` takes a list of tuples and adds them as key-value pairs to an existing dictionary.

- Using `items` in a for loop can be done like so:

  ```python
  for key, value in d.items():
      print(key, value)
  ```

- Relational operators work with tuples and other sequences. It will start with the first element from each sequence. If they are both equal, it will move on until it finds elements that differ. For example:

  ```python
  >>> (0, 1, 2) < (0, 3, 4)
  True
  ```

## Files

- Some programs are **transient** which means they run for a short time, produce an output, but when they end the data disappears. Running the program again starts from a clean slate.
- Other programs are **persistent** meaning they run for a long time (or all the time); they keep at least some of their data in permanent storage and if they shut down and restart, they will pick up where they left off.
- A simple way for a program to maintain their data is by reading and writing text files.
- An alternative is to store the state of the program in a database.

#### Reading and Writing 

- A text file is a sequence of characters stored in a permanent medium such as a hard drive.

- Writing a file requires the use of `open()` with mode `w` as the second parameter. An example is shown below

  ```python
  >>> fout = open('output.txt', 'w')
  >>> print(fout)
  <open file 'output.txt', mode 'w' at 0xb7eb2410>
  ```

- If the file exists, opening it in write mode clears out the old data and starts fresh.

- The `write` method puts data into a file

  ```python
  >>> line1 = "This here's the wattle,\n"
  >>> fout.write(line1)
  ```

- The file object keeps track of where it is. Using write again would add new data to the end of what is there.

- When writing is finished you have to close the file 

  ```python
  >>> fout.close()
  ```

- The argument in `write` needs to be a string

- Files are organised into **directories**

- The `os` module provides functions for working with files and directories.

- `os.path.abspath` returns the **absolute path** to a file. This starts from the topmost directory in the file system.

  ```python
  >>> os.path.abspath('memo.txt')
  '/home/dinsdale/memo.txt'
  ```

- `os.path.exists` - checks if a file or directory exists
- `os.path.isdir` - checks if it is a directory
- `os.path.isfile` - checks if it is a file
- `os.path.listdir` - returns a list of the files and directories in the given directory

- Handling an exception with a `try`  and `except` statement is called **catching** and exception. An example is shown below

  ```python
  try:
      fin = open('bad_file')
      for line in fin:
      	print(line)
      fin.close()
  except:
      print 'Something went wrong.'
  ```

#### Databases

- A **database** is a file that is organised for storing data.
- Most databases are organised like a dictionary in the sense they map keys to values
- Databases are on disk, so it persists after the program ends.

#### Pickling

- The `pickle` module allows the translation of almost any type of object into a string suitable for storage in a database, and back from strings to objects.
- `pickle.dumps` - takes an object and returns a string representation
- `pickle.loads` - takes a string and returns the object that it represents

#### Pipes

- A **pipe** is an object that represents a running program

- An example, Unix command `1s -1` normally displays the contents of the current directory. You can launch `1s` with `os.popen`

  ```python
  >>> cmd = 'ls -l'
  >>> fp = os.popen(cmd)
  ```

#### Writing Modules

- Any file that contains Python code can be imported as a module

- An example

  ```python
  def linecount(filename):
      count = 0
      for line in open(filename):
          count += 1
  	return count
  print(linecount('wc.py'))
  ```

## Classes and Objects

- A user defined type is called a **class**.

- An example of a class to represents a point in 2-D space is shown below

  ```python
  class Point(object):
  	"""Represents a point in 2-D space."""
      self.x = None
      self.y = None
  ```

- This header indicates that the new class is a `Point`, which is a kind of `object`, which is a built-in type

- The body is a **docstring**, used to describe what the class is for

- As point is defined at the top level, its "full name" is `__main__.Point`

- The class object is like a factory for creating objects. To create a Point, you call Point as if it were a function.

  ```python
  >>> blank = Point()
  >>> print blank
  <__main__.Point instance at 0xb7e9d3ac>
  ```

- The return value is a reference to a Point object, which we assign to `blank`. 
- Creating a new object is called **instantiation**, and the object is an **instance** of the class.

#### Attributes

- Values can be assigned to an instance using dot notation:

  ```python
  >>> blank.x = 3.0
  >>> blank.y = 4.0
  ```

- These values are being assigned to named elements of an object. These are called **attributes**.

- The attributes values can be read using the same syntax.

  ```python
  >>> print(blank.y)
  4.0
  >>> x = blank.x
  >>> print(x)
  3.0
  ```

#### Rectangle

- Define a class to represent a rectangle

  ```python
  class Rectangle(object):
  	"""Represents a rectangle.
  	attributes: width, height, corner.
  	"""
      self.width = None
      self.height = None
      self.corner = None
  ```

- To represent the rectangle we must instantiate it

  ```python
  box = Rectangle()
  box.width = 100.0
  box.height = 200.0
  ```

  For the corner we can instantiate the Point class created earlier

  ```python
  box.corner = Point()
  box.corner.x = 0.0
  box.corner.y = 0.0
  ```

- Objects are Mutable

- For example, box width and height can be changed:

  ```python
  box.width = box.width + 50
  box.height = box.width + 100
  ```

- Functions can also be written to perform the same task.

#### Copying

- Copying an object is often an alternative to aliasing

- The `copy` module contains a function called `copy` that can duplicate any object. For example:

  ```python
  >>> p1 = Point()
  >>> p1.x = 3.0
  >>> p1.y = 4.0
  >>> import copy
  >>> p2 = copy.copy(p1)
  ```

- `p1` and `p2` contain the same data but are not the same Point object

  ```python
  >>> p1 is p2
  False
  >>> p1 == p2
  False
  ```

- The `==` operator, for instances, behaves the same as the `is` operator and checks object identity not equivalence 
- If you used `copy.copy` to duplicate the `Rectangle` class, it copies the Rectangle object but not the embedded Point

- Using `copy.deepcopy` means that the copy is a completely separate object to the original

## Classes and Functions

- Functions can be of two kinds in this situation, pure functions and modifiers

- A pure function is one which does not modify any of the objects passed to it as arguments and has no effect other than returning a value. For example:

  ```python
  def add_time(t1, t2):
      sum = Time()
      sum.hour = t1.hour + t2.hour
      sum.minute = t1.minute + t2.minute
      sum.second = t1.second + t2.second
      return sum
  ```

- Modifiers are functions that modify the objects it gets as parameters. For example:

  ```python
  def increment(time, seconds):
      time.second += seconds
      if time.second >= 60:
          time.second -= 60
          time.minute += 1
      if time.minute >= 60:
          time.minute -= 60
          time.hour += 1
  ```

- If `seconds` is much greater than sixty it may be best to replace the `if` statements with `while` statements. This would decrease efficiency though.

## Classes and Methods

- A **method** is a function that is associated with a particular class
- They are semantically the same as functions, but there are two syntactic differences:
  - Methods are defined inside a class definition in order to make the relationship between the class and the method explicit
  - The syntax for invoking a method is different to that of a function.
- By convention, the first parameter of a method is called `self`

#### The init method

- init is short for initialisation.

- This is a special method which gets invoked once an object is instantiated.

- An example of an `__init__` method is shown here:

  ```python
  Class Time(object)
  """Represents the time of day"""
  	def __init__(self, hour=0, minute=0, second=0):
          self.hour = hour
          self.minute = minute
          self.second = second
  ```

- It is common for the parameters of `__init__` to have the same names as the attributes.

- `self.hour = hour` stores the value of the parameter `hour` as an attribute of `self`

- As the class above is written, the default value of `hour`, `minute`, and `second` is `0`.

- Let's create a method of class `Time` called `print_time()` as below:

  ```python
  def print_time(time):
      print('{hour}:{minute}:{second}'.format(hour=time.hour, 	minute=time.minute, second=time.second))
  ```

- We can then instantiate class `Time` and call our `print_time()` method to return a time of the day. For example, instantiating `Time()` with no arguments, the default values are given:

  ```python
  >>> time = Time()
  >>> time.print_time()
  00:00:00
  ```

  If you give one argument, it will override `hour`:

  ```python
  >>> time = Time (9)
  >>> time.print_time()
  09:00:00
  ```

  Giving two will override `hour` and `minute`, and three will override `hour`, `minute`, and `second`:

  ```python
  >>> time = Time(9, 45, 12)
  >>> time.print_time()
  09:45:12
  ```

- Printing values from an object can be done easily using the `.format()` operation as seen above.

- An alternative is to add an `f` before the string starts, for example, rewriting the `print_time()` method can be done like so:

  ```python
  def print_time(time):
      print(f'{time.hour}:{time.minute}:{time.second}')
  ```

#### The `__str__` method:

- `__str__` is another special method like `__init__` which is supposed to return the string representation of an object.

- An example of this could be:

  ```python
  def __str__(self):
  	return f'{self.hour}:{self.minute}:{self.second}'
  ```

- When using `print` on an object, this calls the `__str__` method. For example:

  ```python
  >>> time = Time(9, 45)
  >>> print(time)
  09:45:00
  ```

#### Operator Overloading

- By defining other special methods, the behaviour of operators can be specified on user defined types.

- As an example, by defining a special method called `__add__`, you can use the `+` operator which will then call this method.

- Let's define this method inside the `Time` class:

  ```python
  def __add__(self, other):
      seconds = self.time_to_int() + other.time_to_int()
      return int_to_time(seconds)
  ```

- A usage of this method can be seen here:

  ```python
  >>> start = Time(9, 45)
  >>> duration = Time(1, 35)
  >>> print(start + duration)
  11:20:00
  ```

#### Type-based dispatch

- Previously, we only added two `Time` objects together but what if we want to add an integer and a `Time` object.

- Method `__add__` can be changed so that a type check is done on argument `other`. depending on the outcome, it will either invoke `add_time()` or `increment()`:

  ```python
  def __add__(self, other):
      if isinstance(other, Time):
      	return self.add_time(other)
      else:
      	return self.increment(other)
      
  def add_time(self, other):
      seconds = self.time_to_int() + other.time_to_int()
      return int_to_time(seconds)
  
  def increment(self, seconds):
      seconds += self.time_to_int()
      return int_to_time(seconds)
  ```

- `isinstance` is a built in function that takes a value and a class as parameters and returns `True` if the value is an instance of the class or `False` if it is not.

- If `other` is a `Time` object, `add_time` is invoked, otherwise `increment` is invoked. This is called a **type-based dispatch** as it dispatches the computation to different methods based on the type of the arguments

#### Polymorphism

- Functions that can work with several data types (i.e. string, int, float) are called **polymorphic**
- 

