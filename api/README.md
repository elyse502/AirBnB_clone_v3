<img src="https://github.com/jarehec/AirBnB_clone_v3/blob/master/dev/HBTN-hbnb-Final.png" width="160" height=auto />

# AirBnB Clone: Phase # 3

: API with Swagger

## Description

Project attempts to clone the the AirBnB application and website, including the
database, storage, RESTful API, Web Framework, and Front End.  Currently the
application is designed to run with 2 storage engine models:

* File Storage Engine:

  * [`/models/engine/file_storage.py`](https://github.com/elyse502/AirBnB_clone_v3/blob/master/models/engine/file_storage.py)

* Database Storage Engine:

  * [`/models/engine/db_storage.py`](https://github.com/elyse502/AirBnB_clone_v3/blob/master/models/engine/db_storage.py)

  * To Setup the DataBase for testing and development, there are 2 setup
  scripts that setup a database with certain privileges: `setup_mysql_test.sql`
  & `setup_mysql_test.sql` (for more on setup, see below).

  * The Database uses Environmental Variables for tests.  To execute tests with
  the environmental variables prepend these declarations to the execution
  command:

```groovy
$ HBNB_MYSQL_USER=hbnb_test HBNB_MYSQL_PWD=hbnb_test_pwd \
HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_test_db HBNB_TYPE_STORAGE=db \
[COMMAND HERE]
```

![02078cd7f0573885c85a225c7436584a5afea1f9](https://github.com/elyse502/AirBnB_clone_v3/assets/125453474/d366a221-7c71-42cd-9af3-546556058cfa)

# Concepts
_For this project, we expect you to look at these concepts:_
* [REST API](https://intranet.alxswe.com/concepts/45)
* [AirBnB clone](https://intranet.alxswe.com/concepts/74)

# 1. REST API
REST API is a software architectural style for Backend.

**REST = “REpresentational State Transfer”. API = Application Programming Interface**

Its purpose is to induce performance, scalability, simplicity, modifiability, visibility, portability, and reliability.

REST API is **Resource-based**, a resource is an object and can be access by a URI. An object is “displayed”/transferred via a **representation** (typically JSON). HTTP methods will be actions on a resource.

Example:
* Resource: `Person` (John)
* Service: contact information (`GET`)
* Representation:
  * `first_name`, `last_name`, `date_of_birth`
  * JSON format

## There are 6 constraints:
## 1. Uniform Interface
* Define the interface between client-server
* Simple and can be split in small parts

#### HTTP verbs
* `GET`:
  * Read representation of a resource or a list of resources
* `POST`:
  * Create a new resource
* `PUT`:
  * Update an existing resource
* `DELETE`:
  * Remove an existing resource

#### URIs - resource name
A resource representation is accessible by a URI:
* `GET /users`: path for listing all user resources
* `GET /users/12`: path for the user `id = 12`
* `GET /users/12/addresses`: path for listing all addresses of the user `id = 12`
* `POST /users`: path for creating a user resource
* `PUT /users/12`: path for updating the user `id = 12`
* `DELETE /users/12/addresses/2`: path for deleting the address `id = 2` of the user `id = 12`

### HTTP Response
In the HTTP Response, the client should verify the information of two things:
* status code: result of the action
* body: JSON or XML representation of resources

Some important status code:
* `200`: OK
* `201`: created => after a `POST` request
* `204`: no content => can be return after a `DELETE` request
* `400`: bad request => the server doesn’t understand the request
* `401`: unauthorized => client user can’t be identified
* `403`: forbidden => client user is identified but not allowed to access a resource
* `404`: not found => resource doesn’t exist
* `500`: internal server error

## 2. Stateless
The server is independent of the client. The server doesn’t store user client information/state. Each request contains enough context to process it (HTTP Headers, etc.)

Some authentication systems like OAuth have to store information on the server side but they do it with REST API design.

## 3. Cacheable
All server responses (resource representation) are cacheable:
* Explicit
* Implicit
* Negotiated

Caches are here to improve performances. In a REST API, clients don’t care about the caching strategy, if the resource representation comes from a cache or from a database…

## 4. Client-Server
REST API is designed to separate Client from the Server. The server doesn’t know who is talking to it. Clients are not concerned with data storage => the portability of client code is improved. Servers are not concerned with the user interface or user state so that servers can be simpler and more scalable

## 5. Layered System
Client can’t assume direct connection to server. Intermediary servers may improve system scalability by enabling load-balancing and by providing shared caches. Layers may also enforce security policies.

## 6. Code on Demand (optional)
Server can temporarily:
* Transfer logic to client
* Allow client to execute logic
* Example: JavaScript

# 2. AirBnB clone

![65f4a1dd9c51265f49d0](https://github.com/elyse502/AirBnB_clone/assets/125453474/acf08a8b-f4e4-47b6-b32e-25d73c434b32)

I know you were waiting for it: it’s here!

The AirBnB clone project starts now until… the end of the first year. The goal of the project is to deploy on your server a simple copy of the [AirBnB website](https://www.airbnb.com/).

You won’t implement all the features, only some of them to cover all fundamental concepts of the higher level programming track.

After 4 months, you will have a complete web application composed by:
* A command interpreter to manipulate data without a visual interface, like in a Shell (perfect for development and debugging)
* A website (the front-end) that shows the final product to everybody: static and dynamic
* A database or files that store data (data = objects)
* An API that provides a communication interface between the front-end and your data (retrieve, create, delete, update them)

## Final product

![fe2e3e7701dec72ce612472dab9bb55fe0e9f6d4](https://github.com/elyse502/AirBnB_clone/assets/125453474/25b2713a-ff3d-496e-ac61-c82173a11825)


![da2584da58f1d99a72f0a4d8d22c1e485468f941](https://github.com/elyse502/AirBnB_clone/assets/125453474/1841b787-c8af-49b4-9c5e-dab0a5633846)

## Concepts to learn
* [Unittest](https://docs.python.org/3.4/library/unittest.html#module-unittest) - and please work all together on tests cases
* **Python packages** concept page
* Serialization/Deserialization
* `*args, **kwargs`
* `datetime`
* More coming soon!

## Steps
You won’t build this application all at once, but step by step.

Each step will link to a concept:

## The console
* create your data model
* manage (create, update, destroy, etc) objects via a console / command interpreter
* store and persist objects to a file (JSON file)

The first piece is to manipulate a powerful storage system. This storage engine will give us an abstraction between “My object” and “How they are stored and persisted”. This means: from your console code (the command interpreter itself) and from the front-end and RestAPI you will build later, you won’t have to pay attention (take care) of how your objects are stored.

This abstraction will also allow you to change the type of storage easily without updating all of your codebase.

The console will be a tool to validate this storage engine

![815046647d23428a14ca](https://github.com/elyse502/AirBnB_clone/assets/125453474/10c12086-2708-4322-b6b4-a3df7a66123b)

## Web static
* learn HTML/CSS
* create the HTML of your application
* create template of each object

![87c01524ada6080f40fc](https://github.com/elyse502/AirBnB_clone/assets/125453474/704ad78d-053c-4c30-bedc-3d87b19ebc69)

## MySQL storage
* replace the file storage by a Database storage
* map your models to a table in database by using an O.R.M.

![5284383714459fa68841](https://github.com/elyse502/AirBnB_clone/assets/125453474/f492838c-4d2a-4a75-8324-cc903634c361)

## Web framework - templating
* create your first web server in Python
* make your static HTML file dynamic by using objects stored in a file or database

![cb778ec8a13acecb53ef](https://github.com/elyse502/AirBnB_clone/assets/125453474/e801f00d-ced0-42ce-9bfc-acd1c2273f3e)

## RESTful API
* expose all your objects stored via a JSON web interface
* manipulate your objects via a RESTful API

![06fccc41df40ab8f9d49](https://github.com/elyse502/AirBnB_clone/assets/125453474/d0515e05-f4b0-44a7-bbbc-f7ad7ecc159f)

## Web dynamic
* learn JQuery
* load objects from the client side by using your own RESTful API

![d2d06462824fab5846f3](https://github.com/elyse502/AirBnB_clone/assets/125453474/50a350bb-2492-4701-a198-ef284721d971)

## Files and Directories
* `models` directory will contain all classes used for the entire project. A class, called “model” in a OOP project is the representation of an object/instance.
* `tests` directory will contain all unit tests.
* `console.py` file is the entry point of our command interpreter.
* `models/base_model.py` file is the base class of all our models. It contains common elements:
    * attributes: `id`, `created_at` and `updated_at`
    * methods: `save()` and `to_json()`
* `models/engine` directory will contain all storage classes (using the same prototype). For the moment you will have only one: `file_storage.py`.

## Storage
Persistency is really important for a web application. It means: every time your program is executed, it starts with all objects previously created from another execution. Without persistency, all the work done in a previous execution won’t be saved and will be gone.

In this project, you will manipulate 2 types of storage: file and database. For the moment, you will focus on file.

Why separate “storage management” from “model”? It’s to make your models modular and independent. With this architecture, you can easily replace your storage system without re-coding everything everywhere.

You will always use class attributes for any object. Why not instance attributes? For 3 reasons:
* Provide easy class description: everybody will be able to see quickly what a model should contain (which attributes, etc…)
* Provide default value of any attribute
* In the future, provide the same model behavior for file storage or database storage

## How can I store my instances?
That’s a good question. So let’s take a look at this code:
```groovy
class Student():
    def __init__(self, name):
        self.name = name

students = []
s = Student("John")
students.append(s)
```
Here, I’m creating a student and store it in a list. But after this program execution, my Student instance doesn’t exist anymore.
```groovy
class Student():
    def __init__(self, name):
        self.name = name

students = reload() # recreate the list of Student objects from a file
s = Student("John")
students.append(s)
save(students) # save all Student objects to a file
```
Nice!

But how it works?

First, let’s look at `save(students)`:
* Can I write each `Student` object to a file => _NO_, it will be the memory representation of the object. For another program execution, this memory representation can’t be reloaded.
* Can I write each `Student.name` to a file => _YES_, but imagine you have other attributes to describe `Student`? It would start to be become too complex.

The best solution is to convert this list of `Student` objects to a JSON representation.

Why JSON? Because it’s a standard representation of object. It allows us to share this data with other developers, be human readable, but mainly to be understood by another language/program.

Example:
* My Python program creates `Student` objects and saves them to a JSON file
* Another Javascript program can read this JSON file and manipulate its own `Student` class/representation

And the `reload()`? now you know the file is a JSON file representing all `Student` objects. So `reload()` has to read the file, parse the JSON string, and re-create `Student` objects based on this data-structure.

## File storage == JSON serialization
For this first step, you have to write in a file all your objects/instances created/updated in your command interpreter and restore them when you start it. You can’t store and restore a Python instance of a class as “Bytes”, the only way is to convert it to a serializable data structure:
* convert an instance to Python built in serializable data structure (list, dict, number and string) - for us it will be the method `my_instance.to_json()` to retrieve a dictionary
* convert this data structure to a string (JSON format, but it can be YAML, XML, CSV…) - for us it will be a `my_string = JSON.dumps(my_dict)`
* write this string to a file on disk

And the process of deserialization?

The same but in the other way:
* read a string from a file on disk
* convert this string to a data structure. This string is a JSON representation, so it’s easy to convert - for us it will be a `my_dict = JSON.loads(my_string)`
* convert this data structure to instance - for us it will be a `my_instance = MyObject(my_dict)`

### `*args, **kwargs`

#### [`How To Use them`](https://www.digitalocean.com/community/tutorials/how-to-use-args-and-kwargs-in-python-3)
How do you pass arguments to a function?
```groovy
def my_fct(param_1, param_2):
    ...

my_fct("Best", "School")
```
But with this function definition, you must call `my_fct` with 2 parameters, no more, no less.

Can it be dynamic? Yes you can:
```groovy
def my_fct(*args, **kwargs):
    ...

my_fct("Best", "School")
```
What? What’s `*args` and `**kwargs`?
* `*args` is a Tuple that contains all arguments
* `*kwargs` is a dictionary that contains all arguments by key/value

A dictionary? But why?

So, to make it clear, `*args` is the list of anonymous arguments, no name, just an order. `**kwargs` is the dictionary with all named arguments.

Examples:
```groovy
def my_fct(*args, **kwargs):
    print("{} - {}".format(args, kwargs))

my_fct() # () - {}
my_fct("Best") # ('Best',) - {}
my_fct("Best", 89) # ('Best', 89) - {}
my_fct(name="Best") # () - {'name': 'Best'}
my_fct(name="Best", number=89) # () - {'name': 'Best', 'number': 89}
my_fct("School", 12, name="Best", number=89) # ('School', 12) - {'name': 'Best', 'number': 89}
```
Perfect? Of course you can mix both, but the order should be first all anonymous arguments, and after named arguments.

Last example:
```groovy
def my_fct(*args, **kwargs):
    print("{} - {}".format(args, kwargs))

a_dict = { 'name': "Best", 'age': 89 }

my_fct(a_dict) # ({'age': 89, 'name': 'Best'},) - {}
my_fct(*a_dict) # ('age', 'name') - {}
my_fct(**a_dict) # () - {'age': 89, 'name': 'Best'}
```
You can play with these 2 arguments to clearly understand where and how your variables are stored.

### `datetime`
`datetime` is a Python module to manipulate date, time etc…

In this example, you create an instance of `datetime` with the current date and time:
```groovy
from datetime import datetime

date_now = datetime.now()
print(type(date_now)) # <class 'datetime.datetime'>
print(date_now) # 2017-06-08 20:42:42.170922
```
`date_now` is an object, so you can manipulate it:
```groovy
from datetime import timedelta

date_tomorrow = date_now + timedelta(days=1)
print(date_tomorrow) # 2017-06-09 20:42:42.170922
```
… you can also store it:
```groovy
a_dict = { 'my_date': date_now }
print(type(a_dict['my_date'])) # <class 'datetime.datetime'>
print(a_dict) # {'my_date': datetime.datetime(2017, 6, 8, 20, 42, 42, 170922)}
```
What? What’s this format when a `datetime` instance is in a datastructure??? It’s unreadable.

How to make it readable: [`strftime`](https://strftime.org/)
```groovy
print(date_now.strftime("%A")) # Thursday
print(date_now.strftime("%A %d %B %Y at %H:%M:%S")) # Thursday 08 June 2017 at 20:42:42
```
## Data diagram

![99e1a8f2be8c09d5ce5ac321e8cf39f0917f8db5](https://github.com/elyse502/AirBnB_clone/assets/125453474/3d7ad352-6e69-479b-be7c-96e850e0cb2c)

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif"><br><br>

# Resources🏗️
### Read or watch:
* **REST API** concept page
* [Learn REST: A RESTful Tutorial](https://www.restapitutorial.com/)
* [Designing a RESTful API with Python and Flask](https://blog.miguelgrinberg.com/post/designing-a-restful-api-with-python-and-flask)
* [HTTP access control (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
* [Flask cheatsheet](https://s3.amazonaws.com/intranet-projects-files/holbertonschool-higher-level_programming+/301/flask_cheatsheet.pdf)
* [What are Flask Blueprints, exactly?](https://stackoverflow.com/questions/24420857/what-are-flask-blueprints-exactly)
* [Flask](https://palletsprojects.com/p/flask/)
* [Modular Applications with Blueprints](https://flask.palletsprojects.com/en/1.1.x/blueprints/)
* [Flask tests](https://flask.palletsprojects.com/en/1.1.x/testing/)
* [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/)

# General🧵
* What REST means
* What API means
* What CORS means
* What is an API
* What is a REST API
* What are other type of APIs
* Which is the HTTP method to retrieve resource(s)
* Which is the HTTP method to create a resource
* Which is the HTTP method to update resource
* Which is the HTTP method to delete resource
* How to request REST API

# Requirements
## Python Scripts
* Allowed editors: `vi`, `vim`, `emacs`
* All your files will be interpreted/compiled on Ubuntu 20.04 LTS using `python3` (version 3.4.3)
* All your files should end with a new line
* The first line of all your files should be exactly #!/usr/bin/python3
* A `README.md` file, at the root of the folder of the project, is mandatory
* Your code should use the `PEP 8` style (version 1.7)
* All your files must be executable
* The length of your files will be tested using `wc`
* All your modules should have documentation (`python3 -c 'print(__import__("my_module").__doc__)'`)
* All your classes should have documentation (`python3 -c 'print(__import__("my_module").MyClass.__doc__)'`)
* All your functions (inside and outside a class) should have documentation (`python3 -c 'print(__import__("my_module").my_function.__doc__)'` and `python3 -c` `'print(__import__("my_module").MyClass.my_function.__doc__)'`)
* A documentation is not a simple word, it’s a real sentence explaining what’s the purpose of the module, class or method (the length of it will be verified)

## Python Unit Tests
* Allowed editors: `vi`, `vim`, `emacs`
* All your files should end with a new line
* All your test files should be inside a folder `tests`
* You have to use the [unittest module](https://docs.python.org/3.4/library/unittest.html#module-unittest)
* All your test files should be python files (extension: `.py`)
* All your test files and folders should start by `test_`
* Your file organization in the tests folder should be the same as your project: ex: for `models/base_model.py`, unit tests must be in: `tests/test_models/test_base_model.py`
* All your tests should be executed by using this command: `python3 -m unittest discover tests`
* You can also test file by file by using this command: `python3 -m unittest tests/test_models/test_base_model.py`
* We strongly encourage you to work together on test cases, so that you don’t miss any edge cases

# More Info

![02078cd7f0573885c85a225c7436584a5afea1f9](https://github.com/elyse502/AirBnB_clone_v3/assets/125453474/c7589798-74a0-4d0b-be06-44f17d2ec0ea)

# Install Flask
```groovy
$ pip3 install Flask
```

# Tasks 📃
## 0. Restart from scratch!: [AirBnB_clone_v3](https://github.com/elyse502/AirBnB_clone_v3)
No no no! We are already too far in the project to restart everything.

But once again, let’s work on a new codebase.

For this project you will fork this [codebase](https://github.com/alexaorrico/AirBnB_clone_v2):
* Update the repository name to `AirBnB_clone_v3`
* Update the `README.md`:
  * Add yourself as an author of the project
  * Add new information about your new contribution
  * Make it better!
* If you’re the owner of this codebase, create a new repository called `AirBnB_clone_v3` and copy over all files from `AirBnB_clone_v2`

## 1. Never fail!: [AirBnB_clone_v3](https://github.com/elyse502/AirBnB_clone_v3)

![95fedfc947ba610185a59b99b25811acb1bbe360](https://github.com/elyse502/AirBnB_clone_v3/assets/125453474/363b4bea-dc50-4d8a-9234-e4ecfb70104b)

Since the beginning we’ve been using the `unittest` module, but do you know why `unittests` are so important? Because when you add a new feature, you refactor a piece of code, etc… you want to be sure you didn’t break anything.

At Holberton, we have a lot of tests, and they all pass! Just for the Intranet itself, there are:
* `5,213` assertions (_as of 08/20/2018_)
* `13,061` assertions (_as of 01/25/2021_)

The following requirements **must** be met for your project:
* all current tests must pass (don’t delete them…)
* add new tests as much as you can (tests are mandatory for some tasks)
```groovy
guillaume@ubuntu:~/AirBnB_v3$ python3 -m unittest discover tests 2>&1 | tail -1
OK
guillaume@ubuntu:~/AirBnB_v3$ HBNB_ENV=test HBNB_MYSQL_USER=hbnb_test HBNB_MYSQL_PWD=hbnb_test_pwd HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_test_db HBNB_TYPE_STORAGE=db python3 -m unittest discover tests 2>&1 /dev/null | tail -n 1
OK
guillaume@ubuntu:~/AirBnB_v3$
```

## 2. Improve storage: [models/engine/db_storage.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/models/engine/db_storage.py), [models/engine/file_storage.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/models/engine/file_storage.py), [tests/test_models/test_engine/test_db_storage.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/tests/test_models/test_engine/test_db_storage.py), [tests/test_models/test_engine/test_file_storage.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/tests/test_models/test_engine/test_file_storage.py)
Update `DBStorage` and `FileStorage`, adding two new methods. **All changes should be done in the branch** `storage_get_count`:

A method to retrieve one object:
* Prototype: `def get(self, cls, id):`
  * `cls`: class
  * `id`: string representing the object ID
* Returns the object based on the class and its ID, or `None` if not found

A method to count the number of objects in storage:
* Prototype: `def count(self, cls=None):`
  * `cls`: class (optional)
* Returns the number of objects in storage matching the given class. If no class is passed, returns the count of all objects in storage.

Don’t forget to add new tests for these 2 methods on each storage engine.
```groovy
guillaume@ubuntu:~/AirBnB_v3$ cat test_get_count.py
#!/usr/bin/python3
""" Test .get() and .count() methods
"""
from models import storage
from models.state import State

print("All objects: {}".format(storage.count()))
print("State objects: {}".format(storage.count(State)))

first_state_id = list(storage.all(State).values())[0].id
print("First state: {}".format(storage.get(State, first_state_id)))

guillaume@ubuntu:~/AirBnB_v3$
guillaume@ubuntu:~/AirBnB_v3$ HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db HBNB_TYPE_STORAGE=db ./test_get_count.py 
All objects: 1013
State objects: 27
First state: [State] (f8d21261-3e79-4f5c-829a-99d7452cd73c) {'name': 'Colorado', 'updated_at': datetime.datetime(2017, 3, 25, 2, 17, 6), 'created_at': datetime.datetime(2017, 3, 25, 2, 17, 6), '_sa_instance_state': <sqlalchemy.orm.state.InstanceState object at 0x7fc0103a8e80>, 'id': 'f8d21261-3e79-4f5c-829a-99d7452cd73c'}
guillaume@ubuntu:~/AirBnB_v3$
guillaume@ubuntu:~/AirBnB_v3$ ./test_get_count.py 
All objects: 19
State objects: 5
First state: [State] (af14c85b-172f-4474-8a30-d4ec21f9795e) {'updated_at': datetime.datetime(2017, 4, 13, 17, 10, 22, 378824), 'name': 'Arizona', 'id': 'af14c85b-172f-4474-8a30-d4ec21f9795e', 'created_at': datetime.datetime(2017, 4, 13, 17, 10, 22, 378763)}
guillaume@ubuntu:~/AirBnB_v3$
```
For this task, you **must** make a pull request on GitHub.com, and ask at least one of your peer to review and merge it.

## 3. Status of your API: [api/__init__.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/__init__.py), [api/v1/__init__.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/__init__.py), [api/v1/views/__init__.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/__init__.py), [api/v1/views/index.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/index.py), [api/v1/app.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/app.py)
It’s time to start your API!

Your first endpoint (route) will be to return the status of your API:
```groovy
guillaume@ubuntu:~/AirBnB_v3$ HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db HBNB_TYPE_STORAGE=db HBNB_API_HOST=0.0.0.0 HBNB_API_PORT=5000 python3 -m api.v1.app
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
...
```
In another terminal:
```groovy
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/status
{
  "status": "OK"
}
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET -s http://0.0.0.0:5000/api/v1/status -vvv 2>&1 | grep Content-Type
< Content-Type: application/json
guillaume@ubuntu:~/AirBnB_v3$
``` 
Magic right? (No need to have a pretty rendered output, it’s a JSON, only the structure is important)

Ok, let starts:
* Create a folder `api` at the root of the project with an empty file `__init__.py`
* Create a folder `v1` inside `api`:
  * create an empty file `__init__.py`
  * create a file `app.py`:
    * create a variable `app`, instance of `Flask`
    * import `storage` from `models`
    * import `app_views` from `api.v1.views`
    * register the blueprint `app_views` to your Flask instance `app`
    * declare a method to handle `@app.teardown_appcontext` that calls `storage.close()`
    * inside `if __name__ == "__main__":`, run your Flask server (variable `app`) with:
      * host = environment variable `HBNB_API_HOST` or `0.0.0.0` if not defined
      * port = environment variable `HBNB_API_PORT` or `5000` if not defined
      * `threaded=True`
* Create a folder `views` inside `v1`:
  * create a file `__init__.py`:
    * import `Blueprint` from `flask` [doc](https://flask.palletsprojects.com/en/1.1.x/blueprints/)
    * create a variable `app_views` which is an instance of `Blueprint` (url prefix must be `/api/v1`)
    * wildcard import of everything in the package `api.v1.views.index` => PEP8 will complain about it, don’t worry, it’s normal and this file (`v1/views/__init__.py`) won’t be check.
  * create a file `index.py`
    * import `app_views` from `api.v1.views`
    * create a route `/status` on the object `app_views` that returns a JSON: `"status": "OK"` (see example)

## 4. Some stats?: [api/v1/views/index.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/index.py)
Create an endpoint that retrieves the number of each objects by type:
* In api/v1/views/index.py
* Route: /api/v1/stats
* You must use the newly added count() method from storage
```groovy
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/stats
{
  "amenities": 47, 
  "cities": 36, 
  "places": 154, 
  "reviews": 718, 
  "states": 27, 
  "users": 31
}
guillaume@ubuntu:~/AirBnB_v3$
```
_(No need to have a pretty rendered output, it’s a JSON, only the structure is important)_

## 5. Not found: [api/v1/app.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/app.py)
Designers are really creative when they have to design a “404 page”, a “Not found”… [34 brilliantly designed 404 error pages](https://www.creativebloq.com/web-design/best-404-pages-812505)

Today it’s different, because you won’t use HTML and CSS, but JSON!

In `api/v1/app.py`, create a handler for `404` errors that returns a JSON-formatted `404` status code response. The content should be: `"error": "Not found"`
```groovy
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/nop
{
  "error": "Not found"
}
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/nop -vvv
*   Trying 0.0.0.0...
* TCP_NODELAY set
* Connected to 0.0.0.0 (127.0.0.1) port 5000 (#0)
> GET /api/v1/nop HTTP/1.1
> Host: 0.0.0.0:5000
> User-Agent: curl/7.51.0
> Accept: */*
> 
* HTTP 1.0, assume close after body
< HTTP/1.0 404 NOT FOUND
< Content-Type: application/json
< Content-Length: 27
< Server: Werkzeug/0.12.1 Python/3.4.3
< Date: Fri, 14 Apr 2017 23:43:24 GMT
< 
{
  "error": "Not found"
}
guillaume@ubuntu:~/AirBnB_v3$
```

## 6. State: [api/v1/views/states.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/states.py), [api/v1/views/__init__.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/__init__.py)
Create a new view for `State` objects that handles all default RESTFul API actions:
* In the file `api/v1/views/states.py`
* You must use `to_dict()` to retrieve an object into a valid JSON
* Update `api/v1/views/__init__.py` to import this new file

Retrieves the list of all `State` objects: `GET /api/v1/states`

Retrieves a `State` object: `GET /api/v1/states/<state_id>`
* If the `state_id` is not linked to any `State` object, raise a `404` error

Deletes a `State` object:: `DELETE /api/v1/states/<state_id>`
* If the `state_id` is not linked to any `State` object, raise a `404` error
* Returns an empty dictionary with the status code `200`

Creates a `State`: `POST /api/v1/states`
* You must use `request.get_json` from Flask to transform the HTTP body request to a dictionary
* If the HTTP body request is not valid JSON, raise a `400` error with the message `Not a JSON`
* If the dictionary doesn’t contain the key `name`, raise a `400` error with the message `Missing name`
* Returns the new `State` with the status code `201`

Updates a `State` object: `PUT /api/v1/states/<state_id>`
* If the `state_id` is not linked to any `State` object, raise a `404` error
* You must use `request.get_json` from Flask to transform the HTTP body request to a dictionary
* If the HTTP body request is not valid JSON, raise a `400` error with the message `Not a JSON`
* Update the `State` object with all key-value pairs of the dictionary.
* Ignore keys: `id`, `created_at` and `updated_at`
* Returns the `State` object with the status code `200`
```groovy
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/states/
[
  {
    "__class__": "State", 
    "created_at": "2017-04-14T00:00:02", 
    "id": "8f165686-c98d-46d9-87d9-d6059ade2d99", 
    "name": "Louisiana", 
    "updated_at": "2017-04-14T00:00:02"
  }, 
  {
    "__class__": "State", 
    "created_at": "2017-04-14T16:21:42", 
    "id": "1a9c29c7-e39c-4840-b5f9-74310b34f269", 
    "name": "Arizona", 
    "updated_at": "2017-04-14T16:21:42"
  }, 
...
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/states/8f165686-c98d-46d9-87d9-d6059ade2d99
 {
  "__class__": "State", 
  "created_at": "2017-04-14T00:00:02", 
  "id": "8f165686-c98d-46d9-87d9-d6059ade2d99", 
  "name": "Louisiana", 
  "updated_at": "2017-04-14T00:00:02"
}
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X POST http://0.0.0.0:5000/api/v1/states/ -H "Content-Type: application/json" -d '{"name": "California"}' -vvv
*   Trying 0.0.0.0...
* TCP_NODELAY set
* Connected to 0.0.0.0 (127.0.0.1) port 5000 (#0)
> POST /api/v1/states/ HTTP/1.1
> Host: 0.0.0.0:5000
> User-Agent: curl/7.51.0
> Accept: */*
> Content-Type: application/json
> Content-Length: 22
> 
* upload completely sent off: 22 out of 22 bytes
* HTTP 1.0, assume close after body
< HTTP/1.0 201 CREATED
< Content-Type: application/json
< Content-Length: 195
< Server: Werkzeug/0.12.1 Python/3.4.3
< Date: Sat, 15 Apr 2017 01:30:27 GMT
< 
{
  "__class__": "State", 
  "created_at": "2017-04-15T01:30:27.557877", 
  "id": "feadaa73-9e4b-4514-905b-8253f36b46f6", 
  "name": "California", 
  "updated_at": "2017-04-15T01:30:27.558081"
}
* Curl_http_done: called premature == 0
* Closing connection 0
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X PUT http://0.0.0.0:5000/api/v1/states/feadaa73-9e4b-4514-905b-8253f36b46f6 -H "Content-Type: application/json" -d '{"name": "California is so cool"}'
{
  "__class__": "State", 
  "created_at": "2017-04-15T01:30:28", 
  "id": "feadaa73-9e4b-4514-905b-8253f36b46f6", 
  "name": "California is so cool", 
  "updated_at": "2017-04-15T01:51:08.044996"
}
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/states/feadaa73-9e4b-4514-905b-8253f36b46f6
{
  "__class__": "State", 
  "created_at": "2017-04-15T01:30:28", 
  "id": "feadaa73-9e4b-4514-905b-8253f36b46f6", 
  "name": "California is so cool", 
  "updated_at": "2017-04-15T01:51:08"
}
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X DELETE http://0.0.0.0:5000/api/v1/states/feadaa73-9e4b-4514-905b-8253f36b46f6
{}
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/states/feadaa73-9e4b-4514-905b-8253f36b46f6
{
  "error": "Not found"
}
guillaume@ubuntu:~/AirBnB_v3$
```

## 7. City: [api/v1/views/cities.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/cities.py), [api/v1/views/__init__.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/__init__.py)
Same as `State`, create a new view for `City` objects that handles all default RESTFul API actions:
* In the file `api/v1/views/cities.py`
* You must use `to_dict()` to serialize an object into valid JSON
* Update `api/v1/views/__init__.py` to import this new file

Retrieves the list of all `City` objects of a `State`: `GET /api/v1/states/<state_id>/cities`
* If the `state_id` is not linked to any `State object`, raise a `404` error

Retrieves a `City` object. : `GET /api/v1/cities/<city_id>`
* If the `city_id` is not linked to any `City` object, raise a `404` error

Deletes a `City` object: `DELETE /api/v1/cities/<city_id>`
* If the `city_id` is not linked to any `City` object, raise a `404` error
* Returns an empty dictionary with the status code `200`

Creates a `City`: `POST /api/v1/states/<state_id>/cities`
* You must use `request.get_json` from Flask to transform the HTTP body request to a dictionary
* If the `state_id` is not linked to any `State` object, raise a `404` error
* If the HTTP body request is not a valid JSON, raise a `400` error with the message `Not a JSON`
* If the dictionary doesn’t contain the key `name`, raise a `400` error with the message `Missing name`
* Returns the new `City` with the status code `201`

Updates a `City` object: `PUT /api/v1/cities/<city_id>`
* If the `city_id` is not linked to any `City` object, raise a `404` error
* You must use `request.get_json` from Flask to transform the HTTP body request to a dictionary
* If the HTTP request body is not valid JSON, raise a `400` error with the message `Not a JSON`
* Update the `City` object with all key-value pairs of the dictionary
* Ignore keys: `id`, `state_id`, `created_at` and `updated_at`
* Returns the `City` object with the status code `200`
```groovy
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/states/not_an_id/cities/
{
  "error": "Not found"
}
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/states/2b9a4627-8a9e-4f32-a752-9a84fa7f4efd/cities
[
  {
    "__class__": "City", 
    "created_at": "2017-03-25T02:17:06", 
    "id": "1da255c0-f023-4779-8134-2b1b40f87683", 
    "name": "New Orleans", 
    "state_id": "2b9a4627-8a9e-4f32-a752-9a84fa7f4efd", 
    "updated_at": "2017-03-25T02:17:06"
  }, 
  {
    "__class__": "City", 
    "created_at": "2017-03-25T02:17:06", 
    "id": "45903748-fa39-4cd0-8a0b-c62bfe471702", 
    "name": "Lafayette", 
    "state_id": "2b9a4627-8a9e-4f32-a752-9a84fa7f4efd", 
    "updated_at": "2017-03-25T02:17:06"
  }, 
  {
    "__class__": "City", 
    "created_at": "2017-03-25T02:17:06", 
    "id": "e4e40a6e-59ff-4b4f-ab72-d6d100201588", 
    "name": "Baton rouge", 
    "state_id": "2b9a4627-8a9e-4f32-a752-9a84fa7f4efd", 
    "updated_at": "2017-03-25T02:17:06"
  }
]
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/cities/1da255c0-f023-4779-8134-2b1b40f87683
{
  "__class__": "City", 
  "created_at": "2017-03-25T02:17:06", 
  "id": "1da255c0-f023-4779-8134-2b1b40f87683", 
  "name": "New Orleans", 
  "state_id": "2b9a4627-8a9e-4f32-a752-9a84fa7f4efd", 
  "updated_at": "2017-03-25T02:17:06"
}
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X POST http://0.0.0.0:5000/api/v1/states/2b9a4627-8a9e-4f32-a752-9a84fa7f4efd/cities -H "Content-Type: application/json" -d '{"name": "Alexandria"}' -vvv
*   Trying 0.0.0.0...
* TCP_NODELAY set
* Connected to 0.0.0.0 (127.0.0.1) port 5000 (#0)
> POST /api/v1/states/2b9a4627-8a9e-4f32-a752-9a84fa7f4efd/cities/ HTTP/1.1
> Host: 0.0.0.0:5000
> User-Agent: curl/7.51.0
> Accept: */*
> Content-Type: application/json
> Content-Length: 22
> 
* upload completely sent off: 22 out of 22 bytes
* HTTP 1.0, assume close after body
< HTTP/1.0 201 CREATED
< Content-Type: application/json
< Content-Length: 249
< Server: Werkzeug/0.12.1 Python/3.4.3
< Date: Sun, 16 Apr 2017 03:14:05 GMT
< 
{
  "__class__": "City", 
  "created_at": "2017-04-16T03:14:05.655490", 
  "id": "b75ae104-a8a3-475e-bf74-ab0a066ca2af", 
  "name": "Alexandria", 
  "state_id": "2b9a4627-8a9e-4f32-a752-9a84fa7f4efd", 
  "updated_at": "2017-04-16T03:14:05.655748"
}
* Curl_http_done: called premature == 0
* Closing connection 0
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X PUT http://0.0.0.0:5000/api/v1/cities/b75ae104-a8a3-475e-bf74-ab0a066ca2af -H "Content-Type: application/json" -d '{"name": "Bossier City"}'
{
  "__class__": "City", 
  "created_at": "2017-04-16T03:14:06", 
  "id": "b75ae104-a8a3-475e-bf74-ab0a066ca2af", 
  "name": "Bossier City", 
  "state_id": "2b9a4627-8a9e-4f32-a752-9a84fa7f4efd", 
  "updated_at": "2017-04-16T03:15:12.895894"
}
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/cities/b75ae104-a8a3-475e-bf74-ab0a066ca2af
{
  "__class__": "City", 
  "created_at": "2017-04-16T03:14:06", 
  "id": "b75ae104-a8a3-475e-bf74-ab0a066ca2af", 
  "name": "Bossier City", 
  "state_id": "2b9a4627-8a9e-4f32-a752-9a84fa7f4efd", 
  "updated_at": "2017-04-16T03:15:13"
}
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X DELETE http://0.0.0.0:5000/api/v1/cities/b75ae104-a8a3-475e-bf74-ab0a066ca2af
{}
guillaume@ubuntu:~/AirBnB_v3$ 
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/cities/b75ae104-a8a3-475e-bf74-ab0a066ca2af
{
  "error": "Not found"
}
guillaume@ubuntu:~/AirBnB_v3$
```

## 8. Amenity: [api/v1/views/amenities.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/amenities.py), [api/v1/views/__init__.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/__init__.py)
Create a new view for `Amenity` objects that handles all default RESTFul API actions:
* In the file `api/v1/views/amenities.py`
* You must use `to_dict()` to serialize an object into valid JSON
* Update `api/v1/views/__init__.py` to import this new file

Retrieves the list of all `Amenity` objects: `GET /api/v1/amenities`

Retrieves a `Amenity` object: `GET /api/v1/amenities/<amenity_id>`
* If the `amenity_id` is not linked to any `Amenity object`, raise a `404` error

Deletes a Amenity object:: `DELETE /api/v1/amenities/<amenity_id>`
* If the `amenity_id` is not linked to any `Amenity` object, raise a `404` error
* Returns an empty dictionary with the status code `200`

Creates a `Amenity`: `POST /api/v1/amenities`
* You must use `request.get_json` from Flask to transform the HTTP request to a dictionary
* If the HTTP request body is not valid JSON, raise a `400` error with the message `Not a JSON`
* If the dictionary doesn’t contain the key `name`, raise a `400` error with the message `Missing name`
* Returns the new `Amenity` with the status code `201`

Updates a `Amenity` object: `PUT /api/v1/amenities/<amenity_id>`
* If the `amenity_id` is not linked to any `Amenity` object, raise a `404` error
* You must use `request.get_json` from Flask to transform the HTTP request to a dictionary
* If the HTTP request body is not valid JSON, raise a `400` error with the message `Not a JSON`
* Update the `Amenity` object with all key-value pairs of the dictionary
* Ignore keys: `id`, `created_at` and `updated_at`
* Returns the `Amenity` object with the status code `200`

## 9. User: [api/v1/views/users.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/users.py), [api/v1/views/__init__.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/__init__.py)
Create a new view for `User` object that handles all default RESTFul API actions:
* In the file `api/v1/views/users.py`
* You must use `to_dict()` to retrieve an object into a valid JSON
* Update `api/v1/views/__init__.py` to import this new file

Retrieves the list of all `User` objects: `GET /api/v1/users`

Retrieves a `User` object: `GET /api/v1/users/<user_id>`
* If the `user_id` is not linked to any `User` object, raise a `404` error

Deletes a `User` object:: `DELETE /api/v1/users/<user_id>`
* If the `user_id` is not linked to any `User` object, raise a `404` error
* Returns an empty dictionary with the status code `200`

Creates a `User`: `POST /api/v1/users`
* You must use `request.get_json` from Flask to transform the HTTP body request to a dictionary
* If the HTTP body request is not valid JSON, raise a `400` error with the message `Not a JSON`
* If the dictionary doesn’t contain the key `email`, raise a `400` error with the message `Missing email`
* If the dictionary doesn’t contain the key `password`, raise a `400` error with the message `Missing password`
* Returns the new `User` with the status code `201`

Updates a `User` object: `PUT /api/v1/users/<user_id>`
* If the `user_id` is not linked to any `User` object, raise a `404` error
* You must use `request.get_json` from Flask to transform the HTTP body request to a dictionary
* If the HTTP body request is not valid JSON, raise a `400` error with the message `Not a JSON`
* Update the `User` object with all key-value pairs of the dictionary
* Ignore keys: `id`, `email`, `created_at` and `updated_at`
* Returns the `User` object with the status code `200`

## 10. Place: [api/v1/views/places.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/places.py), [api/v1/views/__init__.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/__init__.py)
Create a new view for `Place` objects that handles all default RESTFul API actions:
* In the file `api/v1/views/places.py`
* You must use `to_dict()` to retrieve an object into a valid JSON
* Update `api/v1/views/__init__.py` to import this new file

Retrieves the list of all `Place` objects of a `City`: `GET /api/v1/cities/<city_id>/places`
* If the `city_id` is not linked to any `City` object, raise a `404` error

Retrieves a `Place` object. : `GET /api/v1/places/<place_id>`
* If the `place_id` is not linked to any `Place` object, raise a `404` error

Deletes a `Place` object: `DELETE /api/v1/places/<place_id>`
* If the `place_id` is not linked to any `Place` object, raise a `404` error
* Returns an empty dictionary with the status code `200`

Creates a `Place`: `POST /api/v1/cities/<city_id>/places`
* You must use `request.get_json` from Flask to transform the HTTP request to a dictionary
* If the `city_id` is not linked to any `City` object, raise a `404` error
* If the HTTP request body is not valid JSON, raise a `400` error with the message `Not a JSON`
* If the dictionary doesn’t contain the key `user_id`, raise a `400` error with the message `Missing user_id`
* If the `user_id` is not linked to any `User` object, raise a `404` error
* If the dictionary doesn’t contain the key `name`, raise a `400` error with the message `Missing name`
* Returns the new `Place` with the status code `201`

Updates a `Place` object: `PUT /api/v1/places/<place_id>`
* If the `place_id` is not linked to any `Place` object, raise a `404` error
* You must use `request.get_json` from Flask to transform the HTTP request to a dictionary
* If the HTTP request body is not valid JSON, raise a `400` error with the message `Not a JSON`
* Update the `Place` object with all key-value pairs of the dictionary
* Ignore keys: `id`, `user_id`, `city_id`, `created_at` and `updated_at`
* Returns the `Place` object with the status code `200`

## 11. Reviews: [api/v1/views/places_reviews.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/places_reviews.py), [api/v1/views/__init__.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/__init__.py)
Create a new view for `Review` object that handles all default RESTFul API actions:
* In the file `api/v1/views/places_reviews.py`
* You must use `to_dict()` to retrieve an object into valid JSON
* Update `api/v1/views/__init__.py` to import this new file

Retrieves the list of all `Review` objects of a `Place`: `GET /api/v1/places/<place_id>/reviews`
* If the `place_id` is not linked to any `Place` object, raise a `404` error

Retrieves a `Review` object. : `GET /api/v1/reviews/<review_id>`
* If the `review_id` is not linked to any `Review` object, raise a `404` error

Deletes a `Review` object: `DELETE /api/v1/reviews/<review_id>`
* If the `review_id` is not linked to any `Review` object, raise a `404` error
* Returns an empty dictionary with the status code `200`

Creates a `Review`: `POST /api/v1/places/<place_id>/reviews`
* You must use `request.get_json` from Flask to transform the HTTP request to a dictionary
* If the `place_id` is not linked to any `Place` object, raise a `404` error
* If the HTTP body request is not valid JSON, raise a `400` error with the message `Not a JSON`
* If the dictionary doesn’t contain the key `user_id`, raise a `400` error with the message `Missing user_id`
* If the `user_id` is not linked to any `User` object, raise a `404` error
* If the dictionary doesn’t contain the key `text`, raise a `400` error with the message `Missing text`
* Returns the new `Review` with the status code `201`

Updates a `Review` object: `PUT /api/v1/reviews/<review_id>`
* If the `review_id` is not linked to any `Review` object, raise a `404` error
* You must use `request.get_json` from Flask to transform the HTTP request to a dictionary
* If the HTTP request body is not valid JSON, raise a `400` error with the message `Not a JSON`
* Update the `Review` object with all key-value pairs of the dictionary
* Ignore keys: `id`, `user_id`, `place_id`, `created_at` and `updated_at`
* Returns the `Review` object with the status code `200`

## 12. HTTP access control (CORS): [api/v1/app.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/app.py)
A resource makes a cross-origin HTTP request when it requests a resource from a different domain, or port, than the one the first resource itself serves.

Read the full definition [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

Why do we need this?

Because you will soon start allowing a web client to make requests your API. If your API doesn’t have a correct CORS setup, your web client won’t be able to access your data.

With Flask, it’s really easy, you will use the class `CORS` of the module `flask_cors`.

How to install it: `$ pip3 install flask_cors`

Update `api/v1/app.py` to create a `CORS` instance allowing: `/*` for `0.0.0.0`

You will update it later when you will deploy your API to production.

Now you can see this HTTP Response Header: `< Access-Control-Allow-Origin: 0.0.0.0`
```groovy
guillaume@ubuntu:~/AirBnB_v3$ curl -X GET http://0.0.0.0:5000/api/v1/cities/1da255c0-f023-4779-8134-2b1b40f87683 -vvv
*   Trying 0.0.0.0...
* TCP_NODELAY set
* Connected to 0.0.0.0 (127.0.0.1) port 5000 (#0)
> GET /api/v1/states/2b9a4627-8a9e-4f32-a752-9a84fa7f4efd/cities/1da255c0-f023-4779-8134-2b1b40f87683 HTTP/1.1
> Host: 0.0.0.0:5000
> User-Agent: curl/7.51.0
> Accept: */*
> 
* HTTP 1.0, assume close after body
< HTTP/1.0 200 OK
< Content-Type: application/json
< Access-Control-Allow-Origin: 0.0.0.0
< Content-Length: 236
< Server: Werkzeug/0.12.1 Python/3.4.3
< Date: Sun, 16 Apr 2017 04:20:13 GMT
< 
{
  "__class__": "City", 
  "created_at": "2017-03-25T02:17:06", 
  "id": "1da255c0-f023-4779-8134-2b1b40f87683", 
  "name": "New Orleans", 
  "state_id": "2b9a4627-8a9e-4f32-a752-9a84fa7f4efd", 
  "updated_at": "2017-03-25T02:17:06"
}
* Curl_http_done: called premature == 0
* Closing connection 0
guillaume@ubuntu:~/AirBnB_v3$
```

## 13. Place - Amenity: [api/v1/views/places_amenities.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/places_amenities.py), [api/v1/views/__init__.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/api/v1/views/__init__.py)
Create a new view for the link between `Place` objects and `Amenity` objects that handles all default RESTFul API actions:
* In the file `api/v1/views/places_amenities.py`
* You must use `to_dict()` to retrieve an object into a valid JSON
* Update `api/v1/views/__init__.py` to import this new file
* Depending of the storage:
  * `DBStorage`: list, create and delete `Amenity` objects from `amenities` relationship
  * `FileStorage`: list, add and remove `Amenity` ID in the list `amenity_ids` of a `Place` object

Retrieves the list of all `Amenity` objects of a `Place`: `GET /api/v1/places/<place_id>/amenities`
* If the `place_id` is not linked to any `Place` object, raise a `404` error

Deletes a `Amenity` object to a `Place`: `DELETE /api/v1/places/<place_id>/amenities/<amenity_id>`
* If the `place_id` is not linked to any `Place` object, raise a `404` error
* If the `amenity_id` is not linked to any `Amenity` object, raise a `404` error
* If the `Amenity` is not linked to the `Place` before the request, raise a `404` error
* Returns an empty dictionary with the status code `200`

Link a `Amenity` object to a `Place`: `POST /api/v1/places/<place_id>/amenities/<amenity_id>`
* No HTTP body needed
* If the `place_id` is not linked to any `Place` object, raise a `404` error
* If the `amenity_id` is not linked to any `Amenity` object, raise a `404` error
* If the `Amenity` is already linked to the `Place`, return the `Amenity` with the status code `200`
* Returns the `Amenity` with the status code `201`

## 14. Security improvements!: [models/base_model.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/models/base_model.py), [models/user.py](https://github.com/elyse502/AirBnB_clone_v3/blob/master/models/user.py)
Currently, the `User` object is designed to store the user password in cleartext.

It’s super bad!

To avoid that, improve the `User` object:
* Update the method `to_dict()` of `BaseModel` to remove the `password` key **except when it’s used** by **`FileStorage`** **to save data to disk**. Tips: default parameters
* Each time a new `User` object is created or password updated, the password is hashed to a [MD5](https://docs.python.org/3.4/library/hashlib.html) value
* In the database for `DBStorage`, the password stored is now hashed to a MD5 value
* In the file for `FileStorage`, the password stored is now hashed to a MD5 value






































































