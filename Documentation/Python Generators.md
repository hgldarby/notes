# Python Generators

- Generator functions - Lazy iterator which can be looped over like a list but doesn't store its contents in memory

- Common use case - Data streams or large files (like CSV)

  Example:

  ```python
  def csv_reader(file_name):
      for row in open(file_name, "r"):
          yield row
  ```

  

- A way of minimising the usage of memory

- can use `next(gen)` where gen is a generator you manually iterate over. (can be useful for testing a generator) 

- Can use generator functions as well as generator expressions (similar to list expressions)

  Example:

  ```python
  csv_gen = (row for row in open(file_name))
  ```

- `yield` results in a generator object
- `return` results in the first line of the file only



- **yield** indicates where in the code the value is sent back to the caller
- You don't exit the function after a yield, instead the state of the function is remembered.

### Profiling Generator Performance

- If a list is smaller than the running machine's available memory, list comprehensions can be faster to evaluate than the equivalent generator expression.

### Understanding Yield statement

- Primary job - control the flow of a generator function
- Calling methods such as `next()` run the code within the function up to the next yield
- Once yield is hit, function is suspended and returns the yielded value to the caller.
- You can use multiple yield statements in a function

### Advanced Generator Methods

#### .send() method

- Used to send values into a generator that you have just yielded.

#### .throw() method

- Allows you to throw exceptions with the generator.
- Useful where you might want to catch an exception.

#### .close() method

- Allows you to stop a generator
- Useful when controlling an infinite sequence generator

### Creating Data Pipelines With Generators

- Data pipelines allow you to string together code to process large datasets or streams without maxing out the machines memory.

