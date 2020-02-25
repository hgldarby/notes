# Flask Tutorial

#### 	   Overview

- Flask - web application framework written in Python

- Web application framework - collection of libraries and modules that enables a web application developer to write applications without worrying about low-level details e.g. protocols etc

- Flask based on the Werkzeug **WSGI** toolkit and Jinja2 template engine

- **Web Server Gateway Interface (WSGI)** - spec for a universal interface between web server and web applications

- Werkzeug - WSGI toolkit implementing requests, response objects and other utility functions

- Jinga2 - templating engine for Python

  #### Virtualenv

- Virtualenv - virtual python environment builder

  ```python
pip install virtualenv
  mkdir newproj
  cd newproj
  virtualenv venv
  
  venv\scripts\activate
  
  pip install Flask
  ```
  
  
  
  #### Application
  
- The route function of flask **route()** - a decorator which tells the application which URL should call the associated function

- The run method of Flask **run()** - runs the application on the local development server

- **Host** - hostname to listen on. Defaults to 127.0.0.1 (localhost). Set to '0.0.0.0' to have server available externally

- **Port** - defaults to 5000

- **Debug** - defaults to false. If set to true, provides a debug information

- **Options** - To be forwarded to underlying Werkzeug server.

- Whilst the program is under development it's best to use Debug mode

  ```python
  app.debug = True
  app.run()
  app.run(debug=TRUE)
  ```

 - Web frameworks use routing to help user remember URLs.

   #### Variable rules

 - **route()** - decorator in Flask used to bind URL to a function

 - **add_url_rule()** - also available to bind a URL with a function 

 - **<variable>** is used as a keyword argument to the function with which the rule is associated.

   #### URL Rules

 - URL rules of Flask are based on Werkzeug's routing module - ensures URLs formed are unique

 - **url_for()** - is very useful for dynamically building a URL for a specific function. The function accepts the name of a function as first argument, and one or more keyword arguments, each corresponding to the variable part of URL.

   #### Http Methods

 - **Get** - Sends data in unencrypted form to the server

 - **Head** - Same as **Get**, but without response body

 - **Post** - Used to send HTML form data to server. Data received by post is not cached by server.

 - **Put** - Replaces all current representations of the target resource with uploaded content

 - **Delete** - Removes all current representations of the target resource given by a URL

   #### Templates

 - You can return the output of a function bound to a certain URL in HTML format

 - This is cumbersome especially when variable data and python language elements like conditionals or loops are needed.

 - Instead of returning hardcoded HTML, a HTML file can be rendered by the **render_template()** function.

 - **Web templating system** refers to designing a HTML script where the variable data can be entered dynamically.

   #### Static files

 - A web app often requires a static file i.e. javascript of CSS supporting the display of a web page. 

   #### Request object

 - Data from a clients webpage is sent as a global request object

 - To process the request data, it should be imported from the Flask module

 - Important attributes of request object are listed below:

   - **Form** − It is a dictionary object containing key and value pairs of form parameters and their values.

   - **args** − parsed contents of query string which is part of URL after question mark (?).

   - **Cookies** − dictionary object holding Cookie names and values.

   - **files** − data pertaining to uploaded file.

   - **method** − current request method.

  #### Sending Form Data to Template

- The **Form** data received by the triggered function can collect it in the form of a dictionary object and forward it to a template to render it on a corresponding web page.

  #### Cookies

- A cookie is stored on a clients computer in the form of a text file.

- Its purpose is to remember and track data pertaining to a client’s usage for better visitor experience and site statistics.

- A **Request object** contains a cookie’s attribute. It is a dictionary object of all the cookie variables and their corresponding values, a client has transmitted. In addition to it, a cookie also stores its expiry time, path and domain name of the site.

  #### Sessions

- Unlike a cookie, Session data is store on a server

- **Session** is the time interval when a client logs into a server and logs out of it

- The data, which is needed to be help across this session, is stored in a temporary directory on the server.

- A session with each client is assigned a **Session ID**

- Session data is stored on top of cookies

