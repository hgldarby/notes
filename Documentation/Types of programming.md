# Types of programming

###       Procedure-oriented programming

- Where we design our program around functions i.e. blocks of statements which manipulate data.

  ### Object-oriented programming 

- Where we combine data and functionality and wrap it inside something called an object. These use classes and objects. Classes create a new type where objects are instances of the class. Another way to describe it, you can have variables of type int which is like saying, variables that store integers are variables which are instances (objects) of the int class.

- Fields - variables that belong to an object or class are referred to as fields

- Methods - objects can have functionality using functions that belong to a class, these are called methods

- The fields and methods can be referred to as the attributes of that class.

- Inheritance - This can be best imagined as implementing a **type** and **subtype** relationship between classes. You can have a class "Schoolmember" and have subclasses "Student" and "Teacher" which inherit characteristics from the super class

- 

- Polymorphism - where a subtype can be substituted in any situation where a parent type is expected.

# Data Structures

Data Structures are a means to store a collection of related data. Python has four different data structures listed below. A note prior to starting, Strings are immutable.

- List [a, b] - Mutable data structure. You can add remove or search for items within the list
- Tuple (a, b) - Immutable data structure like strings. Usually used in cases where a statement or user-defined function can safely assume the collection of values won't change.
- Dictionary {k: v} - Keys (k) must be immutable objects like strings. Values can either be immutable or mutable objects. 
- Set set() - An unordered collection of simple objects. Used when the existence of an object in a collection is more important that then the order or how many times it occurs.