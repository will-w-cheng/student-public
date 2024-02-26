---
comments: True
layout: notebook
title: Class 3- JWT Implimentation
description: Teamteach by Lindsay, Anika, Grace, Samhita
type: collab
courses: {'csp': {'week': 19}}
---

# JWT Implimentation

![JWT](https://files.catbox.moe/t69vm3.png)

## What is a JWT (JSON Web Token)?

JSON Web Tokens (JWT) serve as a secure means of transmitting information in JSON format, providing a way to establish trust between different parties in a web application. 
- Typically used to transmit information about an authenticated user and additional metadata (usernames, user ID, email, roles, etc.).

### Parts of a JWT:

![Parts](https://files.catbox.moe/19taua.png)

Each section is divided by a dot
- Header (red): Consists of two parts, how the JWT is encoded, such as the type of token (JWT) and the signing algorithm being used.



```python
{
  # For example:
  "alg": "HS256",
  "typ": "JWT"
}
```

- Payload (purple): Contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: registered, public, and private claims.


```python
{
  # For Example:
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

- Signature (teal): Created by combining the encoded header, encoded payload, and a secret (or key) using the specified algorithm. This signature is used to verify that the sender of the JWT is who it says it is and to ensure that the message wasn't changed along the way.


```python
# Using the HMAC SHA256 algorithm the signature will be created as such:
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

### HMAC and RSA or ECDSA Keys:

Used for signing JWT tokens
- HMAC Algorithm (Secret Key): 
  - HMAC (Hash-based Message Authentication Code)
  - A secret key is used to both create and verify the signature.
  - The issuer (who creates the JWT) uses a secret key and a hashing algorithm to create a signature by combining the encoded header and payload.
  - The recipient (who validates the JWT) uses the same secret key to independently calculate the signature and verify that it matches the one provided in the JWT.
  - Symmetric key solution: same key used for signing and verification
- RSA or ECDSA (Public/Private Key Pair):
  - RSA (Rivest–Shamir–Adleman) or ECDSA (Elliptic Curve Digital Signature Algorithm)
  - A pair of keys is used: a private key for signing and a corresponding public key for verification.
  - The issuer signs the JWT using their private key, and the signature is included in the JWT.
  - The recipient, who wants to verify the JWT, uses the public key associated with the issuer to check the signature's validity.
  - Asymmetric key solution: private key is kept secret, and only the public key is shared.

## Rest APIs and JSON Web Tokens

### Rest APIs:

![JWT](https://files.catbox.moe/mc4jvz.png)

- REST (Representational State Transfer) API (Application Programming Interface)
- Architectural style for designing networked applications
- Set of rules and conventions for building and interacting with web services that adhere to the principles of REST.

Principals of REST-
- Statelessness: Each request from a client to a server must contain all the information needed to understand and fulfill the request. The server should not store any information about the client's state between requests. This makes the system scalable and easy to maintain.
- Client-Server Architecture: The client and server are separate entities that communicate over a network. The client is responsible for the user interface and user experience, while the server is responsible for processing requests, managing resources, and handling business logic.
- Uniform Interface: RESTful APIs have a uniform and consistent interface, which simplifies the architecture and promotes a clear separation of concerns. The uniform interface is defined by several constraints, including resource identification through URIs (Uniform Resource Identifiers), resource manipulation through representations, and self-descriptive messages.
- Representation: Resources can have multiple representations, such as JSON or XML, which can be selected based on the client's needs or capabilities. The representation contains the current state of the resource.

### REST APIs and JWT:

A Java Web Token (JWT) is often used in the context of RESTful APIs to secure and authenticate communication between clients and servers.
- Authentication and Authorization: When a client makes a request to a RESTful API, the server may need to verify the identity of the client and determine whether the client has the necessary permissions to perform the requested operation. JWTs can be used to securely transmit authentication information (such as user identity and roles) between the client and server.
- Stateless Communication: RESTful APIs typically follow the stateless constraint, meaning that each request from the client to the server should contain all the information needed to understand and fulfill the request. JWTs provide a way to include authentication and authorization information directly within the token, eliminating the need for the server to store session state.
- Token-Based Authentication: Instead of relying on sessions and cookies, which are commonly used in traditional web applications, JWTs allow for token-based authentication. When a user logs in, the server issues a JWT containing relevant user information and a signature to ensure its integrity. The client then includes this token in the headers of subsequent requests, allowing the server to authenticate and authorize the user.
- Secure Transmission: JWTs can be signed and, optionally, encrypted, providing a secure way to transmit information between the client and server. The server can verify the integrity of the token by checking its signature, ensuring that the information it contains has not been tampered with.

## Implimenting JWT in Flask Using PyJWT

#### 1) Add PyJWT to requirements.txt

PyJWT will be used to encode and decode JWT tokens
Flask_SqlAlchemy
Flask_Migrate
Flask_Restful
Flask_Cors
PyJWT
#### 2) Add a Secret Key as App Config

Modify the app.config ['SECRET_KEY'] to try and get secret key for encoding and decoding the JWT from the variable SECRET_KEY. It defaults to "SECRET_KEY" for the key.


```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate
import os

"""
These objects can be used throughout project.
"""
@@ -14,7 +15,8 @@
dbURI = 'sqlite:///volumes/sqlite.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
app.config['SQLALCHEMY_DATABASE_URI'] = dbURI
SECRET_KEY = os.environ.get('SECRET_KEY') or 'SECRET_KEY'
app.config['SECRET_KEY'] = SECRET_KEY
db = SQLAlchemy()
Migrate(app, db)
```

#### 3) Migration Script Hashes Passwords and New Valid Hash Method

We need to prevent storing passwords in plaintext (for security reasons) so we need to hash passwords when initializing users in the database (in migration sript). All the user set_password methods are set to the same hash method.

##### Migration Script Hashes Passwords


```python
from alembic import op
import sqlalchemy as sa
from datetime import date
from werkzeug.security import generate_password_hash


# revision identifiers, used by Alembic.
revision = '5ac11951f352'
down_revision = None
branch_labels = None
depends_on = None
def upgrade():
    # ### commands auto generated by Alembic - please adjust! ###
    players_table = op.create_table('players',
    sa.Column('id', sa.Integer(), nullable=False),
    sa.Column('_name', sa.String(length=255), nullable=False),
    sa.Column('_uid', sa.String(length=255), nullable=False),
    sa.Column('_password', sa.String(length=255), nullable=False),
    sa.Column('_tokens', sa.Integer(), nullable=True),
    sa.PrimaryKeyConstraint('id'),
    sa.UniqueConstraint('_uid')
    )
    users_table = op.create_table('users',
    sa.Column('id', sa.Integer(), nullable=False),
    sa.Column('_name', sa.String(length=255), nullable=False),
    sa.Column('_uid', sa.String(length=255), nullable=False),
    sa.Column('_password', sa.String(length=255), nullable=False),
    sa.Column('_dob', sa.Date(), nullable=True),
    sa.PrimaryKeyConstraint('id'),
    sa.UniqueConstraint('_uid')
    )
    posts_table = op.create_table('posts',
    sa.Column('id', sa.Integer(), nullable=False),
    sa.Column('note', sa.Text(), nullable=False),
    sa.Column('image', sa.String(), nullable=True),
    sa.Column('userID', sa.Integer(), nullable=True),
    sa.ForeignKeyConstraint(['userID'], ['users.id'], ),
    sa.PrimaryKeyConstraint('id')
    )
    op.bulk_insert(players_table,
    [
        {'id': 1,
        '_name': "Azeem Khan",
        '_uid': "azeemK",
        '_password': generate_password_hash("123qwerty", "pbkdf2:sha256", salt_length=10),
        "_tokens": 45},
        {'id': 2,
        '_name': "Ahad Biabani",
        '_uid': "ahadB",
        '_password': generate_password_hash("123qwerty", "pbkdf2:sha256", salt_length=10),
        "_tokens": 41},
        {'id': 3,
        '_name': "Akshat Parikh",
        '_uid': "akshatP",
        '_password': generate_password_hash("123qwerty", "pbkdf2:sha256", salt_length=10),
        "_tokens": 40},
        {'id': 4,
        '_name': "Josh Williams",
        '_uid': "joshW",
        '_password': generate_password_hash("123qwerty", "pbkdf2:sha256", salt_length=10),
        "_tokens": 38},
    ]
    )
    op.bulk_insert(users_table,
    [
        {'id': 1,
        '_name': "Thomas Edison",
        '_uid': "toby",
        '_password': generate_password_hash("123toby", "pbkdf2:sha256", salt_length=10),
        "_dob": date(1847, 2, 11)},
        {'id': 2,
        '_name': "Nicholas Tesla",
        '_uid': "niko",
        '_password': generate_password_hash("123niko", "pbkdf2:sha256", salt_length=10),
        "_dob": date(1856, 7, 10)},
        {'id': 3,
        '_name': "Alexander Graham Bell",
        '_uid': "lex",
        '_password': generate_password_hash("123qwerty", "pbkdf2:sha256", salt_length=10),
        "_dob": date.today()},
        {'id': 4,
        '_name': "Grace Hopper",
        '_uid': "hop",
        '_password': generate_password_hash("123hop", "pbkdf2:sha256", salt_length=10),
        "_dob": date(1906, 12, 9)},
    ]
    )
    op.bulk_insert(posts_table,
    [
        {'id': 1,
        'note': "#### Thomas Edison Test Note ####",
        'image': "ncs_logo.png",
        'userID': 1
        },
        {'id': 2,
        'note': "#### Nicholas Tesla Test Note ####",
        'image': "ncs_logo.png",
        'userID': 2
        },
        {'id': 3,
        'note': "#### Alexander Graham Bell Test Note ####",
        'image': "ncs_logo.png",
        'userID': 3
        },
        {'id': 4,
        'note': "#### Grace Hopper Test Note ####",
        'image': "ncs_logo.png",
        'userID': 4},
    ]
    )
    # ### end Alembic commands ###
def downgrade():
    # ### commands auto generated by Alembic - please adjust! ###
    op.drop_table('posts')
    op.drop_table('users')
    op.drop_table('players')
    # ### end Alembic commands ###
```

##### New Valid Hash Method


```python
    # update password, this is conventional setter
    def set_password(self, password):
        """Create a hashed password."""
        self._password = generate_password_hash(password, "pbkdf2:sha256", salt_length=10)

    # check password parameter versus stored/encrypted password
    def is_password(self, password):
```

#### 4) Checking JWT Token and Authentication

This authentication middleware functions as a checkpoint for all incoming requests to the web server before reaching the API. Its primary task is to check for the presence of a JWT cookie in the incoming request. In cases where the cookie is absent, the middleware responds with a 401 Unauthorized Error, indicating that the required token is missing. If a cookie is found, the middleware proceeds to decode the token, extracting the user ID (uid). Following this, it validates the existence of a user associated with that ID.


```python
from functools import wraps
import jwt
from flask import request, abort
from flask import current_app
from model.users import User

def token_required(f):
    @wraps(f)
    def decorated(*args, **kwargs):
        token = request.cookies.get("jwt")
        print(token)
        if not token:
            return {
                "message": "Authentication Token is missing!",
                "data": None,
                "error": "Unauthorized"
            }, 401
        try:
            data=jwt.decode(token, current_app.config["SECRET_KEY"], algorithms=["HS256"])
            print(data["_uid"])
            current_user=User.query.filter_by(_uid=data["_uid"]).first()
            if current_user is None:
                return {
                "message": "Invalid Authentication token!",
                "data": None,
                "error": "Unauthorized"
            }, 401
        except Exception as e:
            return {
                "message": "Something went wrong",
                "data": None,
                "error": str(e)
            }, 500

        return f(current_user, *args, **kwargs)

    return decorated
```

#### 5) Authenticate Returns from Generaated JWT Tokens

The endpoint /api/users/authenticate now provides a JWT token based on the request's JSON data, which includes the uid and password. Several checks are performed, ensuring the presence of the request body, existence of the uid, presence of a user with the specified uid, and correctness of the provided password. If all checks pass, the uid is encoded into a JWT token, which is then returned as a cookie.

Additionally, the @token_required decorator is applied to the get and post methods so that only authenticated users can reach and access resources.


```python
import json, jwt
from flask import Blueprint, request, jsonify, current_app, Response
from flask_restful import Api, Resource # used for REST API building
from datetime import datetime
from auth_middleware import token_required

from model.users import User

user_api = Blueprint('user_api', __name__,
                   url_prefix='/api/users')
# API docs https://flask-restful.readthedocs.io/en/latest/api.html
api = Api(user_api)

class UserAPI:        
    class _CRUD(Resource):  # User API operation for Create, Read.  THe Update, Delete methods need to be implemeented
        @token_required
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
            # look for password and dob
            password = body.get('password')
            dob = body.get('dob')
            ''' #1: Key code block, setup USER OBJECT '''
            uo = User(name=name, 
                      uid=uid)
            
            ''' Additional garbage error checking '''
            # set password if provided
            if password is not None:
                uo.set_password(password)
            # convert to date type
            if dob is not None:
                try:
                    uo.dob = datetime.strptime(dob, '%Y-%m-%d').date()
                except:
                    return {'message': f'Date of birth format error {dob}, must be mm-dd-yyyy'}, 400
            
            ''' #2: Key Code block to add user to database '''
            # create user in database
            user = uo.create()
            # success returns json of user
            if user:
                return jsonify(user.read())
            # failure returns error
            return {'message': f'Processed {name}, either a format error or User ID {uid} is duplicate'}, 400
        
        @token_required
        def get(self, current_user): # Read Method
            users = User.query.all()    # read/extract all users from database
            json_ready = [user.read() for user in users]  # prepare output in json
            return jsonify(json_ready)  # jsonify creates Flask response object, more specific to APIs than json.dumps

    class _Security(Resource):
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
                print(user._uid,user._password)
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
                                httponly=True,
                                path='/'
                                # domain="frontend.com"
                                )
                        return resp
                    except Exception as e:
                        return {
                            "error": "Something went wrong",
                            "message": str(e)
                        }, 500
                return {
                    "message": "Error fetching auth token!, invalid email or password",
                    "data": None,
                    "error": "Unauthorized"
                },
            except Exception as e:
                return {
                        "message": "Something went wrong!",
                        "error": str(e),
                        "data": None
                }, 500



    # building RESTapi endpoint
    api.add_resource(_CRUD, '/')
    api.add_resource(_Security, '/authenticate')

```

## Implimenting JWT in Flask Using Flask-JWT-Extended

#### 1) Install Flask-JWT-Extended


```python
pip install Flask-JWT-Extended
```

#### 2) Include JWT Library in Flask App Setup


```python
from flask_jwt_extended import JWTManager

# You don't have to add this again if you already have it.
app = Flask(__name__)

# Setup the Flask-JWT-Extended extension
app.config["JWT_SECRET_KEY"] = "SECRET_KEY"  # Remember to change "secret" to a more complex key
jwt = JWTManager(app)
```

#### 3) Create an Endpoint for Generating Tokens

Using POST because it is creating tokens (POST is for creation)


```python
POST /token
Content-type: application/json
Body:
{
     "username": "alesanchezr",
     "password": "12341234"
}
```


```python
from flask_jwt_extended import create_access_token

# Create a route to authenticate your users and return JWT Token
# The create_access_token() function is used to actually generate the JWT
@app.route("/token", methods=["POST"])
def create_token():
    username = request.json.get("username", None)
    password = request.json.get("password", None)

    # Query your database for username and password
    user = User.query.filter_by(username=username, password=password).first()

    if user is None:
        # The user was not found on the database
        return jsonify({"msg": "Bad username or password"}), 401
    
    # Create a new token with the user id inside
    access_token = create_access_token(identity=user.id)
    return jsonify({ "token": access_token, "user_id": user.id })
```

#### 4) Use @jwt_required() Decorator on Private Routes

Endpoints that require authorization (private endpoints) should use the @jwt_required() decorator. You can retrieve valid, authenticated user information using the get_jwt_identity function. 


```python
from flask_jwt_extended import jwt_required, get_jwt_identity

# Protect a route with jwt_required, which will kick out requests without a valid JWT
@app.route("/protected", methods=["GET"])
@jwt_required()
def protected():
    # Access the identity of the current user with get_jwt_identity
    current_user_id = get_jwt_identity()
    user = User.query.get(current_user_id)
    
    return jsonify({"id": user.id, "username": user.username }), 200
```

## Implimenting JWT in Front-End

#### 1) Create a New Token

Based on earlier endpoints, we have to POST /token with username + password information in request body.


```python
const login = async (username, password) => {
     const resp = await fetch(`https://your_api.com/token`, { 
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ username, password }) 
     })

     if(!resp.ok) throw Error("There was a problem in the login request")

     if(resp.status === 401){
          throw("Invalid credentials")
     }
     else if(resp.status === 400){
          throw ("Invalid email or password format")
     }
     const data = await resp.json()
     // Save your token in the localStorage
     // Also you should set your user into the store using the setItem function
     localStorage.setItem("jwt-token", data.token);

     return data
}
```

#### 2) Retrieving Information

Now, lets say I've logged in to the front-end application and I want to retrieve sensitive data:


```python
// Assuming "/protected" is a private endpoint
const getMyTasks = async () => {
     // Retrieve token from localStorage
     const token = localStorage.getItem('jwt-token');

     const resp = await fetch(`https://your_api.com/protected`, {
        method: 'GET',
        headers: { 
          "Content-Type": "application/json",
          'Authorization': 'Bearer ' + token // ⬅⬅⬅ authorization token
        } 
     });

     if(!resp.ok) {
          throw Error("There was a problem in the login request")
     } else if(resp.status === 403) {
          throw Error("Missing or invalid token");
     } else {
         throw Error("Unknown error");
     }

     const data = await resp.json();
     console.log("This is the data you requested", data);
     return data
}
```

## CORS Configuration:

Cross-Origin Resource Sharing (CORS) is a crucial aspect of web development, allowing or restricting requests from different origins. This configuration is essential to ensure that your Flask application can seamlessly handle requests from various sources, promoting security and compatibility.

Change: Added CORS support for deployed and local runs.
- Allows Flask to handle requests from different origins. The inclusion of supports_credentials=True ensures that credentials, such as cookies, can be sent and received.


```python
cors = CORS(app, supports_credentials=True)
```

### Dynamic Allowed Origins:

The concept of "Dynamic Allowed Origins" refers to the ability to dynamically set the allowed origins for Cross-Origin Resource Sharing (CORS) based on the incoming request's 'Origin' header. In CORS, the 'Origin' header indicates the origin (domain) of the requesting client.

Change: A before_request hook is implemented to dynamically set the allowed origin based on the incoming request's 'Origin' header.
- Helps prevent unauthorized cross-origin requests by allowing only specified origins.


```python
@app.before_request
def before_request():
    allowed_origin = request.headers.get('Origin')
    if allowed_origin in ['http://localhost:4100', 'http://127.0.0.1:4100', 'https://nighthawkcoders.github.io']:
        cors._origins = allowed_origin
