---
toc: True
comments: True
layout: post
title: Student Lesson Python Libraries
description: To teach the class how to use public Python libraries around the internet
type: hacks
courses: {'compsci': {'week': 10}}
---

### What is a Library?
Essentially a list of pre-written code that you can use to streamline and clean up your program.

Libraries can help simplify complex programs

APIS are specifications for how the procedures in a library behave, and how they can be used 

Documentations for an API/library is necessary in understanding the behaviors provided by the API/library and how to use them

Libraries that we will go over: Requests, Pillow, Pandas, Numpy, Scikit-Learn, TensorFlow, matplotlib.


### Required Installations
Please run the following commands in your vscode terminal in order to continue the lesson
- pip install numpy
- pip install matplotlib
- pip install scikit-learn
- pip install pillow
- pip install pandas
- pip install tensorflow
- pip install requests


```python
import sys
!{sys.executable} -m pip install pandas
!{sys.executable} -m pip install matplotlib
```

    Collecting pandas
      Obtaining dependency information for pandas from https://files.pythonhosted.org/packages/db/3e/db3e98911b5da217d1e3f85b6e091448cb8f8be674bdaff3c0ec0dd855e0/pandas-2.1.2-cp311-cp311-win_amd64.whl.metadata
      Downloading pandas-2.1.2-cp311-cp311-win_amd64.whl.metadata (18 kB)
    Requirement already satisfied: numpy<2,>=1.23.2 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from pandas) (1.26.1)
    Requirement already satisfied: python-dateutil>=2.8.2 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from pandas) (2.8.2)
    Collecting pytz>=2020.1 (from pandas)
      Obtaining dependency information for pytz>=2020.1 from https://files.pythonhosted.org/packages/32/4d/aaf7eff5deb402fd9a24a1449a8119f00d74ae9c2efa79f8ef9994261fc2/pytz-2023.3.post1-py2.py3-none-any.whl.metadata
      Downloading pytz-2023.3.post1-py2.py3-none-any.whl.metadata (22 kB)
    Collecting tzdata>=2022.1 (from pandas)
      Downloading tzdata-2023.3-py2.py3-none-any.whl (341 kB)
         ---------------------------------------- 0.0/341.8 kB ? eta -:--:--
         -------- ------------------------------ 71.7/341.8 kB 1.3 MB/s eta 0:00:01
         -------------------------------------  337.9/341.8 kB 3.5 MB/s eta 0:00:01
         -------------------------------------- 341.8/341.8 kB 3.6 MB/s eta 0:00:00
    Requirement already satisfied: six>=1.5 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from python-dateutil>=2.8.2->pandas) (1.16.0)
    Downloading pandas-2.1.2-cp311-cp311-win_amd64.whl (10.6 MB)
       ---------------------------------------- 0.0/10.6 MB ? eta -:--:--
       --- ------------------------------------ 0.8/10.6 MB 17.6 MB/s eta 0:00:01
       ----- ---------------------------------- 1.4/10.6 MB 14.4 MB/s eta 0:00:01
       ------- -------------------------------- 2.1/10.6 MB 18.8 MB/s eta 0:00:01
       --------- ------------------------------ 2.4/10.6 MB 12.8 MB/s eta 0:00:01
       ----------- ---------------------------- 3.1/10.6 MB 13.3 MB/s eta 0:00:01
       ------------- -------------------------- 3.6/10.6 MB 12.9 MB/s eta 0:00:01
       --------------- ------------------------ 4.2/10.6 MB 12.7 MB/s eta 0:00:01
       ------------------ --------------------- 5.0/10.6 MB 13.8 MB/s eta 0:00:01
       --------------------- ------------------ 5.8/10.6 MB 14.2 MB/s eta 0:00:01
       ------------------------- -------------- 6.7/10.6 MB 14.2 MB/s eta 0:00:01
       -------------------------- ------------- 6.9/10.6 MB 13.8 MB/s eta 0:00:01
       ------------------------------ --------- 8.1/10.6 MB 14.9 MB/s eta 0:00:01
       ---------------------------------- ----- 9.2/10.6 MB 15.5 MB/s eta 0:00:01
       -------------------------------------- - 10.3/10.6 MB 16.0 MB/s eta 0:00:01
       ---------------------------------------  10.6/10.6 MB 16.0 MB/s eta 0:00:01
       ---------------------------------------- 10.6/10.6 MB 15.2 MB/s eta 0:00:00
    Downloading pytz-2023.3.post1-py2.py3-none-any.whl (502 kB)
       ---------------------------------------- 0.0/502.5 kB ? eta -:--:--
       --------------------------------------- 502.5/502.5 kB 15.9 MB/s eta 0:00:00
    Installing collected packages: pytz, tzdata, pandas
    Successfully installed pandas-2.1.2 pytz-2023.3.post1 tzdata-2023.3


    
    [notice] A new release of pip is available: 23.2.1 -> 23.3.1
    [notice] To update, run: C:\Users\will\AppData\Local\Microsoft\WindowsApps\PythonSoftwareFoundation.Python.3.11_qbz5n2kfra8p0\python.exe -m pip install --upgrade pip


    Requirement already satisfied: matplotlib in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (3.8.0)
    Requirement already satisfied: contourpy>=1.0.1 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from matplotlib) (1.1.1)
    Requirement already satisfied: cycler>=0.10 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from matplotlib) (0.12.1)
    Requirement already satisfied: fonttools>=4.22.0 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from matplotlib) (4.43.1)
    Requirement already satisfied: kiwisolver>=1.0.1 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from matplotlib) (1.4.5)
    Requirement already satisfied: numpy<2,>=1.21 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from matplotlib) (1.26.1)
    Requirement already satisfied: packaging>=20.0 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from matplotlib) (23.2)
    Requirement already satisfied: pillow>=6.2.0 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from matplotlib) (10.1.0)
    Requirement already satisfied: pyparsing>=2.3.1 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from matplotlib) (3.1.1)
    Requirement already satisfied: python-dateutil>=2.7 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from matplotlib) (2.8.2)
    Requirement already satisfied: six>=1.5 in c:\users\will\appdata\local\packages\pythonsoftwarefoundation.python.3.11_qbz5n2kfra8p0\localcache\local-packages\python311\site-packages (from python-dateutil>=2.7->matplotlib) (1.16.0)


    
    [notice] A new release of pip is available: 23.2.1 -> 23.3.1
    [notice] To update, run: C:\Users\will\AppData\Local\Microsoft\WindowsApps\PythonSoftwareFoundation.Python.3.11_qbz5n2kfra8p0\python.exe -m pip install --upgrade pip


