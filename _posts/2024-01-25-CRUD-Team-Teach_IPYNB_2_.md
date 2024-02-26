---
toc: False
comments: True
layout: post
title: Team Teach - Full Stack and User Profile
description: CRUD backend and frontend, Authentication
type: hacks
courses: {'compsci': {'week': 19}}
---

# CRUD

## What is CRUD?

CRUD stands for:

C-reate: Involves the creation of addition of data to a database. In essence, it "create"s entries in databases.

R-ead: Involves the retrieval, querying, or "read"ing of existing data from a database.

U-pdate: Involves the modification or "update"ing of existing data in a database. Operation of changing the values of specific fields in a system. 

D-elete: Involves the removal or "delete"ion of existing data from a database. It's the operation of eliminating information from a database.

In the past, each function has had its own link to fetch from, but with CRUD all four functions will be under one link, differentiated by the request type most suited for it.
Create: POST request, as create operation needs to sent data back to the backend, best suited by post request
Read: GET request, as read operation is simple and requires no data to be sent back
Update: PUT request, as update requires the user ID of the user being updated, and this can be modified in the URL which PUT requests allow
Delete: DELETE request, self explanatory
This is simpler and makes fetching less confusing, as everything is done under one link. 

## Authentication
- How users will authenticate to be able to access function that require a token
- POST request is sent to backend
    - payload contains user ID and password
- Backend compares user ID and password, and returns with token if successful
- Note that authentication and authorization are two different things
    - Authentication is identifying who you are, client saying hi to backend
    - Authorization is getting permission to view something, website letting client know that they can view something

#### Frontend


```python
function login_user(){
    // Set Authenticate endpoint
    const url = 'http://127.0.0.1:8086/api/users/authenticate';

    // Set the body of the request to include login data from the DOM
    const body = {
        uid: document.getElementById("uid").value,
        password: document.getElementById("password").value,
    };

    // Change options according to Authentication requirements
    const authOptions = {
        mode: 'cors', // no-cors, *cors, same-origin
        credentials: 'include', // include, same-origin, omit
        headers: {
            'Content-Type': 'application/json',
        },
        method: 'POST', // Override the method property
        cache: 'no-cache', // Set the cache property
        body: JSON.stringify(body)
    };

    // Fetch JWT
    fetch(url, authOptions)
    .then(response => {
        // handle error response from Web API
        if (!response.ok) {
            const errorMsg = 'Login error: ' + response.status;
            console.log(errorMsg);
            alert("Failed Authentication: Credentials Incorrect")
            return;
        }
        // Success!!!
        // Redirect to the database page
        window.location.href = "/csp-blog//log/2024/01/30/Users.html";
    })
    // catch fetch errors (ie ACCESS to server blocked)
    .catch(err => {
        console.error(err);
    });
}

// Attach login_user to the window object, allowing access to form action
window.login_user = login_user;
```

#### Backend


```python
from werkzeug.security import generate_password_hash, check_password_hash
# update password, this is conventional setter
def set_password(self, password):
    """Create a hashed password."""
    self._password = generate_password_hash(password, "pbkdf2:sha256", salt_length=10)

# check password parameter versus stored/encrypted password
def is_password(self, password):
    """Check against hashed password."""
    result = check_password_hash(self._password, password)
    return result
```


```python
def post(self):
            try:
                body = request.get_json()
                if not body:
                    return {
                        "message": "Please provide user details",
                        "data": None,
                        "error": "Bad request"
                    }, 400
                ''' Get Data '''
                uid = body.get('uid')
                if uid is None:
                    return {'message': f'User ID is missing'}, 400
                password = body.get('password')
                
                ''' Find user '''
                user = User.query.filter_by(_uid=uid).first()
                if user is None or not user.is_password(password):
                    return {'message': f"Invalid user id or password"}, 400
                if user:
                    try:
                        token = jwt.encode(
                            {"_uid": user._uid},
                            current_app.config["SECRET_KEY"],
                            algorithm="HS256"
                        )
                        resp = Response("Authentication for %s successful" % (user._uid))
                        resp.set_cookie("jwt", token,
                                max_age=3600,
                                secure=True,
                                httponly=False,
                                path='/',
                                samesite='None'  # This is the key part for cross-site requests

                                # domain="frontend.com"
                                )
                        return resp
                    except Exception as e:
                        return {
                            "error": "Something went wrong",
                            "message": str(e)
                        }, 500
                return {
                    "message": "Error fetching auth token!",
                    "data": None,
                    "error": "Unauthorized"
                }, 404
            except Exception as e:
                return {
                        "message": "Something went wrong!",
                        "error": str(e),
                        "data": None
                }, 500

```

## Create
#### Frontend
The code below uses user entered data from a form, and sends a POST request to the backend with the user entered data.


