
# SQLAlchemy Mapping and Table Creation Lab

SQLAlchemy is a powerful Object Relational Mapper that lets us "map" our Python objects to a SQL database.  We can create Python classes that are represented by tables in our database.  Each new instance of a class gets "mapped" to a row on a table in our database.  As we are probably well aware by now, writing SQL inserts, updates, and queries can be repetitive and tedious.  SQLAlchemy has a library of built-in methods that handle these tasks in an efficient manner.  In this lab, we will use SQLAlchemy to create a new database and create a table.

## Objectives

1.  Understand that we can map Python classes to a SQL database
2.  Create and connect to a SQLite database using SQLAlchemy
3.  Create a table with several columns and different datatypes using SQLAlchemy

### Part 1: Setup

#### Create and connect to our database

We can create and establish a connection to our new database with sqlalchemy's `create_engine` function.  The first step is to import this function from the `sqlalchemy` library at the top of our `schema.py` file.  Then, we will use this function to create a database, in this case `musicians.db`, with the following line of code:

> ```engine = create_engine('sqlite:///musicians.db', echo=True)```

Technically, the database does not exist yet.  We will not create the musicians database until later on when we call the `engine` variable.  For now, let this line of code linger at the bottom of the `schema.py` file until we are ready to use it.

#### Declare a mapping

Next, we need our Python classes to have the functionality of the *declarative base class*.  The declarative base is responsible for cataloging our classes and tables.  We import the `declarative_base` from the sqlalchemy library at the top of our Python script with the other dependencies as so:

> ```from sqlalchemy.ext.declarative import declarative_base```

> ```Base = declarative_base()```

### Part 2: Create the schema

#### Construct the musicians table

Finally, with all this setup out of the way, we are ready to create a SQL table!  The `Musician` class will take the `Base` we declared above as an argument.  The table's name will be `'musicians'`, and it should have the following five columns with these respective datatypes:

> 1. id - integer
2. fullname - string
3. instrument - string
4. dob - datetime
5. alive - boolean

We will need to import `Column`, `Integer`, `String`, `DateTime`, and `Boolean` from the sqlalchemy at the top of the `schema.py` file.  By now, we are importing so much of the sqlalchemy library that it probably makes sense to simply import all.

> ```from sqlalchemy import *```

#### Execute the table creation

Remember that engine variable from the very beginning that we left at the bottom of the file?  Time to put it to use!  We will execute the creation of our database and the musicians table with the code below.  The declarative base's `metadata.create_all()` issues the SQL commands so that our database and table are up and running.

> ```Base.metadata.create_all(engine)```

## A Note on the Tests

Prior to running the tests, run the `python schema.py` in your terminal after you have finished writing all the code in the `schema.py` file.  Python will read and execute your code and create the `musicians.db` file.  The tests check this file's output.

If the tests don't pass, for now simply delete the `musicians.db` file then try again!
