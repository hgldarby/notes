# Pony ORM

- What is Pony - an advanced object relational mapper
- **ORM** - Object Relational Mapper which allows developers to work with the content of a database in the form of objects
- Pony ORM is a library for Python language that allows you to conveniently work with objects that are stored as rows in a relational database

#### Installing

- To install Pony use:

  ```python
  pip install pony
  ```

- When using SQLite you don't need to install anything else, but with other databases you need to have the corresponding database driver installed.

- To install just the orm package use:

  ```python
  >>> from pony install orm
  ```

#### Creating a Database object

- Entities in Pony are connected to a database

- To create a database use:

  ```python
  >>> db = Database()
  ```

#### Defining entities

- Defining entities is done as such:

  ```python
  >>> class Person(db.Entity):
  ...     name = Required(str)
  ...     age = Required(int)
  ...     cars = Set('Car')
  ...
  >>> class Car(db.Entity):
  ...     make = Required(str)
  ...     model = Required(str)
  ...     owner = Required(Person)
  ...
  >>>
  ```

- To check the entity definition in interactive mode, use:

  ```
  >>> show()
  class Person(Entity):
      id = PrimaryKey(int, auto=True)
      name = Required(str)
      age = Required(int)
      cars = Set(Car)
  ```

- An automatic key has been set since we did not previously set one, hence the id.

#### Database Binding

- Binding - attaches declared entities to a specific database

- Use method:

  ```
  >>> Database.bind()
  ```

- An example is shown below:

  ```python
  >>> db.bind(provider='sqlite', filename=':memory:')
  ```

- Currently Pony supports 4 database types: `'sqlite'`, `'mysql'`, `'postgresql'` and `'oracle'`
- If the database is created in-memory, it will be deleted once the interactive session in Python is over

- To work with a database stored as a file use:

  ```python
  >>> db.bind(provider='sqlite', filename='database.sqlite', create_db=True)
  
  ```

- In this case, if the database file does not exist, it will be created. In our example, we can use a database created in-memory.

- How to connect to the databases:

  ```python
  # SQLite
  db.bind(provider='sqlite', filename=':memory:')
  # or
  db.bind(provider='sqlite', filename='database.sqlite', create_db=True)
  
  # PostgreSQL
  db.bind(provider='postgres', user='', password='', host='', database='')
  
  # MySQL
  db.bind(provider='mysql', host='', user='', passwd='', db='')
  
  # Oracle
  db.bind(provider='oracle', user='', password='', dsn='')
  ```

#### Mapping Entities to Database Tables

- Use `generate_mapping()` to create database tables where we persist our data

  ```python
  >>> db.generate_mapping(create_tables=True)
  ```

#### Using the debug mode

- Use `set_sql_debug()` so you can see the SQL commands that pony sends to the database.

- To turn it on use:

  ```
  >>> set_sql_debug(True)
  ```

#### Creating entity instances

- This is achieved the same way we do it in python, by instantiating a class
- Must use `commit()` to save the objects to the database

#### db_session

- Code which interacts with the database needs to be within a database session

- Using Pony in an application, all database interactions need to be done within a database session

- To do that, wrap the functions with `db_session()` decorator as such:

  ```python
  @db_session
  def print_person_name(person_id):
      p = Person[person_id]
      print p.name
      # database session cache will be cleared automatically
      # database connection will be returned to the pool
  
  @db_session
  def add_car(person_id, make, model):
      Car(make=make, model=model, owner=Person[person_id])
      # commit() will be done automatically
      # database session cache will be cleared automatically
      # database connection will be returned to the pool
  ```

- This decorator performs the following actions on exiting functions:

  - Performs rollback of transaction if the function raises an exception
  - Commits transaction if data was changed and no exceptions occurred
  - Returns the database connection to the connection pool
  - Clears the database session cache

- Entity instances are valid only within the `db_session()`

- To render a HTML template using the objects, do it within `db_session()`

- Could use `db_session()` as the context manager instead of the decorator:

  ```python
  with db_session:
      p = Person(name='Kate', age=33)
      Car(make='Audi', model='R8', owner=p)
      # commit() will be done automatically
      # database session cache will be cleared automatically
      # database connection will be returned to the pool
  ```





