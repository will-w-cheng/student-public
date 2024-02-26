---

---

## What is a Database?

To begin, let's clarify what a database is and go over the most popular ones for different applications. 

A database which most of you should know is just a place to store data. Some popular databses for diffrent types of programs include . . .

### 1. SQL (Structured Query Language) Databases:

A type of relational database that uses a structured query language for defining and manipulating data. Examples include:

- **MySQL:** A widely used open-source relational database management system.
- **PostgreSQL:** Known for its extensibility and support for advanced data types.

### 2. Databases for Application Development:

In application development, NoSQL databases are often favored for their flexibility and scalability. Examples include:

- **MongoDB:** A document-oriented NoSQL database, ideal for handling JSON-like documents.
- **Cassandra:** A distributed NoSQL database designed for handling large amounts of data across commodity servers.

### 3. Databases for Web Development:

Web development often involves databases that can efficiently manage dynamic content and user interactions. Two popular choices are:

- **Firebase:** A cloud-based platform that includes a real-time NoSQL database, suitable for building web and mobile applications.
- **SQLite:** A lightweight, embedded relational database often used in web development due to its simplicity and portability.

These databases cater to various needs in the development landscape, providing developers with options based on the specific requirements of their projects. Whether it's relational databases for structured data or NoSQL databases for flexibility, the choice of a database depends on factors such as data structure, scalability, and the nature of the application being developed.



```python
-- code

-- MySQL

CREATE TABLE users (
  id INT PRIMARY KEY,
  username VARCHAR(50),
  email VARCHAR(100)
);

-- post sql

CREATE TABLE products (
  product_id SERIAL PRIMARY KEY,
  product_name VARCHAR(100),
  price DECIMAL
);

-- Biggest diffrence is postsql supports more and is more intensive

```


```python
// MongoDb

db.users.insert({
    username: "john_doe",
    email: "john.doe@example.com"
  });

```


```python
-- cql

CREATE TABLE user_profiles (
    user_id UUID PRIMARY KEY,
    first_name TEXT,
    last_name TEXT,
    email TEXT
  );


-- Cassandra Query Language (CQL) is a query language designed for Apache Cassandra, 
-- a highly scalable and distributed NoSQL database. Unlike SQL, which is relational, 
-- CQL is specifically tailored for managing and querying non-relational, decentralized data storage in Cassandra.
```


```python
// Firebase

const ref = firebase.database().ref('users');
ref.on('value', (snapshot) => {
  console.log(snapshot.val());
});

```

## For this Lesson we will be covering SQL and User Logins.

IF You want to follow along in your own flask feel free to code along otherwise its more than ok to just listen and ask questions.

PS: To code along a SQL DB link or file is needed


```python

from flask import Flask
from flask_sqlalchemy import SQLAlchemy

# Setup of key Flask object (app)
app = Flask(__name__)
# Setup SQLAlchemy object and properties for the database (db)
database = 'sqlite:///sqlite.db'  # path and filename of database
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False  # Configures Mods
app.config['SQLALCHEMY_DATABASE_URI'] = database  # Configurs the URI of the databse
app.config['SECRET_KEY'] = 'SECRET_KEY'  # Adds in a KEY, think of API keys
db = SQLAlchemy()  # Calls the function


# This belongs in place where it runs once per project
db.init_app(app)
```

## Explaining the Setup and Imports

To begin we always need to import what we are using. We start off with a basic flask setup and then add in the specalized SQL imports needed. 

Then the URI/file path is stored in database.

This is then called in the app.config.

Finnaly we call db=SQLAlechemy()  This is the key line needed to allow python interactions( makes your life easier)

### Now lets look into Models
No need to type all of this RN. 




