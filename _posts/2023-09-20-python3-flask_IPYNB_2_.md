---
title: Python flask backend
toc: True
description: Flask backend
courses: {'csp': {'week': 5}}
type: hacks
---

```python
%%python --bg

from flask import Flask, jsonify
from flask_cors import CORS

# initialize a flask application (app)
app = Flask(__name__)
CORS(app, supports_credentials=True, origins='*')  # Allow all origins (*)

# ... your existing Flask

# add an api endpoint to flask app
@app.route('/api/data')
def get_data():
    # start a list, to be used like a information database
    InfoDb = []

    # add a row to list, an Info record
    InfoDb.append({
        "FirstName": "Will",
        "LastName": "Cheng",
        "DOB": "Novemeber 27",
        "Residence": "San Diego",
        "Email": "funnykidland@gmail.com",
        "Cats": ["siberian", "persian", "bengal", "maine-coon", "sphynx"]
    })

    # add a row to list, an Info record
    InfoDb.append({
        "FirstName": "Saaras",
        "LastName": "Kodali",
        "DOB": "October 1",
        "Residence": "San Diego",
        "Email": "kodalisaaras@gmail.com",
        "Games": ["League of Legends", "Genshin Impact", "Valorant"]
    })
    
    InfoDb.append({
        "FirstName": "Andrew",
        "LastName": "Kim",
        "DOB": "Novemeber 26",
        "Residence": "San Diego",
        "Email": "andrew.kim328@gmail.com",
        "Music": ["Ghibli", "Nukes", "Nirvana"]
    })
    
    return jsonify(InfoDb)

# add an HTML endpoint to flask app
@app.route('/')
def say_hello():
    html_content = """
    <html>
    <head>
        <title>Team Influencer Innovator's Blog</title>
    </head>
    <body>
        <h2>Hi everyone! We are Team Influence and Innovators, our teams consist of Will Cheng, Saaras Kodali, Daniel Lee, Andrew Kim, and Ryan Liao!</h2>
    </body>
    </html>
    """
    return html_content

if __name__ == '__main__':
    # starts flask server on default port, http://127.0.0.1:5001
    app.run(port=5001)
```


```python
%%script bash

# After app.run(), see the the Python process
lsof -i :5001
# see the the Python app
lsof -i :5001 | awk '/Python/ {print $2}' | xargs ps

```

    your 131072x1 screen size is bogus. expect trouble


      PID TTY          TIME CMD
      443 pts/2    00:00:00 bash
      450 pts/2    00:00:00 xargs
      451 pts/2    00:00:00 ps



```python
import requests
res = requests.get('http://127.0.0.1:5001/api/data')
res.json()
```




    [{'Cats': ['siberian', 'persian', 'bengal', 'maine-coon', 'sphynx'],
      'DOB': 'Novemeber 27',
      'Email': 'funnykidland@gmail.com',
      'FirstName': 'Will',
      'LastName': 'Cheng',
      'Residence': 'San Diego'},
     {'DOB': 'October 1',
      'Email': 'kodalisaaras@gmail.com',
      'FirstName': 'Saaras',
      'Games': ['League of Legends', 'Genshin Impact', 'Valorant'],
      'LastName': 'Kodali',
      'Residence': 'San Diego'},
     {'DOB': 'Novemeber 26',
      'Email': 'andrew.kim328@gmail.com',
      'FirstName': 'Andrew',
      'LastName': 'Kim',
      'Music': ['Ghibli', 'Nukes', 'Nirvana'],
      'Residence': 'San Diego'}]