### Images using requests and pillow libraries
'Requests' is focused on handling HTTP requests and web data while 'Pillow' is designed for data manipulation and analysis
It's common to see them used together in data-related assignments where data is fetched by HTTP requests using Requests and then processed and analyzed with Pandas.

Here's an example:


```python
import requests
from PIL import Image
from io import BytesIO

# Step 1: Download an image using Requests
image_url = "https://example.com/path/to/your/image.jpg"  # Replace with the actual URL of the image you want to download
response = requests.get(image_url)

if response.status_code == 200:
    # Step 2: Process the downloaded image using Pillow
    image_data = BytesIO(response.content)  # Create an in-memory binary stream from the response content
    img = Image.open(image_data)  # Open the image using Pillow

    # Perform image processing tasks here, like resizing or applying filters
    img = img.resize((x, y))  # Resize the image and replace x,y with desired amounts

    # Step 3: Save the processed image using Pillow
    img.save("processed_image.jpg")  # Save the processed image to a file

    print("Image downloaded, processed, and saved.")
else:
    print(f"Failed to download image. Status code: {response.status_code}")

```

In this code, we use the Requests library to download an image from a URL and then if the download is successful the HTTP status code 200 will pop up, and from there we create an in-memory binary stream (BytesIO) from the response content. We then use the Pillow library to open the image, make any necessary changes, and save the processed image to a file.

Here's a step by step tutorial on how we wrote this code: 
1)We started by importing the necessary libraries, which were Requests, Pillow, and io.

2)Download the Image