```python
import { uri, options } from '{{site.baseurl}}/assets/js/api/config.js';
//
//    const url = uri + '/api/users/authenticate';
//    const body = {
//            // name: document.getElementById("name").value,
//            uid: "toby",
//            password: "123toby"
//            // dob: document.getElementById("dob").value
//        };
//    const authOptions = {
//            ...options, // This will copy all properties from options
//            method: 'POST', // Override the method property
//            cache: 'no-cache', // Set the cache property
//            body: JSON.stringify(body)//       };
//    fetch(url, authOptions)
    function login_user(){
        // Set Authenticate endpoint
        const url = uri + '/api/users/';

        // Set the body of the request to include login data from the DOM
        const body = {
            name: document.getElementById("name").value,
            uid: document.getElementById("uid").value,
            password: document.getElementById("password").value,
            dob: document.getElementById("dob").value
        };

        // Change options according to Authentication requirements
        const authOptions = {
            ...options, // This will copy all properties from options
            method: 'POST', // Override the method property
            cache: 'no-cache', // Set the cache property
            body: JSON.stringify(body)
        };

        // Fetch JWT
        fetch(url, authOptions)
        .then(response => {
            // handle error response from Web API
            if (!response.ok) {
                const errorMsg = 'Login error: ' + response.status;
                console.log(errorMsg);
                return;
            }
            // Success!!!
            // Redirect to the database page
            window.location.href = "{{site.baseurl}}/data/database";
        })
        // catch fetch errors (ie ACCESS to server blocked)
        .catch(err => {
            console.error(err);
        });
    }

    // Attach login_user to the window object, allowing access to form action
    window.login_user = login_user;
```

#### Backend
The backend then takes the user data, and adds a new user to the database, given that the code is input properly. Note the lack of token required, as this is the create method and shouldn't need authentication.


```python
def post(self, current_user): # Create method
            ''' Read data for json body '''
            body = request.get_json()
            
            ''' Avoid garbage in, error checking '''
            # validate name
            name = body.get('name')
            if name is None or len(name) < 2:
                return {'message': f'Name is missing, or is less than 2 characters'}, 400
            # validate uid
            uid = body.get('uid')
            if uid is None or len(uid) < 2:
                return {'message': f'User ID is missing, or is less than 2 characters'}, 400
            # look for password
            password = body.get('password')

            active_classes = body.get('active_classes')
            if active_classes is None or len(active_classes) == 0:
                return {'message': 'Active class is missing'}, 400

            archived_classes = body.get('archived_classes')

            ''' #1: Key code block, setup USER OBJECT '''
            uo = User(name=name, 
                      uid=uid,
                      active_classes=active_classes,
                      archived_classes=archived_classes)
            
            ''' Additional garbage error checking '''
            # set password if provided
            if password is not None:
                uo.set_password(password)
            # set server request status    
            
            ''' #2: Key Code block to add user to database '''
            # create user in database
            user = uo.create()
            # success returns json of user
            if user:
                return jsonify(user.read())
            # failure returns error
            return {'message': f'Processed {name}, either a format error or User ID {uid} is duplicate'}, 400
```


```python
    def create(self):
        try:
            # creates a person object from User(db.Model) class, passes initializers
            db.session.add(self)  # add prepares to persist person object to Users table
            db.session.commit()  # SqlAlchemy "unit of work pattern" requires a manual commit
            return self
        except IntegrityError:
            db.session.remove()
            return None
```

## Read
#### Frontend
This example read code sends a GET request to the backend. Note that read doesn't necessarily mean returning the entire database, but simply reading already existing information from the database. Note that the javaScript below creates a table with the retrieved information but other things can be done with it.


```python
// uri variable and options object are obtained from config.js
  import { uri, options } from '/teacher_portfolio/assets/js/api/config.js';

  // Set Users endpoint (list of users)
  const url = uri + '/api/users/';

  // prepare HTML result container for new output
  const resultContainer = document.getElementById("result");

  // fetch the API
  fetch(url, options)
    // response is a RESTful "promise" on any successful fetch
    .then(response => {
      // check for response errors and display
      if (response.status !== 200) {
          const errorMsg = 'Database response error: ' + response.status;
          console.log(errorMsg);
          const tr = document.createElement("tr");
          const td = document.createElement("td");
          td.innerHTML = errorMsg;
          tr.appendChild(td);
          resultContainer.appendChild(tr);
          return;
      }
      // valid response will contain JSON data
      response.json().then(data => {
          console.log(data);
          for (const row of data) {
            // tr and td build out for each row
            const tr = document.createElement("tr");
            const name = document.createElement("td");
            const id = document.createElement("td");
            const age = document.createElement("td");
            // data is specific to the API
            name.innerHTML = row.name; 
            id.innerHTML = row.uid; 
            age.innerHTML = row.age; 
            // this builds td's into tr
            tr.appendChild(name);
            tr.appendChild(id);
            tr.appendChild(age);
            // append the row to table
            resultContainer.appendChild(tr);
          }
      })
  })
  // catch fetch errors (ie ACCESS to server blocked)
  .catch(err => {
    console.error(err);
    const tr = document.createElement("tr");
    const td = document.createElement("td");
    td.innerHTML = err + ": " + url;
    tr.appendChild(td);
    resultContainer.appendChild(tr);
  });
```

