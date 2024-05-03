---
comments: true
layout: post
title: Data Structures
description: My writeup for the data structures project (Enjoy!)
type: hacks
courses: {'csp': {'week': 30}}
---

# Collections

- ![image](https://i.ibb.co/C710qj1/image.png)
## Here we have the unique collection with the different columns such as:
- the name of the different videos
- description of the different videos
- views of each video
- the video name stored locally
- thumbnail image name of the video stored within the instances
- _videoID to correspond to each video
- userID to correspond who uploaded the video
- genre of the video for sorting

## Code to Initialize and Create Test Code Data:

- ![image](https://i.ibb.co/0hBVTQP/image.png)
- In this part we create the table with the initial test data of different videos and their features.
- ![image](https://i.ibb.co/VMzRmXr/image.png)
- Here's the creation of the different videos: we utilize the upload_folder which is in the (instance/volumes/uploads) to access the different pictures. After searching for an image in that directory it's converted to base64 and passed to the create method.
- ![image](https://i.ibb.co/BV0v6Nk/image.png)
- After decoding the base64 image that we passed into the create method, the new image file turns into it's name with ID+name, Then we commit the new image file changes into the database of the thumbnail column and the videoID as the ID.

# List and Dictionaries
- This section goes over Object Relational Mapping (ORM) and the creation of a video object instance from a class to the database

## Debugger 
- ![image](https://i.ibb.co/qg3MPYL/image.png)
- Here we have a list of videos seen as the video list with [vid1,vid2]
- Each video has a corresponding key value and a dictionary such as the description, name, thumbnail, userID

# API and JSON

## Get Request
- ![image](https://i.ibb.co/6FDscbP/image.png)
- ![image](https://i.ibb.co/kq3f8S6/image.png)
- ![image](https://i.ibb.co/Vm9bxvs/image.png)
- Here we query the video with the specific Video ID, when going to the corresponding integer in the URL (for example: backend/1 would corresponding to the video with ID 1)

## Post Request
- ![image](https://i.ibb.co/rsnVrRH/image.png)
- ![image](https://i.ibb.co/YZ1582B/image.png)
- Here we upload the video and if  the body of the response is JSON and convert all the metadata to the corresponding video object. Then we use the create method for the specific thumbnail image to the instance
- Otherwise if the response isn't JSON, so we know it's uploading the code saves it within the VIDEO directory in the backend and we record the Video User ID

### The validation above in the POST request is to make sure the JSON isn't mepty and is formatted properly

## Put Request
- ![image](https://i.ibb.co/vVsRSQv/image.png)
- ![image](https://i.ibb.co/t41wZZN/image.png)
- First it checks if the body is json, and it queries the video to the specific ID and we get the specific TYPE on the video. If the specific TYPE is registered as a 1 it's a like and if it's a 2 it's considered a dislike.
- We also do this with the views and we update it.
- ![image](https://i.ibb.co/Tg9jCr2/image.png)
- ![image](https://i.ibb.co/wwgFQ1h/image.png)
- The PUT request modifies the views, likes, and dislikes 


## Postman 
## The Following is when 200 and everythign works
- GET request based on the VIdeo ID for metadata
- ![image](https://i.ibb.co/kHkNzLp/image.png)
- GET request of the specific video once it searches through the Video ID and finds the corresponding name in the db
- ![image](https://i.ibb.co/FmJdZSx/image.png)
- POST request in Postman with the required fields filled out and uploading a video
- ![image](https://i.ibb.co/dkqXWt3/image.png)
- You can see the PUT request in Postman  with the corresponding VideoID to update the total amount of views.
- ![image](https://i.ibb.co/2nyYvwk/image.png)

## 400 errors
- Here are issues that happen the body is missing in the POST request
- ![image](https://i.ibb.co/tZFcg25/image.png)
- 404 error when you try and update a wrong user
- ![image](https://i.ibb.co/8gQKX7q/image.png)

# Frontend
## Responses
- GET request shows the JSON response (just getting the specific video querying by the VIDEO ID)
- ![image](https://i.ibb.co/GQFHNDW/image.png) 
- POST request shows the JSON response (uploading videos)
- ![image](https://i.ibb.co/QKF9kP8/image.png)
- PUT request shows the JSON response (liking the video)
- ![image](https://i.ibb.co/L5Hdtg0/image.png) 

## In the Chrome browser, show a demo (GET) of obtaining an Array of JSON objects that are formatted into the browsers screen.
- ![image](https://i.ibb.co/gWsc4JC/image.png)
- Here's a snippet of some code that fetches for the videos based on the corresponding category into a videos list.
- Then we format it into a whole grid by utilizing the rendervideos function. The function will loop through all the videos we just queried and assign a specific HREF link to the corresponding video with it's ID.  
- ![image](https://i.ibb.co/wRWBBwB/image.png)

## In the Chrome browser, show a demo (POST or UPDATE) gathering and sending input and receiving a response that show update. Repeat this demo showing both success and failure.
- Properly working POST request working (success)
- ![image](https://i.ibb.co/QKF9kP8/image.png)
- POST request failure, I uploaded a video file that was too large for the request to handle as an image
- ![image](https://i.ibb.co/58FHDnD/image.png)

## In the In JavaScript code, show and describe code that handles success. Describe how code shows success to the user in the Chrome Browser screen.
- Basically whenever you upload you are supposed to get a message on the screen that shows you success
- ![image](https://i.ibb.co/RptjKyL/image.png)
- ![image](https://i.ibb.co/2kPs8jv/image.png)
- Whenever you get an error you will get the same thing similarly but instead it shows you a failure message
- ![image](https://i.ibb.co/WtQDzfW/image.png)

# Optional/Extra, Algorithm Analysis
- My project Tips made a prediction on the total amount a person payed in terms of tips value. 

## Show algorithms and preparation of data for analysis. This includes cleaning, encoding, and one-hot encoding. (Preparation for prediction)
- ![image](https://i.ibb.co/HFgC2vW/image.png)
- Cleaning the data to be a binary matrix of 1's and 0's, on the other hand the One Hot Encoding here will change the days which is categorical data into a binary matrix of whether or not the day was attended for tipping customers (1's and 0's)

## Prediction
- ![image](https://i.ibb.co/BZPShdw/image.png)
- Here we simply run the prediction after training everything, which I will talk about below

## Linear Regression Algorithims
- ![image](https://i.ibb.co/Q65GCDf/image.png)
- We use Linear Regression here because the outcome variable which is the total amount of TIPs a person payed ia continous end value. In comparison, the Titanic which predicts categorical outcome variables such as the surviving or death probability would require Logistic Regression
- I trained the X to be the different features which could all be causations for the Y variable which is the actual total amount payed in tips