- The server signs them cryptographically

- For the encryption, Flask needs a defined **Secret_key**

  #### Redirect and Errors

- Flask has a redirect function **redirect()** - returns a response object and redirects user to another target location with specified status code.

- Takes three parameters:

  - **location** parameter is the URL where response should be redirected.

  - **statuscode** sent to browser’s header, defaults to 302.

  - **response** parameter is used to instantiate response.

- Flask class has **abort()** function with an error code

- Takes one parameter:

- The **Code** parameter takes one of following values −

  - **400** − for Bad Request
  - **401** − for Unauthenticated
  - **403** − for Forbidden
  - **404** − for Not Found
  - **406** − for Not Acceptable
  - **415** − for Unsupported Media Type
  - **429** − Too Many Requests
  
  #### Message Flashing
  
- Good Graphical User Interface (GUI) provides feedback to user about the interaction

- Flask contains method **flash()** - Passes a message to the next request which is generally a template.

- Takes two parameters:

  - **message** parameter is the actual message to be flashed.
  - **category** parameter is optional. It can be either ‘error’, ‘info’ or ‘warning’.
  
 - **get_flashed_messages()** - called to remove message from session

 - Can take two parameters - Both parameters are optional. The first parameter is a tuple if received messages are having category. The second parameter is useful to display only specific messages.

   #### File Uploading

 - File upload needs a HTML form with its enctype attribute set to 'multipart/form-data', posting the file to a URL.

 - URL handler fetches file from **request.files[]** and saves it to desired location.

 - Each uploaded file is saved in a temp location on server before being saved in its ultimate location.

 - Destination name can be hardcoded or obtained from filename property **request.files[file]** but it is recommended to obtain a secure version using **secure_filename()**.

 - **app.config[‘UPLOAD_FOLDER’]** - Defines path for upload folder

 - **app.config[‘MAX_CONTENT_PATH’]** - Specifies maximum size of file to be uploaded in bytes

   #### Extensions

 - Flask - often referred to as micro framework because a core functionality includes WSGI and routing based on **Werkzeug** and template engine based on **Jinja2**

 - Flask framework has support for cookie and sessions as well as web helpers like **JSON**, static files etc.

 - Flask extension - Python module, which adds a specific type of support to the Flask app.

 - Important Flask extensions:

   - **Flask Mail** − provides SMTP interface to Flask application

   - **Flask WTF** − adds rendering and validation of WTForms

   - **Flask SQLAlchemy** − adds SQLAlchemy support to Flask application

   - **Flask Sijax** − Interface for Sijax - Python/jQuery library that makes AJAX easy to use in web applications

   #### Flask Mail

- This extension makes it very easy to set up a simple interface with any email server.

- Needs configuring with following parameters:

   - **MAIL_SERVER** - Name/IP address of email server

   - **MAIL_PORT** - Port number of server used

   - **MAIL_USE_TLS** - Enable/disable Transport Security Layer encryption

   - **MAIL_USE_SSL** - Enable/disable Secure Sockets Layer encryption

   - **MAIL_DEBUG** - Debug support. Default is Flask application’s debug status

   - **MAIL_USERNAME** - User name of sender

   - **MAIL_PASSWORD** - password of sender

   - **MAIL_DEFAULT_SENDER** - sets default sender

   - **MAIL_MAX_EMAILS** - Sets maximum mails to be sent

   - **MAIL_SUPPRESS_SEND** - Sending suppressed if app.testing set to true

   - **MAIL_ASCII_ATTACHMENTS** - If set to true, attached filenames converted to ASCII

- Contains the following classes:

- **Mail Class** - Manages email messaging requirements

- Methods of Mail class:

   - **send()** - Sends contents of Message class object
   - **connect()** - opens connection with mail host
   - **send_message()** - Sends message object
   
- **Message Class** - Encapsulates an email message