3)Use the Requests library to send an HTTP GET request to the URL to download the image.
Check the response status code to make sure the download goes through(status code 200).

4)If the download is successful, create an in-memory binary stream (BytesIO) from the response content.
Process the Image:

5)Utilize the Pillow library to open the image from the binary stream.
Change photo to desired preference(ie: size)
Save the Processed Image:

6)Save the processed image to a file using Pillow. Choose a filename and file format for the saved image.




### Hack 1

Write a Python code that accomplishes the following tasks:

Downloads an image from a specified URL using the Requests library.
Processes the downloaded image (like resizing) using the Pillow library.
Save the processed image to a file.



```python
import requests
from PIL import Image
from io import BytesIO

# Step 1: Download a random image using Requests
image_url = "https://source.unsplash.com/random"  # Use a source that provides random images
response = requests.get(image_url)

if response.status_code == 200:
    # Step 2: Process the downloaded image using Pillow
    image_data = BytesIO(response.content)  # Create an in-memory binary stream from the response content
    img = Image.open(image_data)  # Open the image using Pillow

    # Perform image processing tasks here, like resizing or applying filters
    img = img.resize((200, 400))  # Resize the image and replace with desired dimensions

    img.save("processed_image.jpg")  # Save the processed image to a file

    print("Random image downloaded, processed, and saved.")
else:
    print(f"Failed to download image. Status code: {response.status_code}")
```

    Random image downloaded, processed, and saved.


### Math Operations With Python Libraries
Numpy(Numerical Python) is used for numerical and scientific computing. It provides tools for handling large sets of numbers, such as data tables and arrays. Numpy makes it easier and more efficient to do mathematical tasks. 

The Matplotlib library lets you create a visual representation of your data (graphs, charts, and etc.)

### Example Sine Graph
Uses numpy and matplotlib libaries


```python
import numpy as np
import matplotlib.pyplot as plt

# Generate sample data with NumPy
x = np.linspace(0, 2 * np.pi, 100) 
# Create an array of values from 0 to 2*pi
# 100 is included to have 100 points distributed between 0 and 2π to make graph smoother
y = np.sin(x)
# Compute the sine of each value

# Create a simple line plot using Matplotlib
plt.plot(x, y, label='Sine Function', color='blue', linestyle='-')  # Create the plot
plt.title('Sine Function')  # Set the title
plt.xlabel('x')  # Label for the x-axis
plt.ylabel('sin(x)')  # Label for the y-axis
plt.grid(True)  # Display a grid
plt.legend()  # Show the legend
plt.show()  # Display the plot

```


    
![png](output_11_0.png)
    


### Hack 2
Using the data from the numpy library, create a visual graph using different matplotlib functions.


```python
import numpy as np
import matplotlib.pyplot as plt

# Generate data for the line
x = np.linspace(0, 10, 50)  # Create an array of values from 0 to 10
y1 = 2 * x + 1  # Set of data points for the line

# Create and display a plot using Matplotlib
plt.plot(x, y1, label='Linear Graph', color='red', linestyle='-')  # Create the plot
plt.title('Line')  # Set the title
plt.xlabel('x')  # Label for the x-axis
plt.ylabel('2x + 1')  # Label for the y-axis
plt.grid(True)  # Display a grid
plt.legend()  # Show the legend
plt.show()  # Display the plot
```


    
![png](output_13_0.png)
    


Tensor Flow is used in deep learning and neural networks, while scikit-learn is used for typical machine learning tasks. When used together, they can tackle machine learning projects. In the code below, Tensor Flow is used for model creation and training. Scikit-learn is used for data-processing and model evaluation.

## Pip install tensorflow scikit-learn