```python
""" 
Database dependencies to support SQLite examples 
"""

import datetime
from datetime import datetime
import json

from sqlalchemy.exc import IntegrityError
from werkzeug.security import generate_password_hash, check_password_hash

''' 
Tutorial: https://www.sqlalchemy.org/library.html#tutorials, try to get into a Python shell and follow along 
'''

# Define the User class to manage actions in the 'users' table
# -- Object-Relational Mapping (ORM) is the key concept of SQLAlchemy
# -- a.) db.Model is like an inner layer of the onion in ORM
# -- b.) User represents data we want to store, something that is built on db.Model
# -- c.) SQLAlchemy ORM is layer on top of SQLAlchemy Core, then SQLAlchemy engine, SQL
class User(db.Model):
    __tablename__ = 'users'  # table name is plural, class name is singular

    # Define the User schema with "vars" from object
    id = db.Column(db.Integer, primary_key=True)
    _name = db.Column(db.String(255), unique=False, nullable=False)
    _uid = db.Column(db.String(255), unique=True, nullable=False)
    _password = db.Column(db.String(255), unique=False, nullable=False)
    _dob = db.Column(db.Date)

    # constructor of a User object, initializes the instance variables within object (self)
    def __init__(self, name, uid, password="123qwerty", dob=datetime.today()):
        self._name = name    # variables with self prefix become part of the object
        self._uid = uid
        self.set_password(password)
        if isinstance(dob, str):  # not a date type     
            dob = date=datetime.today()
        self._dob = dob

    # a name getter method, extracts name from object
    @property
    def name(self):
        return self._name
    
    # a setter function, allows name to be updated after initial object creation
    @name.setter
    def name(self, name):
        self._name = name
    
    # a getter method, extracts uid from object
    @property
    def uid(self):
        return self._uid
    
    # a setter function, allows uid to be updated after initial object creation
    @uid.setter
    def uid(self, uid):
        self._uid = uid
        
    # check if uid parameter matches user id in object, return boolean
    def is_uid(self, uid):
        return self._uid == uid
    
    @property
    def password(self):
        return self._password[0:10] + "..." # because of security only show 1st characters

    # update password, this is conventional method used for setter
    def set_password(self, password):
        """Create a hashed password."""
        self._password = generate_password_hash(password, method='sha256')

    # check password parameter against stored/encrypted password
    def is_password(self, password):
        """Check against hashed password."""
        result = check_password_hash(self._password, password)
        return result
    
    # dob property is returned as string, a string represents date outside object
    @property
    def dob(self):
        dob_string = self._dob.strftime('%m-%d-%Y')
        return dob_string
    
    # dob setter, verifies date type before it is set or default to today
    @dob.setter
    def dob(self, dob):
        if isinstance(dob, str):  # not a date type     
            dob = date=datetime.today()
        self._dob = dob
    
    # age is calculated field, age is returned according to date of birth
    @property
    def age(self):
        today = datetime.today()
        return today.year - self._dob.year - ((today.month, today.day) < (self._dob.month, self._dob.day))
    
    # output content using str(object) is in human-readable form
    # output content using json dumps, this is ready for API response
    def __str__(self):
        return json.dumps(self.read())

    # CRUD create/add a new record to the table
    # returns self or None on error
    def create(self):
        try:
            # creates a person object from User(db.Model) class, passes initializers
            db.session.add(self)  # add prepares to persist person object to Users table
            db.session.commit()  # SqlAlchemy "unit of work pattern" requires a manual commit
            return self
        except IntegrityError:
            db.session.remove()
            return None

    # CRUD read converts self to dictionary
    # returns dictionary
    def read(self):
        return {
            "id": self.id,
            "name": self.name,
            "uid": self.uid,
            "dob": self.dob,
            "age": self.age,
        }

    # CRUD update: updates user name, password, phone
    # returns self
    def update(self, name="", uid="", password=""):
        """only updates values with length"""
        if len(name) > 0:
            self.name = name
        if len(uid) > 0:
            self.uid = uid
        if len(password) > 0:
            self.set_password(password)
        db.session.add(self) # performs update when id exists
        db.session.commit()
        return self

    # CRUD delete: remove self
    # None
    def delete(self):
        db.session.delete(self)
        db.session.commit()
        return None

```

## Simplifying the Code

Imagine you have a cool app where users can sign up, log in, and do all sorts of fun stuff. Now, to keep track of these users and their information, we use something called a "model." Think of a model like a blueprint or a design for how we want to organize and store information about each user.

In our app, we have a special model called the "User" model. This model knows exactly what kind of information we want to store for each user, like their name, username, password, and even their date of birth. It's like a form we fill out for every user, and the User model helps us keep everything neat and organized.

But here's the cool part – we don't have to worry too much about the technical details of talking to a database (where we store all this user info). We have a friend called SQLAlchemy that helps us with that. SQLAlchemy is like a magic assistant that takes care of the communication between our app and the database. So, when a new user signs up, SQLAlchemy helps us save their info in the database.