- Methods of Message class:

   - **attach()** - adds an attachment to message. Takes following parameters:
     - **filename** - name of file to attach
     - **content_type** - Multipurpose Internet Mail Extensions (MIME) type of file
     - **data** - raw file data
     - **disposition** - content disposition, if any.
   - **add_recipient()** - adds another recipient to message
   
   #### WTF
   
- HTML provides <form> tag, used to design an interface

- Data entered by a user is submitted in the form of Http request message to the server side script by either GET or POST method.

   - The Server side script has to recreate the form elements from http request data. So in effect, form elements have to be defined twice – once in HTML and again in the server side script.
   - Another disadvantage of using HTML form is that it is difficult (if not impossible) to render the form elements dynamically. HTML itself provides no way to validate a user’s input.

- Flask WTF contains a **Forms** class which has to be used as a parent for user defined form.

- **WTForms** - flexible form, rendering and validation library

- Contains definitions of various form fields. Some standard fields are listed below:

   - **TextField** - Represents <input type = 'text'> HTML form element
   - **BooleanField** - Represents <input type = 'checkbox'> HTML form element
   - **DecimalField** - Textfield for displaying number with decimals
   - **IntegerField** - TextField for displaying integer
   - **RadioField** - Represents <input type = 'radio'> HTML form element
   - **SelectField** - Represents select form element
   - **TextAreaField** - Represents <testarea> html form element
   - **PasswordField** - Represents <input type = 'password'> HTML form element
   - **SubmitField** - Represents <input type = 'submit'> form element
   
- **WTForms** contains **validator** class which is useful in applying validation to form fields. Commonly used validators:

   - **DataRequired** - checks whether input field is empty
   - **Email** - Checks whether text in the field follows email ID conventions
   - **IPAddress** - Validates IP address in input field
   - **Length** - Verifies if length of string in input field is in given range
   - **NumberRange** - Validates a number in input field within given range
   - **URL** - Validates URL entered in input field
   
- The **validate()** function of form object validates the form data and throws the validation errors if validation fails

   #### SQLite

- Python has an in-built support for **SQlite**. 

- SQlite3 module is shipped with Python distribution

- **MultiDict** - a dictionary subclass customized to deal with multiple values for the same key which is for example used by the parsing functions in the wrappers

   #### SQLAlchemy

- Using raw SQL in FLask web apps to perform **CRUD** (Create, Read, Update, Delete) can be tedious

- Instead **SQLAlchemy** is a powerful **OR Mapper** that gives application developers the full power and flexibility of SQL

- **Object relation Mapping (ORM)** - a technique of mapping object parameters to the underlying **Relational Database Management System** table structure.

- An **ORM** API provides methods to perform **CRUD** operations without having to write raw SQL statements.

- The **Session** object of **SQLAlchemy** manages all persistence operations of **ORM** object.

- These **Session** methods perform **CRUD** operations:

   - **db.session.add**(model object) - inserts a record into mapped table
   - **db.session.delete**(model object) - deletes record from table
   - **model.query.all()** - retrieves all records from table (corresponding to SELECT query)
   
   #### Sijax
   
- **Sijax** - standing for **Simple Ajax** is a Python library designed to help bring Ajax to your app.

- Config:

   - **SIJAX_STATIC_PATH** − the static path where you want the Sijax javascript files to be mirrored. The default location is **static/js/sijax**. In this folder, **sijax.js** and **json2.js** files are kept.
   - **SIJAX_JSON_URI** − the URI to load the json2.js static file from
   
- **Sijax** uses **JSON** to pass the data between the browser and the server.

- Every **Sijax** handler receives at least one parameter automatically - **obj_response**

- **obj_response** - the functions way of talking back to the browser

   #### Deployment

- A Flask app on the Dev server is accessible only on the computer on which the dev environment is set up

- To switch from a dev environment to production an app needs to be deployed on a real web server

- For small apps, consider deploying on any of the following hosted platforms:

   - Heroku
   - Dotcloud
   - Webfaction
   
- **mod_wsgi** - Apache module that provides a **WSGI** compliant interface for hosting Python based web apps on Apache server.

- Many popular servers written in Python contain **WSGI** apps and serve 