```python
import numpy as np
import tensorflow as tf
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
from sklearn.preprocessing import StandardScaler
from tensorflow import keras
from tensorflow.keras import layers
# Generate synthetic data
np.random.seed(0)
X = np.random.rand(100, 1)  # Feature
y = 2 * X + 1 + 0.1 * np.random.randn(100, 1)  # Target variable with noise
# Split the data into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
# Standardize the features
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)
# Create a simple linear regression model using TensorFlow and Keras
model = keras.Sequential([
    layers.Input(shape=(1,)),
    layers.Dense(1)
])
# Compile the model
model.compile(optimizer='adam', loss='mean_squared_error')
# Train the model
model.fit(X_train, y_train, epochs=100, batch_size=32, verbose=2)
# Make predictions on the test set
y_pred = model.predict(X_test)
# Calculate the Mean Squared Error on the test set
mse = mean_squared_error(y_test, y_pred)
print(f"Mean Squared Error: {mse:.4f}")
```

    Epoch 1/100
    3/3 - 0s - loss: 4.8368 - 175ms/epoch - 58ms/step
    Epoch 2/100
    3/3 - 0s - loss: 4.8196 - 5ms/epoch - 2ms/step
    Epoch 3/100
    3/3 - 0s - loss: 4.8022 - 5ms/epoch - 2ms/step
    Epoch 4/100
    3/3 - 0s - loss: 4.7843 - 5ms/epoch - 2ms/step
    Epoch 5/100
    3/3 - 0s - loss: 4.7666 - 5ms/epoch - 2ms/step
    Epoch 6/100
    3/3 - 0s - loss: 4.7493 - 5ms/epoch - 2ms/step
    Epoch 7/100
    3/3 - 0s - loss: 4.7312 - 4ms/epoch - 1ms/step
    Epoch 8/100
    3/3 - 0s - loss: 4.7149 - 6ms/epoch - 2ms/step
    Epoch 9/100
    3/3 - 0s - loss: 4.6971 - 4ms/epoch - 1ms/step
    Epoch 10/100
    3/3 - 0s - loss: 4.6794 - 4ms/epoch - 1ms/step
    Epoch 11/100
    3/3 - 0s - loss: 4.6624 - 5ms/epoch - 2ms/step
    Epoch 12/100
    3/3 - 0s - loss: 4.6462 - 5ms/epoch - 2ms/step
    Epoch 13/100
    3/3 - 0s - loss: 4.6289 - 4ms/epoch - 1ms/step
    Epoch 14/100
    3/3 - 0s - loss: 4.6123 - 5ms/epoch - 2ms/step
    Epoch 15/100
    3/3 - 0s - loss: 4.5950 - 4ms/epoch - 1ms/step
    Epoch 16/100
    3/3 - 0s - loss: 4.5777 - 5ms/epoch - 2ms/step
    Epoch 17/100
    3/3 - 0s - loss: 4.5608 - 4ms/epoch - 1ms/step
    Epoch 18/100
    3/3 - 0s - loss: 4.5446 - 5ms/epoch - 2ms/step
    Epoch 19/100
    3/3 - 0s - loss: 4.5278 - 5ms/epoch - 2ms/step
    Epoch 20/100
    3/3 - 0s - loss: 4.5111 - 5ms/epoch - 2ms/step
    Epoch 21/100
    3/3 - 0s - loss: 4.4943 - 4ms/epoch - 1ms/step
    Epoch 22/100
    3/3 - 0s - loss: 4.4772 - 6ms/epoch - 2ms/step
    Epoch 23/100
    3/3 - 0s - loss: 4.4617 - 4ms/epoch - 1ms/step
    Epoch 24/100
    3/3 - 0s - loss: 4.4444 - 5ms/epoch - 2ms/step
    Epoch 25/100
    3/3 - 0s - loss: 4.4281 - 5ms/epoch - 2ms/step
    Epoch 26/100
    3/3 - 0s - loss: 4.4119 - 4ms/epoch - 1ms/step
    Epoch 27/100
    3/3 - 0s - loss: 4.3962 - 5ms/epoch - 2ms/step
    Epoch 28/100
    3/3 - 0s - loss: 4.3787 - 5ms/epoch - 2ms/step
    Epoch 29/100
    3/3 - 0s - loss: 4.3633 - 4ms/epoch - 1ms/step
    Epoch 30/100
    3/3 - 0s - loss: 4.3470 - 5ms/epoch - 2ms/step
    Epoch 31/100
    3/3 - 0s - loss: 4.3306 - 4ms/epoch - 1ms/step
    Epoch 32/100
    3/3 - 0s - loss: 4.3145 - 5ms/epoch - 2ms/step
    Epoch 33/100
    3/3 - 0s - loss: 4.2986 - 5ms/epoch - 2ms/step
    Epoch 34/100
    3/3 - 0s - loss: 4.2835 - 4ms/epoch - 1ms/step
    Epoch 35/100
    3/3 - 0s - loss: 4.2678 - 4ms/epoch - 1ms/step
    Epoch 36/100
    3/3 - 0s - loss: 4.2524 - 5ms/epoch - 2ms/step
    Epoch 37/100
    3/3 - 0s - loss: 4.2358 - 4ms/epoch - 1ms/step
    Epoch 38/100
    3/3 - 0s - loss: 4.2203 - 4ms/epoch - 1ms/step
    Epoch 39/100
    3/3 - 0s - loss: 4.2056 - 4ms/epoch - 1ms/step
    Epoch 40/100
    3/3 - 0s - loss: 4.1896 - 4ms/epoch - 1ms/step
    Epoch 41/100
    3/3 - 0s - loss: 4.1749 - 4ms/epoch - 1ms/step
    Epoch 42/100
    3/3 - 0s - loss: 4.1585 - 5ms/epoch - 2ms/step
    Epoch 43/100
    3/3 - 0s - loss: 4.1429 - 4ms/epoch - 1ms/step
    Epoch 44/100
    3/3 - 0s - loss: 4.1277 - 4ms/epoch - 1ms/step
    Epoch 45/100
    3/3 - 0s - loss: 4.1120 - 5ms/epoch - 2ms/step
    Epoch 46/100
    3/3 - 0s - loss: 4.0971 - 5ms/epoch - 2ms/step
    Epoch 47/100
    3/3 - 0s - loss: 4.0810 - 4ms/epoch - 1ms/step
    Epoch 48/100
    3/3 - 0s - loss: 4.0658 - 5ms/epoch - 2ms/step
    Epoch 49/100
    3/3 - 0s - loss: 4.0503 - 4ms/epoch - 1ms/step
    Epoch 50/100
    3/3 - 0s - loss: 4.0357 - 5ms/epoch - 2ms/step
    Epoch 51/100
    3/3 - 0s - loss: 4.0198 - 4ms/epoch - 1ms/step
    Epoch 52/100
    3/3 - 0s - loss: 4.0052 - 5ms/epoch - 2ms/step
    Epoch 53/100
    3/3 - 0s - loss: 3.9896 - 4ms/epoch - 1ms/step
    Epoch 54/100
    3/3 - 0s - loss: 3.9749 - 7ms/epoch - 2ms/step
    Epoch 55/100
    3/3 - 0s - loss: 3.9603 - 5ms/epoch - 2ms/step
    Epoch 56/100
    3/3 - 0s - loss: 3.9452 - 6ms/epoch - 2ms/step
    Epoch 57/100
    3/3 - 0s - loss: 3.9303 - 4ms/epoch - 1ms/step
    Epoch 58/100
    3/3 - 0s - loss: 3.9173 - 4ms/epoch - 1ms/step
    Epoch 59/100
    3/3 - 0s - loss: 3.9017 - 5ms/epoch - 2ms/step
    Epoch 60/100
    3/3 - 0s - loss: 3.8872 - 4ms/epoch - 1ms/step
    Epoch 61/100
    3/3 - 0s - loss: 3.8729 - 4ms/epoch - 1ms/step
    Epoch 62/100
    3/3 - 0s - loss: 3.8584 - 4ms/epoch - 1ms/step
    Epoch 63/100
    3/3 - 0s - loss: 3.8449 - 5ms/epoch - 2ms/step
    Epoch 64/100
    3/3 - 0s - loss: 3.8306 - 4ms/epoch - 1ms/step
    Epoch 65/100
    3/3 - 0s - loss: 3.8161 - 4ms/epoch - 1ms/step
    Epoch 66/100
    3/3 - 0s - loss: 3.8022 - 5ms/epoch - 2ms/step
    Epoch 67/100
    3/3 - 0s - loss: 3.7881 - 5ms/epoch - 2ms/step
    Epoch 68/100
    3/3 - 0s - loss: 3.7741 - 5ms/epoch - 2ms/step
    Epoch 69/100
    3/3 - 0s - loss: 3.7610 - 5ms/epoch - 2ms/step
    Epoch 70/100
    3/3 - 0s - loss: 3.7465 - 4ms/epoch - 1ms/step
    Epoch 71/100
    3/3 - 0s - loss: 3.7326 - 5ms/epoch - 2ms/step
    Epoch 72/100
    3/3 - 0s - loss: 3.7193 - 4ms/epoch - 1ms/step
    Epoch 73/100
    3/3 - 0s - loss: 3.7050 - 5ms/epoch - 2ms/step
    Epoch 74/100
    3/3 - 0s - loss: 3.6910 - 5ms/epoch - 2ms/step
    Epoch 75/100
    3/3 - 0s - loss: 3.6781 - 4ms/epoch - 1ms/step
    Epoch 76/100
    3/3 - 0s - loss: 3.6644 - 4ms/epoch - 1ms/step
    Epoch 77/100
    3/3 - 0s - loss: 3.6509 - 5ms/epoch - 2ms/step
    Epoch 78/100
    3/3 - 0s - loss: 3.6368 - 5ms/epoch - 2ms/step
    Epoch 79/100
    3/3 - 0s - loss: 3.6235 - 4ms/epoch - 1ms/step
    Epoch 80/100
    3/3 - 0s - loss: 3.6105 - 5ms/epoch - 2ms/step
    Epoch 81/100
    3/3 - 0s - loss: 3.5959 - 4ms/epoch - 1ms/step
    Epoch 82/100
    3/3 - 0s - loss: 3.5822 - 4ms/epoch - 1ms/step
    Epoch 83/100
    3/3 - 0s - loss: 3.5692 - 5ms/epoch - 2ms/step
    Epoch 84/100
    3/3 - 0s - loss: 3.5556 - 6ms/epoch - 2ms/step
    Epoch 85/100
    3/3 - 0s - loss: 3.5418 - 5ms/epoch - 2ms/step
    Epoch 86/100
    3/3 - 0s - loss: 3.5280 - 6ms/epoch - 2ms/step
    Epoch 87/100
    3/3 - 0s - loss: 3.5151 - 5ms/epoch - 2ms/step
    Epoch 88/100
    3/3 - 0s - loss: 3.5018 - 5ms/epoch - 2ms/step
    Epoch 89/100
    3/3 - 0s - loss: 3.4888 - 5ms/epoch - 2ms/step
    Epoch 90/100
    3/3 - 0s - loss: 3.4749 - 6ms/epoch - 2ms/step
    Epoch 91/100
    3/3 - 0s - loss: 3.4619 - 6ms/epoch - 2ms/step
    Epoch 92/100
    3/3 - 0s - loss: 3.4488 - 5ms/epoch - 2ms/step
    Epoch 93/100
    3/3 - 0s - loss: 3.4360 - 4ms/epoch - 1ms/step
    Epoch 94/100
    3/3 - 0s - loss: 3.4228 - 5ms/epoch - 2ms/step
    Epoch 95/100
    3/3 - 0s - loss: 3.4089 - 4ms/epoch - 1ms/step
    Epoch 96/100
    3/3 - 0s - loss: 3.3963 - 5ms/epoch - 2ms/step
    Epoch 97/100
    3/3 - 0s - loss: 3.3831 - 4ms/epoch - 1ms/step
    Epoch 98/100
    3/3 - 0s - loss: 3.3694 - 4ms/epoch - 1ms/step
    Epoch 99/100
    3/3 - 0s - loss: 3.3568 - 4ms/epoch - 1ms/step
    Epoch 100/100
    3/3 - 0s - loss: 3.3435 - 4ms/epoch - 1ms/step
    1/1 [==============================] - 0s 24ms/step
    Mean Squared Error: 3.7303