The User model also has some superpowers. It can check if a password is correct, calculate a user's age from their date of birth, and even update or delete user information when needed. All these actions are part of what we call CRUD – Create, Read, Update, and Delete.

In simple terms, the User model is like a superhero that helps our app manage and organize information about all the cool people who use it. It's the backbone that keeps everything running smoothly, making sure our app knows who's who and what they're up to!



```python
"""Database Creation and Testing """


# Builds working data for testing
def initUsers():
    with app.app_context():
        """Create database and tables"""
        db.create_all()
        """Tester data for table"""
        u1 = User(name='Thomas Edison', uid='toby', password='123toby', dob=datetime(1847, 2, 11))
        u2 = User(name='Nikola Tesla', uid='niko', password='123niko')
        u3 = User(name='Alexander Graham Bell', uid='lex', password='123lex')
        u4 = User(name='Eli Whitney', uid='whit', password='123whit')
        u5 = User(name='Indiana Jones', uid='indi', dob=datetime(1920, 10, 21))
        u6 = User(name='Marion Ravenwood', uid='raven', dob=datetime(1921, 10, 21))


        users = [u1, u2, u3, u4, u5, u6]

        """Builds sample user/note(s) data"""
        for user in users:
            try:
                '''add user to table'''
                object = user.create()
                print(f"Created new uid {object.uid}")
            except:  # error raised if object nit created
                '''fails with bad or duplicate data'''
                print(f"Records exist uid {user.uid}, or error.")
                
initUsers()
```

## What this Did

In the code above we set up 6 users and it only took us inputing a few fields like Name, UID, password etc. Look how much easier it is to just call the User() and add in paramas than it would be to hard code every user. Thats the power behind Models. It may be alot of code to start but it allows for incredibily quick user creation and allows us to edit features the users have very quickly.



## Finding Users Using Our ID

Earlier we set up a few paramaters for the USER, but what do these let us do? A simple feature is finding the user by their ID. In code below we have a function called find_by_uid where the uid is passed in. Here we filter the query and then find the very first uid that matches the given uid. In simple words we just find the first ID that matches our desiered ID. 

Then we can check if the password the user puts in is equal to the password saved for that ID. First we would find the data for the user who has that ID. Then we would find the password for that user and check if the password matches the given password. 


```python
# SQLAlchemy extracts single user from database matching User ID
def find_by_uid(uid):
    with app.app_context():
        user = User.query.filter_by(_uid=uid).first()
    return user # returns user object

# Check credentials by finding user and verify password
def check_credentials(uid, password):
    # query email and return user record
    user = find_by_uid(uid)
    if user == None:
        return False
    if (user.is_password(password)):
        return True
    return False
        
#check_credentials("indi", "123qwerty")
```

## How to Make Users?

Making users is the most crucial part, but you may be thinking didn't we already make our users earlier?  Yes we did but that was with us hard coding it what if we wanted the user to input their own information like sign up pages do?. Well to do that we need to make a Create function.



```python
# Inputs, Try/Except, and SQLAlchemy work together to build a valid database object
def create():
    # optimize user time to see if uid exists
    uid = input("Enter your user id:")
    user = find_by_uid(uid)
    try:
        print("Found\n", user.read())
        return
    except:
        pass # keep going
    
    # request value that ensure creating valid object
    name = input("Enter your name:")
    password = input("Enter your password")
    
    # Initialize User object before date
    user = User(name=name, 
                uid=uid, 
                password=password
                )
    
    # create user.dob, fail with today as dob
    dob = input("Enter your date of birth 'YYYY-MM-DD'")
    try:
        user.dob = datetime.strptime(dob, '%Y-%m-%d').date()
    except ValueError:
        user.dob = datetime.today()
        print(f"Invalid date {dob} require YYYY-mm-dd, date defaulted to {user.dob}")
           
    # write object to database
    with app.app_context():
        try:
            object = user.create()
            print("Created\n", object.read())
        except:  # error raised if object not created
            print("Unknown error uid {uid}")
        
create()
```

In the code above we have some basic functions. We ask the user various inputs and store the name, password etc. Then we call our User function and input these details. Then we check if theres any form errors. These are all the basic functionalitys that forms due but the cod ebehind them can be quite complex at some times. Thats why it is so important to study how these models, and functions work to ensure perfect app functionality. 

## Optional Hacks

-Add this to your website </br>
-Create the delete and update user functions </br>
-Create USer functionality i.e you return the id of the user who presses a certain button. 
