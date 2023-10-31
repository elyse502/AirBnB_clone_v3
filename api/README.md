
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