A decrease in loss and time metrics (ms/epoch and ms/step) shows the efficiency increases as the training epochs increases

## Hack
fill in the missing code to match the custom data set


```python
import numpy as np
import tensorflow as tf
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
from sklearn.preprocessing import StandardScaler
from tensorflow import keras
from tensorflow.keras import layers

# Generate a custom dataset
np.random.seed(0)
num_samples = 100
bedrooms = np.random.randint(1, 5, num_samples)
square_footage = np.random.randint(1000, 2500, num_samples)
house_prices = 100000 + 50000 * bedrooms + 100 * square_footage + 10000 * np.random.randn(num_samples)
X = np.column_stack((bedrooms, square_footage))
y = house_prices.reshape(-1, 1)

# Split the data into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Standardize the features
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

# Create a regression model using TensorFlow and Keras
model = keras.Sequential([
    layers.Input(shape=(2,)),  # Input shape adjusted to the number of features
    layers.Dense(64, activation='relu'),
    layers.Dense(1)  # Output layer for regression
])

# Compile the model for regression
model.compile(optimizer='adam', loss='mean_squared_error')

# Train the model
model.fit(X_train, y_train, epochs=100, batch_size=32, verbose=0)

# Make predictions on the test set
y_pred = model.predict(X_test)

# Calculate the Mean Squared Error on the test set
mse = mean_squared_error(y_test, y_pred)
print(f"Mean Squared Error on the test set: {mse:.2f}")
```

    1/1 [==============================] - 0s 43ms/step
    Mean Squared Error on the test set: 158474157368.09


