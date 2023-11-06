---
toc: True
comments: True
layout: post
title: Individual Review
description: What we learned this week, and all the amazing things we have accomplished
courses: {'csp': {'week': 10}}
type: tangibles
---

# Issues:

- []
- [JPG base64 image displayment issue](https://github.com/rliao569/Frontend-CSP/issues/11) - Crucial for exemplifying how URI's (Unique Resource Identifier) and can call upon the data points 
- [Movement of the target on DOM events, flag logic](https://github.com/rliao569/Frontend-CSP/issues/8) - Added a flag to check bsaed on DOM events and only moved upon once it finished



# Backend - creating an API endpoint



## Main.py and functionality for the API here
- Functionality of how everything works underneath the main.py:
- <img src="https://cdn.discordapp.com/attachments/1151587106322382948/1168426411531448432/image.png?ex=6551b8e4&is=653f43e4&hm=2ebc676979aa659fa5ebf786ecd0376e6db3f28cbee8ab16abd0d8fe83cd9f21&">
- Essentially what the main.py does and it's relevance is it calls upon the model and the API, the model is where the initial data is initialized and the API is how it handles requests.

## Specific code within the main.py
- [Main.py commit](https://github.com/will-w-cheng/team-influencer-innovator-backend/commit/5f71b2c2b92bf95798d4fba4bce7c6b403023cc5#diff-b10564ab7d2c520cdd0243874879fb0a782862c3c902ab535faabe57d5a505e1)
- Importing modules is crucial, as seen in the Python Libraries lesson we can import modules and libraries from other code. One way that the backend does this is through the main.py file in the flask server where it calls upon the model file where we can initialize the code
- We can also incorporate the use of the setting up an API and registering it as URi through importing the main function within the API.locations





```python
import threading

# import "packages" from flask
from flask import render_template  # import render_template from "public" flask libraries

# import "packages" from "this" project
from __init__ import app,db  # Definitions initialization
from model.users import initLeaderboard
from model.locations import init_locations

# setup APIs\
from api.player import player_api
from api.locations import location_api

# setup App pages
from projects.projects import app_projects # Blueprint directory import projects definition


# Initialize the SQLAlchemy object to work with the Flask app instance
db.init_app(app)

# register URIs
app.register_blueprint(app_projects) # register app pages
app.register_blueprint(location_api)

@app.errorhandler(404)  # catch for URL not found
def page_not_found(e):
    # note that we set the 404 status explicitly
    return render_template('404.html'), 404

@app.route('/')  # connects default URL to index() function
def index():
    return render_template("index.html")

@app.route('/table/')  # connects /stub/ URL to stub() function
def table():
    return render_template("table.html")

@app.before_first_request
def activate_job():
    db.drop_all()  # Clear the database
    db.create_all()  # Recreate the database schema
    initPlayers()
    init_locations()



# this runs the application on the development server
if __name__ == "__main__":
    # change name for testing
    from flask_cors import CORS
    cors = CORS(app)
    app.run(debug=True, host="0.0.0.0", port="8242")

```

## the api/locations.py file:
- The API locations.py is how it handles the requests including put, get, delete, and post requests. For our project, we really only need to have get requests since we don't really need to make any other requests to post any new locations, but we added functionality for it in case we wanted to make it easier to add things to the database. 


## api/users.py
- For just two fields where it's the user and the points assigned to the name of the user and points, however it also handles POST requests
- <img src="https://cdn.discordapp.com/attachments/1151587106322382948/1168429990417813564/image.png?ex=6551bc3a&is=653f473a&hm=253a548986a46c8d5477b4ea2913f83a59dcf5cbcef54e6bf8135ea34a9266d9&">

## Learning
- Learning how to create blueprints, endpoints, and handling the GET requests similar to how it was done in previuso example codes. I also incorporate POST requests to the different users and whatnot 


```python
from flask import Blueprint, jsonify
from flask_restful import Api, Resource, reqparse
from __init__ import db
from model.locations import Location

# Create a Blueprint for the location API
location_api = Blueprint('location_api', __name__, url_prefix='/api/locations')

# Create the API instance
api = Api(location_api)

class LocationAPI(Resource):
    def get(self):
        # Retrieve all locations from the database
        locations = Location.query.all()

        # Prepare the data in JSON format
        json_ready = [location.to_dict() for location in locations]

        # Return the JSON response
        return jsonify(json_ready)

    def post(self):
        parser = reqparse.RequestParser()
        parser.add_argument("location_name", required=True, type=str)
        parser.add_argument("image", required=True, type=str)
        args = parser.parse_args()
        location = Location(args["location_name"], args["image"])

        try:
            db.session.add(location)
            db.session.commit()
            return location.to_dict(), 201
        except Exception as exception:
            db.session.rollback()
            return {"message": f"Error: {exception}"}, 500

    def put(self):
        parser = reqparse.RequestParser()
        parser.add_argument("id", required=True, type=int)
        parser.add_argument("location_name", type=str)
        parser.add_argument("image", type=str)
        args = parser.parse_args()

        try:
            location = db.session.query(Location).get(args["id"])
            if location:
                if args["location_name"] is not None:
                    location.location_name = args["location_name"]
                if args["image"] is not None:
                    location.image = args["image"]
                db.session.commit()
                return location.to_dict(), 200
            else:
                return {"message": "Location not found"}, 404
        except Exception as exception:
            db.session.rollback()
            return {"message": f"Error: {exception}"}, 500

    def delete(self):
        parser = reqparse.RequestParser()
        parser.add_argument("id", required=True, type=int)
        args = parser.parse_args()

        try:
            location = db.session.query(Location).get(args["id"])
            if location:
                db.session.delete(location)
                db.session.commit()
                return location.to_dict()
            else:
                return {"message": "Location not found"}, 404
        except Exception as exception:
            db.session.rollback()
            return {"message": f"Error: {exception}"}, 500

# Add the LocationAPI resource to the /api/locations endpoint
api.add_resource(LocationAPI, "/")

class LocationListAPI(Resource):
    def get(self):
        # Retrieve all locations from the database
        locations = Location.query.all()

        # Prepare the data in JSON format
        json_ready = [location.to_dict() for location in locations]

        # Return the JSON response
        return jsonify(json_ready)

# Add the LocationListAPI resource to the /api/locationsList endpoint
api.add_resource(LocationListAPI, "/api/locations")
```


```python
import json
from flask import Blueprint, request, jsonify
from flask_restful import Api, Resource  # used for REST API building

from model.users import User

user_api = Blueprint('user_api', __name__,
                     url_prefix='/api/leaderboard')

# API docs https://flask-restful.readthedocs.io/en/latest/api.html
api = Api(user_api)

class LeaderboardAPI:
    class _CRUD(Resource):
        def post(self):
            '''
            Create a new user entry in the leaderboard table.
            Read data from the JSON body.
            '''
            body = request.get_json()

            # Validate username
            username = body.get('username')
            if username is None or len(username) < 2:
                return {'message': f'Username is missing or is less than 2 characters'}, 400

            # Validate points (should be a non-negative integer)
            points = body.get('points')
            if not isinstance(points, int) or points < 0:
                return {'message': 'Points must be a non-negative integer'}, 400

            # Create a new leaderboard entry
            leaderboard_entry = User(username=username, points=points)
            leaderboard_entry.create()

            # Return the newly created leaderboard entry
            return jsonify({'username': leaderboard_entry.username, 'points': leaderboard_entry.points})

        def get(self):
            '''
            Retrieve the leaderboard data.
            Read all leaderboard entries and prepare the output in JSON format.
            '''
            leaderboard_entries = User.query.all()
            leaderboard_data = [{'username': entry.username, 'points': entry.points} for entry in leaderboard_entries]
            return jsonify(leaderboard_data)
        
        def put(self):
            ''' Update user points '''
            body = request.get_json()
            username = body.get('username')
            new_points = body.get('points')

            user = User.query.filter_by(username=username).first()
            if user is None:
                return {'message': 'User not found'}, 404

            if new_points is not None:
                user.update_points(new_points)
                return {'message': f'Updated points for user {user.username}'}



    # Building REST API endpoints
    api.add_resource(_CRUD, '/')  # Create and Read operations

```

## model/locations.py and model/users.py
- Locations.py in the model is where the initial data is loaded and we can add some instances for it to work
- Here base64 is encoded for the images, and we also assign specific things to the database 




```python
from __init__ import db
import base64

class Location(db.Model):
    __tablename__ = "locations"

    id = db.Column(db.Integer, primary_key=True)
    location_name = db.Column(db.String, nullable=False)
    image = db.Column(db.String, nullable=False)

    def __init__(self, location_name, image):
        self.location_name = location_name
        self.image = image

    def to_dict(self):
        return {"id": self.id, "location_name": self.location_name, "image": self.image}

def image_to_base64(image_path):
    with open(image_path, "rb") as image_file:
        image_binary = image_file.read()
        base64_encoded = base64.b64encode(image_binary)
        base64_string = base64_encoded.decode("utf-8")
        return base64_string

# Example usage
image_path = "static/assets/IMG_0902.jpg"  # Relative path to the image
base64_data = image_to_base64(image_path)
image_path2 = "static/assets/IMG_0908.jpg"  # Another relative path to a different image
base64_data2 = image_to_base64(image_path2)
# locationposition=(20, 45)
# AND locationposition=(20, 45)
def init_locations():
    location1 = Location(location_name="20, 45", image=base64_data)
    location2 = Location(location_name="35, 40", image=base64_data2)
    # location3 = Location(location_name="Location 3", image="image3.jpg")  # Placeholder for the third image

    db.session.add(location1)
    db.session.add(location2)
    # db.session.add(location3)

    db.session.commit()

if __name__ == '__main__':
    init_locations()

```


```python
from datetime import date
import os
import base64
import json
from sqlalchemy.exc import IntegrityError
from werkzeug.security import generate_password_hash, check_password_hash

from __init__ import app, db

# Define the User class for the leaderboard table
class User(db.Model):
    __tablename__ = 'leaderboard'

    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(255), unique=True, nullable=False)
    _points = db.Column(db.Integer, default=0)  # Use _points as a private attribute

    def __init__(self, username, points=0):
        self.username = username
        self._points = points  # Initialize _points attribute

    @property
    def points(self):
        return self._points

    @points.setter
    def points(self, points):
        if points >= 0:
            self._points = points

    def create(self):
        """Create a new user entry in the leaderboard table."""
        try:
            db.session.add(self)
            db.session.commit()
            return self
        except IntegrityError:
            db.session.remove()
            return None

    def read(self):
        """Retrieve user information from the leaderboard table."""
        return {
            "id": self.id,
            "username": self.username,
            "points": self.points  # Use the property, not the private attribute
        }

    def update_points(self, points):
        """Update the points of a user in the leaderboard."""
        if points >= 0:
            self.points = points  # Use the property, not the private attribute
            db.session.commit()
            return self

    def delete(self):
        """Delete a user from the leaderboard."""
        db.session.delete(self)
        db.session.commit()
        return None

# Function to initialize the leaderboard table with sample data
def initLeaderboard():
    with app.app_context():
        # create the database and the leaderboard table
        db.create_all()
        
        users_data = [
            {"username": "user1", "points": 100},
            {"username": "user2", "points": 150},
            {"username": "user3", "points": 50},
            # Add some more users later for now it's just testing
        ]

        for data in users_data:
            user = User(username=data["username"], points=data["points"])
            user.create()

# Run the initialization function to create and populate the leaderboard
if __name__ == "__main__":
    initLeaderboard()
```

# Frontend
## Getting pull requests through javascript in our HTML map_game file HTML

- We can call upon our API endpoint and make a get response through the use of the fetch function in the HTTP get request. Afterwards once we make a request to the API url which is the /api/locations we can store the response data as JSON data which we can then access and store as a dictionary with callable objects to acess our data. Below is an example of how we can store the initial data as just call from our endpoint and format it in JSON and then eventually store it as a dictionary.
- [Fetch Commit](https://github.com/rliao569/Frontend-CSP/commit/30a4e5f63edf371b0d21845dcb034bd2994672b7)

## Dictionaries
- Learning dictionaries for our program was really useful and i



```python
        let coordinatesData = {}; // Store the coordinates and images
        let dictCoordinates = {}; // Global variable to store the organized data just fo rnow 
        let currentIndex = 0; // Initialize to 0
        let dotClicked = false; // Flag to check if the dot has been clicked

        function fetchAndDisplayImages() {
            // Defining our API endpoint
            const apiUrl = 'https://teaminfluencerinnovator.stu.nighthawkcodingsociety.com/api/locations/';

            // Make an HTTP GET request to the API
            fetch(apiUrl)
                .then(response => response.json()) // Parse the JSON response
                .then(data => {
                    // coordinatesData = data; // Store the data as it is
                    dictCoordinates = data;
                    // Call moveTarget immediately to position the dot at the first location
                    moveTarget();
                })
                .catch(error => {
                    console.error("Error fetching images:", error);
                });
        }

        fetchAndDisplayImages(); // Call fetchAndDisplayImages to initiate the process
```

- Now what this will look like is it will look like is 
- <img src="https://cdn.discordapp.com/attachments/1151587106322382948/1168413853730746410/image.png?ex=6551ad32&is=653f3832&hm=93b2073ed7bd1ac4098dd7241f08c5316897f1e8e83aac8e37c3fdd653a91b4b&">


```python

```

## Looping through the data and then incorporating it into the game 

- Once we have all that data we need to know how to incorporate it into the game, we need to implement indexing to acess those specific datapoints. Afterwards, already implemented in the moveTarget data, we can supply the coordinates for the target to move. Again, the target only moves based on DOM click event listeners highlighted in an earlier blog so the only time we want to move onto the next datapoint in the dictionary's ID is after a click has been performed.
- Below is an example of when the target is moved after a click is performed and displaying the image at that specific coordinate and adding it to a container as base64 jpg file 
- Specific commits: [Coordinates Commit](https://github.com/rliao569/Frontend-CSP/commit/0ee5667e88d4e7f08970313402d98d0a33249999) + [Image Commit](https://github.com/rliao569/Frontend-CSP/commit/46e891af13ab6d63428e9e44bfc4ea93aded6610)


## Use of DOM for event listener objects
- DOM for objects utilized on event listener clicks, showing growth and learning from the Web Programming Basics test and lessons on DOM

## HTMl elements
- Image tags and element use with the imager container 



### Example on click on the WEB programming test


```python
%%html
<!-- the ID must be specified on the elements -->
<button id="buttonID">Click here!</button>

<div id="divContainerIDbutton">
    <h1 id="h1ElementIDbutton">My Title</h1>
</div>

<!-- our javascript goe here -->
<script>
    // define a function => takes parameter text, returns a new p tab
    function createPTag(text) {
        // creates a new element
        var pElement = document.createElement("p")

        // using the parameter like a variable
        pElement.innerHTML = text
        
        // outputs p tag after it has been created
        console.log("Example #7.1, add p tag using a function")
        console.log(pElement)

        return pElement;
    }

    // create a function that sets specific text and adds to div
    function addPTagOnButton() {
        // using our new function
        var pTag = createPTag("Starting a paragraph with text created on button press.")

        // place the p element in the webpage
        var div = document.getElementById("divContainerIDbutton")

        // add p tag to the div
        div.appendChild(pTag)
        
        // outputs p tag after it has been created
        console.log("Example #7.2, update container adding a 'p' tag")
        console.log(div)
    }

    // add the P tag when our button is clicked
    var myButton = document.getElementById("buttonID")
    myButton.onclick = addPTagOnButton
    
</script>
```

### On click DOM, HTML element in our code


```python
function moveTarget() {
    const keys = Object.keys(dictCoordinates);
    if (currentIndex >= 0 && currentIndex < keys.length) {
        const key = keys[currentIndex];
        const value = dictCoordinates[key];
        const location_name = value.location_name;
        const coordinatesParsed = location_name.split(",");
        const x = parseInt(coordinatesParsed[0], 10);
        const y = parseInt(coordinatesParsed[1], 10);
        const imageSrc = `data:image/jpg;base64, ${value.image}`;

        const maxX = gameContainer.clientWidth - target.clientWidth;
        const maxY = gameContainer.clientHeight - target.clientHeight;

        target.style.left = Math.min(x, maxX) + "px";
        target.style.top = Math.min(y, maxY) + "px"; 

        // Get the image container by ID
        const imageContainer = document.getElementById("image-container");

        // Create a new image element
        const image = document.createElement("img");
        image.src = imageSrc;

        // Clear the existing content of the image container
        imageContainer.innerHTML = '';

        // Append the new image to the image container
        imageContainer.appendChild(image);
    } else {
        // If there are no more locations, stop moving the target
        target.style.display = 'none';
    }
}


gameContainer.addEventListener("click", () => {
    if (!dotClicked) {
        currentIndex++; // Move to the next location when there's no click
        moveTarget();
    }
    dotClicked = false;
});

target.addEventListener("click", (event) => {
    const earnedPoints = 1; // You always get 1 point for clicking on the dot
    score += earnedPoints;
    scoreDisplay.textContent = `Score: ${score}`;
    alert(`You got ${earnedPoints} point!`); // Display a pop-up message
    currentIndex++; // Move to the next location when the dot is clicked
    moveTarget();
    dotClicked = true; // Set the flag to true
});

```


```python
#image-container img {
    position: fixed;
    top: 0;
    right: 0;
    padding: 20px;
    max-width: 30%;
}

<div id="image-container" class="w3-container" style="display: flex; flex-wrap: wrap;"></div>

const imageSrc = `data:image/jpg;base64, ${value.image}`;

// Get the image container by ID
const imageContainer = document.getElementById("image-container");

// Create a new image element
const image = document.createElement("img");
image.src = imageSrc;
```

### AWS deployment fixes

- Learning how to fix the AWS instance especially when the server is down through the SSH instance
<img src="https://media.discordapp.net/attachments/932459151127355403/1169512175736471552/image.png?ex=6555ac17&is=65433717&hm=844bc0ade03e2400f6bf2c4fe1e0902bd82ae001e322e0d057eb9cafa8bc1877&=&width=1036&height=671">
<img src="https://cdn.discordapp.com/attachments/932459151127355403/1169512371396546603/image.png?ex=6555ac45&is=65433745&hm=8415bf6b10003cc9fdf7569b27defda1376e56dbe142abfdea6420793e84dc8e&">


### Reflection
- **Collaboration**: For presenting i need to improve on implementing on how to go from easier to harder in order to ease in the way that I present. I also think slowing down and preparing exactly what I'm going to say is really important for what I'm going to do this trimester. This can be evident throughout the team teach and thinking about how I can present and talking with Mr Mortensen was really helpful for how I could learn about different items.
- **Review**: The usefulness of talking and reflecting after events especially witih Mr Mortensen
- **Project**: I think that collaboration on the backend was extremely well. The cohesiosn and the adhesion within the backend and the frontend integration which was really hard and lacking, I needed to incorporate and consider other people's thoughts and teaching others. I'm really disappointed in how I collaborated this trimester, and honestly I was not a good collaborator and team member. I should've taken the time to explain to my other teammates in the frontend to talk about how I did. 
- **Perspective**: In general, I think that I could improve on the vision of our project. A "passion" project should be something I extend on other then just night at the museum. In a real world, I should make the project extensible and make it more playable then just one time.
- 
