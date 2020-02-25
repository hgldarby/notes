# Logging in Python

- Can help develop a better understanding of the flow of a program
- Logs can store information like which user or IP accessed the app
- Can be easier to find where the error happened if there was one

### Logging module

- 5 levels indicating the severity of events where each has a corresponding method that can be used to log events. They are:
  
  - DEBUG
  - INFO
  - WARNING
  - ERROR
  - CRITICAL
  
- These can be called in the following way

  ```python
  import logging
  
  logging.debug('This is a debug message')
  logging.info('This is an info message')
  logging.warning('This is a warning message')
  logging.error('This is an error message')
  logging.critical('This is a critical message')
  ```

- The output is

  ```python
  WARNING:root:This is a warning message
  ERROR:root:This is an error message
  CRITICAL:root:This is a critical message
  ```

- The output shows the severity level before each message along with `root`, which is the name the logging module gives to its default logger

- The output can include things like timestamp, line number and other details in addition to the default level, name and message
- Debug and info messages aren't loaded as by default the logging module only logs messages with level warning or above; this can be changed.

### Basic Configurations

- Use `basicConfig(**kwargs)` to configure the logging

- Commonly used parameters are:

  - level: The root logger will be set to the specified severity level
  - filename: This specifies the file
  - filemode: If filename is given, the file is opened in this mode. The default is "a", which means append.
  - format: This is the format of the log message.

- Examples:

  EX1:

  ```python
  import logging
  
  logging.basicConfig(level=logging.DEBUG)
  logging.debug('This will get logged')
  ```

  Gives:

  ```python
  DEBUG:root:This will get logged
  ```

  EX2:

  ```python
  import logging
  
  logging.basicConfig(filename='app.log', filemode='w', format='%(name)s - %(levelname)s - %(message)s')
  logging.warning('This will get logged to a file')
  ```

  Gives:

  ```python
  root - ERROR - This will get logged to a file
  ```

- This latter examples message will be written to file named app.log rather than the console

- filemode is "w" which means log file is open in "write mode". each run of the program will rewrite the file

- Calling `basicConfig()` to configure the root logger only works if it has not been configured before.

### Capturing stack traces

- Can capture full stack traces in an app

- Captured if `exc_info` parameter is set to `True` and logging functions are called like this:

  ```python
  import logging
  
  a = 5
  b = 0
  
  try:
    c = a / b
  except Exception as e:
    logging.error("Exception occurred", exc_info=True)
  ```

  which gives:

  ```python
  ERROR:root:Exception occurred
  Traceback (most recent call last):
    File "exceptions.py", line 6, in <module>
      c = a / b
  ZeroDivisionError: division by zero
  [Finished in 0.2s]
  ```

- Logging from and exception handler you can use `logging.exception()` which is equivalent to calling `logging.error(exc_info=True)`

### Classes and Functions

- You should define your own logger by creating an object of the Logger class.
- Classes and functions in the module:
  - Logger - class whose objects will be used in the apps code directly to call the functions
  - LogRecord - Loggers auto create `LogRecord` objects that have all the info related to the event being logged
  - Handler - Send the `LogRecord` to the required output destination. A base for the subclasses like `StreamHandler, FileHandler` etc.
  - Formatter - where you specify the format of the output.

- Example of creating a logger:

  ```python
  import logging
  
  logger = logging.getLogger('example_logger')
  logger.warning('This is a warning')
  ```

  Gives:

  ```python
  This is a warning
  ```

- Unlike `root` logger, the name of the custom logger is not part of the default output and has to be added to the config.

### Handlers

- Necessary when you create your own logger and want to sent the logs to multiple places when they are generated.

- A logger can have more than one handler

- Example of adding two handlers to a new logger:

  ```python
  # logging_example.py
  
  import logging
  
  # Create a custom logger
  logger = logging.getLogger(__name__)
  
  # Create handlers
  c_handler = logging.StreamHandler()
  f_handler = logging.FileHandler('file.log')
  c_handler.setLevel(logging.WARNING)
  f_handler.setLevel(logging.ERROR)
  
  # Create formatters and add it to handlers
  c_format = logging.Formatter('%(name)s - %(levelname)s - %(message)s')
  f_format = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
  c_handler.setFormatter(c_format)
  f_handler.setFormatter(f_format)
  
  # Add handlers to the logger
  logger.addHandler(c_handler)
  logger.addHandler(f_handler)
  
  logger.warning('This is a warning')
  logger.error('This is an error')
  ```

  