```

### Same Site Attribute in set_cookie:

The SameSite attribute in a cookie is a security feature that controls whether a cookie should be sent with cross-site requests. It is set within the Set-Cookie header when a server instructs a browser to store a cookie on the user's device. The SameSite attribute helps mitigate certain types of cross-site request forgery (CSRF) attacks.

Change: The SameSite attribute is set to 'None' in the set_cookie method to allow cross-site requests.
- Allows for cookies to be sent with cross-site requests, especially when working with front-end applications hosted on different domains.


```python
resp.set_cookie(
    "jwt",
    token,
    max_age=3600,
    secure=True,
    httponly=True,
    path='/',
    samesite='None'
)
```

### Nginx Preflighted Requests Configuration:

The Nginx preflighted requests configuration is designed to handle preflighted requests. Preflighted requests are HTTP OPTIONS requests sent by the browser before the actual request to check whether the server will accept the actual request.

Change: Nginx configuration is added to handle preflighted requests, ensuring that only the specified frontend server is allowed.
- Includes headers necessary for proper CORS handling during preflight checks made by the browser, ensuring that only the designated frontend server is allowed for preflighted requests. 


```python
if ($request_method = OPTIONS) {
    add_header "Access-Control-Allow-Credentials" "true" always;
    add_header "Access-Control-Allow-Origin"  "https://nighthawkcoders.github.io" always;
    add_header "Access-Control-Allow-Methods" "GET, POST, PUT, OPTIONS, HEAD" always;
    add_header "Access-Control-Allow-MaxAge" 600 always;
    add_header "Access-Control-Allow-Headers" "Authorization, Origin, X-Requested-With, Content-Type, Accept" always;
    return 204;
}
```

## Cookies

![Cookie](https://files.catbox.moe/yxzao5.png)

Cookies are small pieces of data stored on the user's browser by website
- Primarily used for session management, user authentication, and tracking user behavior.
- Store authentication tokens to allow the user to stay authenticated on the server
- Sent between the client (browser) and the server with each HTTP request, providing a way to maintain stateful information.
- With each interaction, the server can store the user session, manage session info, and store user preferences


### Cookies and JWT

Cookies can be used to store JWTs.
- When a user logs in, the server can send a JWT as a cookie, and the browser will include the JWT in subsequent requests to the server.
- Stateless authentication while still leveraging the benefits of cookies for managing sessions and user information.

The process of maintaining tokens in cookies and transmitting them in HTTP requests involves several steps (we've gone over this earlier, but lets go through it again in the context of cookies):

1. Token Generation and Storage:
- When a user logs in, the server generates a token (e.g., JWT - JSON Web Token) containing user information and possibly permissions.
- This token is then stored in a cookie on the user's device. Cookies are pieces of data sent from the server and stored on the client side.
2. Cookie Storage and Retrieval:
- The cookie is typically stored in the user's browser. It includes attributes such as domain, path, expiration time, and the secure flag.
- For subsequent requests, the browser automatically includes the relevant cookies in the HTTP headers.
3. Transmission in HTTP Request:
- When the user makes an HTTP request to the server (e.g., by navigating to a different page or sending an AJAX request), the browser includes the cookies associated with the domain in the request headers.
- The server extracts the token from the cookie in the incoming HTTP request.
4. Token Verification:
- The server verifies the token to ensure its authenticity and integrity. This involves checking the signature in the case of JWT.
- If the token is valid, the server can extract user information and use it to process the request.

## Postman

![Postman](https://files.catbox.moe/dp76tr.webp)

Postman serves as a valuable tool in the realm of computer science, specifically designed for testing and interacting with Application Programming Interfaces (APIs). Postman can be likened to a sophisticated testing environment that facilitates the exploration of API functionalities.

Within Postman, users can craft and dispatch HTTP requests to APIs, allowing for a comprehensive examination of how different software components communicate and respond. This tool is instrumental in ensuring the seamless integration of APIs into software applications. Its intuitive interface provides a user-friendly platform to engage in the essential practice of testing and validating API behavior.

### Postman and JWT:

Postman allows you to include JWTs in your requests easily. Here's different ways of how you can use Postman to send a request with a JWT:

1. Authorization Tab
- Open your request in Postman.
- Go to the "Authorization" tab.
- Select "Bearer Token" from the "Type" dropdown.
- Paste your JWT token in the "Token" field.
2. Headers:
- Enter the JWT in the headers manually using the "Headers" tab by adding a key-value pair like Authorization: Bearer YOUR_JWT_TOKEN.

This way, Postman enables you to simulate API requests with JWTs, ensuring that your authentication mechanisms are working as expected. If everything is working as expected, you will recieve a status code in the 2xx range (e.g., 200 OK) which typically indicates success. If you do not recieve a 200 OK message, Postman will let you know what is wrong so you can catch errors in your code. 

### Postman and Cookies:

Similar to JWT, Postman allows you to manage cookies as efficently. Here's different ways you can work with cookies in Postman:

1. Cookies Tab:
- Open your request in Postman.
- Navigate to the "Cookies" tab.
- Add the necessary cookies by providing the key-value pairs.
2. Headers:
- Cookies can also be included in the request headers manually.

## Anatomy of Python Flask Repo 
### ([Teacher Flask Repo](https://github.com/nighthawkcoders/flask_portfolio))

![Part1](https://files.catbox.moe/vqejur.png)
![Part1](https://files.catbox.moe/glrmpa.png)

- main.py: The Python source file responsible for running, testing, and debugging your project. Its role is central to the execution of the entire project.
- Dockerfile and docker-compose.yml: These files play a vital role in running and testing your project within a Docker container, providing a simulated deployment environment, such as on AWS. They are crucial to ensuring the consistent functionality of your project across diverse machines.
- instances: Serving as the base location for data files meant to persist on the server, this directory retains files even after a web application restart. It stands apart from other files, which get recreated during restarts.
- static: Positioned as the foundational storage for files intended to be cached and concealed by the web server, this directory commonly houses unchanging files like images or JavaScript files throughout web server execution.
- api: Housing code that manages requests from external servers, this directory acts as the bridge connecting the external world to the logic and code within the rest of your project.
- model: Within this directory, you'll find files implementing backend functionality for various files in the api directory, such as direct interaction with the database.
- templates: This section holds files and subdirectories crucial for supporting the home and error pages of your project's site.