## HOMEWORK 1

Create a GPA calculator using Pandas and Matplot libraries and make:
1) A dataframe
2) A specified dictionary
3) and a print function that outputs the final GPA

Extra points can be earned with creativity.


```python
# Import the Pandas library
import pandas as pd

# Import the Matplotlib library 
import matplotlib.pyplot as plt

# Create a dictionary 'data' containing course information
data = {
    'Course': ['Calc', 'CSP', 'World', 'Chem', 'Photography'],
    'Credits': [2, 4, 3, 2, 4],
    'Grade': ['F', 'A', 'F', 'F', 'F'],
}

# Create a Pandas DataFrame 'df' from the 'data' dictionary
df = pd.DataFrame(data)

# Create a dictionary 'grade_points' to map letter grades to grade points
grade_points = {
    'A': 4.0,
    'B': 3.0,
    'C': 2.0,
    'D': 1.0,
    'F': 0.0,
}

# Add a new column 'Grade Points' to the DataFrame 'df' based on the 'Grade' column
df['Grade Points'] = df['Grade'].map(grade_points)

# Calculate the total grade points by multiplying 'Grade Points' and 'Credits' columns and summing them
total_grade_points = (df['Grade Points'] * df['Credits']).sum()

# Calculate the total credits by summing the 'Credits' column
total_credits = df['Credits'].sum()

# Calculate the GPA by dividing the total grade points by the total credits
gpa = total_grade_points / total_credits

# Create a bar chart to visualize the 'Grade Points' for each course
plt.bar(df['Course'], df['Grade Points'])
plt.xlabel('Course')
plt.ylabel('Grade Points')
plt.title('Course Grade Points')

# Display the bar chart
plt.show()

def print_final_gpa(gpa):
    print(f'Your GPA is {gpa:.2f} this trimester')

print_final_gpa(gpa) # print
```


    
![png](output_21_0.png)
    


    Your GPA is 1.07 this trimester


## HOMEWORK 2

Import and use the "random" library to generate 50 different points from the range 0-100, then display the randomized data using a scatter plot.

Extra points can be earned with creativity.


```python
import random
import matplotlib.pyplot as plt

# Generate 50 random data points in the range of 0-100 for x and y coordinates
xCoords = [random.randint(0, 100) for _ in range(50)]
yCoords = [random.randint(0, 100) for _ in range(50)]

# Create a scatter plot
plt.scatter(xCoords, yCoords, c='b', marker='o')

# Add labels and a title to the plot
plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.title('Random Data Scatter Plot')


# Display the plot
plt.legend()
plt.grid(True)
plt.show()
```

    No artists with labels found to put in legend.  Note that artists whose label start with an underscore are ignored when legend() is called with no argument.



    
![png](output_23_1.png)
    