#### Backend
The below code returns all users from the database in as JSON when fetched.


```python
@token_required
def get(self, current_user): # Read Method
    users = User.query.all()    # read/extract all users from database
    json_ready = [user.read() for user in users]  # prepare output in json
    return jsonify(json_ready)  # jsonify creates Flask response object, more specific to APIs than json.dumps
```

## Put
#### Frontend
The following code sends a put request to backend to update a user based on the user's UID.


```python
function update_user(){
      if (document.getElementById("password").value != document.getElementById("confirmpassword").value) {
        alert("Error: Passwords do not match.");
        return;
      }
      const body = {
        uid: document.getElementById("uid").value,
        password: document.getElementById("password").value,
        name: document.getElementById("name").value,
      };
      const AuthOptions = {
                  mode: 'cors', // no-cors, *cors, same-origin
                  credentials: 'include', // include, same-origin, omit
                  headers: {
                      'Content-Type': 'application/json',
                  },
                  method: 'PUT', // Override the method property
                  cache: 'no-cache', // Set the cache property
                  body: JSON.stringify(body)
              };
        // fetch the API
        fetch(url, AuthOptions)
          // response is a RESTful "promise" on any successful fetch
          .then(response => {
            // check for response errors and display
            if (response.status !== 200) {
                window.location.href = "/csp-blog/403.html";
            }
            // valid response will contain JSON data
            response.json().then(data => {
              // insert whatever code you want here
            })
        })
        // catch fetch errors (ie ACCESS to server blocked)
        .catch(err => {
          console.log(err)
        });
    }
    // Attach login_user to the window object, allowing access to form action
    window.update_user = update_user;
```

#### Backend


```python
@token_required
def put(self, current_user):
    body = request.get_json() # get the body of the request
    uid = body.get('uid') # get the UID (Know what to reference)
    name = body.get('name') # get name (to change)
    password = body.get('password') # get password (to change)
    users = User.query.all() # get users
    for user in users:
        if user.uid == uid: # find user with matching uid
            user.update(name,'',password) # update info
    return f"{user.read()} Updated"
```

## Delete
#### Frontend
Similarly to put, this code removes the appropriate user from the database


```python
function delete_user(){
    const body = {
      uid: document.getElementById("duid").value,
    };
    const AuthOptions = {
                mode: 'cors', // no-cors, *cors, same-origin
                credentials: 'include', // include, same-origin, omit
                headers: {
                    'Content-Type': 'application/json',
                },
                method: 'DELETE', // Override the method property
                cache: 'no-cache', // Set the cache property
                body: JSON.stringify(body) // delete if using backend code that fetches directly from the cookie
            };
      // fetch the API
      fetch(url, AuthOptions)
        // response is a RESTful "promise" on any successful fetch
        .then(response => {
          // check for response errors and display
          if (response.status !== 200) {
              window.location.href = "/csp-blog/403.html";
          }
          // valid response will contain JSON data
          response.json().then(data => {
            window.location.href = "/csp-blog//log/2024/01/30/Users.html";
          })
      })
      // catch fetch errors (ie ACCESS to server blocked)
      .catch(err => {
        console.log(err)
      });
  }
  window.delete_user = delete_user;
```

#### Backend

## Mr.Mortensen Version


```python
def delete(self, id):  # Delete method
#Find user by ID 
user = User.query.get(id)
if user is None:
    return {'message': f'User with ID {id} not found'}, 404

''' Delete user '''
user.delete()
return {'message': f'User with ID {id} has been deleted'}
```

## Ian's Version


```python
@token_required
def delete(self, current_user):
    body = request.get_json()
    uid = body.get('uid')
    users = User.query.all()
    for user in users:
        if user.uid == uid:
            user.delete()
    return jsonify(user.read())
```

## Tarun's Version


```python
@token_required
def delete(self, current_user):
    token = request.cookies.get("jwt")
    cur_user= data=jwt.decode(token, current_app.config["SECRET_KEY"], algorithms=["HS256"])['_uid']
    users = User.query.all()
    for user in users:
        if user.uid == uid and user.id==cur_user: # modified with the and user.id==cur_user so random users can't delete other ppl
            user.delete()
        elif(user.uid == uid):
            print(cur_user," tried to delete someone who they are not")
            return 
    return jsonify(user.read())
```
