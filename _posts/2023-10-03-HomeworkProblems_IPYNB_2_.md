---
toc: True
comments: False
layout: post
title: Homework problems Data Abstractions
type: hacks
courses: {'csp': {'week': 7}}
---

### Problem 1
- Two airplanes are in a race, your job is to make a plane name list, append the name value to the participents  then make a variable that pulls the distance covered for each plane. in the end, in the curly brackets print the name of the plane, add more variables with curly brackets. 


```python
# Define a list of airplane race participants
participants = [
    {"name": "Billium Bang", "plane": "Red Rocket", "distance_covered": 1200},
    {"name": "Bushawn Bal", "plane": "The Biggest Bird", "distance_covered": 1500}
]

planes = []

# Calculate the total distance covered by each pilot during the race
for participant in participants:
    name = participant["name"]
    plane = participant["plane"]
    distance_covered = participant["distance_covered"]
    
    # Append the name of the plane to the 'planes' list
    planes.append(plane)
    
    # Print information about each participant using f-strings
    print(f"{name} flew the '{plane}' and covered a distance of {distance_covered} miles.")

# Determine the winner
winner = max(participants, key=lambda x: x["distance_covered"])
print(f"The winner of the airplane race is {winner['name']} in the '{winner['plane']}' with a distance of {winner['distance_covered']} miles!")

# Additional information about the planes
print("Additional information about the planes:")
for plane in planes:
    print(f"The '{plane}' is an impressive aircraft.")

```

    Billium Bang flew the 'Red Rocket' and covered a distance of 1200 miles.
    Bushawn Bal flew the 'The Biggest Bird' and covered a distance of 1500 miles.
    The winner of the airplane race is Bushawn Bal in the 'The Biggest Bird' with a distance of 1500 miles!
    Additional information about the planes:
    The 'Red Rocket' is an impressive aircraft.
    The 'The Biggest Bird' is an impressive aircraft.


### Problem 2
- Add more participants , in the loop, add a tricks variable that gets data from participants list
    score = tricks * 10  # Each trick is worth 10 points
    add a score and add it to a score in the list ex list[score] = score


```python
# Define a list of dog show participants
participants = [
    {"name": "Fido", "breed": "Golden Retriever", "tricks": 4},
    {"name": "Doggo", "breed": "Labrador Retriever", "tricks": 7},
    # Add more dog participants here
    {"name": "Rex", "breed": "German Shepherd", "tricks": 5},
    {"name": "Buddy", "breed": "Poodle", "tricks": 6}
]

# Calculate the scores for each dog based on the number of tricks they can perform
for participant in participants:
    tricks = participant["tricks"]
    score = tricks * 10  # Each trick is worth 10 points
    participant["score"] = score  # Add the score to the participant dictionary

# Determine the winning dog
winner = max(participants, key=lambda x: x["score"])

# Display the dog show results
print("Dog Show Results:")
for participant in participants:
    print(f"{participant['name']} the {participant['breed']} scored {participant['score']} points!")

print(f"The winner of the dog show is {winner['name']} with {winner['score']} points!")

```

    Dog Show Results:
    Fido the Golden Retriever scored 40 points!
    Doggo the Labrador Retriever scored 70 points!
    Rex the German Shepherd scored 50 points!
    Buddy the Poodle scored 60 points!
    The winner of the dog show is Doggo with 70 points!


this problem, were making a bank account, you just have to know what to do to add all of the functions to change the variables


```python
# Define a class representing a Bank Account
class BankAccount:
    def __init__(self, account_holder, balance=0):
        self.account_holder = account_holder
        self.balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            print(f"Deposited ${amount}. New balance: ${self.balance}")
        else:
            print("Invalid deposit amount.")

    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            print(f"Withdrew ${amount}. New balance: ${self.balance}")
        else:
            print(f"Insufficient funds. Cannot withdraw ${amount}.")

    def get_balance(self):
        return self.balance

    def __str__(self):
        return f"Account Holder: {self.account_holder}, Balance: ${self.balance}"

# Create two bank accounts Alex with 1000$ initially, and Noah with 5$ initially:
alexAccount = BankAccount("Alex", 1000)
noahAccount = BankAccount("Noah", 5)

# Perform some transactions:
alexAccount.withdraw(alexAccount.get_balance())  # Withdraw all money of Alex
noahAccount.deposit(alexAccount.get_balance())    # Give it all to Noah
noahAccount.withdraw(noahAccount.get_balance())    # Noah withdraws all of his money

# Display account information
print("Alex Account:", alexAccount)
print("Noah Account:", noahAccount)

```

    Withdrew $1000. New balance: $0
    Invalid deposit amount.
    Withdrew $5. New balance: $0
    Alex Account: Account Holder: Alex, Balance: $0
    Noah Account: Account Holder: Noah, Balance: $0


### add more regions



```python
import random

# Define a list of regions, each represented as a dictionary
regions = [
    {
        "name": "Region A",
        "GDP_growth": random.uniform(0.5, 3.0),
        "unemployment_rate": random.uniform(3.0, 10.0),
        "investment_score": random.uniform(50, 100),
        "education_index": random.uniform(0.5, 1.0),
        "infrastructure_quality": random.uniform(3.0, 8.0)
    },
    {
        "name": "Region B",
        "GDP_growth": random.uniform(0.5, 3.0),
        "unemployment_rate": random.uniform(3.0, 10.0),
        "investment_score": random.uniform(50, 100),
        "education_index": random.uniform(0.5, 1.0),
        "infrastructure_quality": random.uniform(3.0, 8.0)
    },
    {
        "name": "Region C",
        "GDP_growth": random.uniform(0.5, 3.0),
        "unemployment_rate": random.uniform(3.0, 10.0),
        "investment_score": random.uniform(50, 100),
        "education_index": random.uniform(0.5, 1.0),
        "infrastructure_quality": random.uniform(3.0, 8.0)
    }
    # Add more regions here as needed
]

# Define weights for each economic indicator
weights = {
    "GDP_growth": 0.4,
    "unemployment_rate": -0.2,
    "investment_score": 0.3,
    "education_index": 0.1,
    "infrastructure_quality": 0.2
}

# Function to calculate a score for each region based on economic indicators and weights
def calculate_score(region):
    score = 0
    for indicator, weight in weights.items():
        score += region[indicator] * weight
    return score

# Find the region with the highest economic growth potential
best_region = max(regions, key=calculate_score)

# Display information about the winning region
print(f"The region with the highest economic growth potential is {best_region['name']}:")
print(f"- GDP Growth Rate: {best_region['GDP_growth']:.2f}%")
print(f"- Unemployment Rate: {best_region['unemployment_rate']:.2f}%")
print(f"- Investment Score: {best_region['investment_score']:.2f}")
print(f"- Education Index: {best_region['education_index']:.2f}")
print(f"- Infrastructure Quality: {best_region['infrastructure_quality']:.2f}")

```

### problem final

- make an empty list and dictionary
- add data in all of the given simple loops, so that this problem runs its print functions without error
- this one is hard, try very hard, a heartfelt atempt, like all of the code done with minor issues is still full credit

try to understand this problem, it has lots of data abstractions

data is given on the bottem and a function is calling it IMPORTANT!!!



```python
def simulate_data_structure(data):

    city_data = {}


    city_stats = {}

    for person in data:
        age = person["age"]
        name = person["name"]
        city = person["city"]

        if city not in city_data:
            city_data[city] = {"names": [], "total_age": 0, "total_people": 0}

        city_data[city]["names"].append(name) 
        city_data[city]["total_age"] += age 
        city_data[city]["total_people"] += 1  

    for city, city_info in city_data.items():
   
        average_age = city_info["total_age"] / city_info["total_people"]
        city_info["average_age"] = round(average_age, 2)  # Round to 2 decimal places

  
        city_stats[city] = {
            "total_people": city_info["total_people"],
            "average_age": city_info["average_age"]
        }

   
    city_data["Statistics"] = city_stats

    return city_data


data = [
    {"name": "Will", "age": 15, "city": "Cherry Hill"},
    {"name": "Saaras", "age": 14, "city": "San Diego"},
    {"name": "Andrew", "age": 15, "city": "San Diego"},
    {"name": "David", "age": 16, "city": "San Diego"},
    {"name": "Ryan", "age": 16, "city": "San Diego"},
]

result = simulate_data_structure(data)
print(result)

```

    {'New York': {'names': ['Alice', 'Charlie'], 'total_age': 47, 'total_people': 2, 'average_age': 23.5}, 'Los Angeles': {'names': ['Bob', 'David'], 'total_age': 65, 'total_people': 2, 'average_age': 32.5}, 'Chicago': {'names': ['Eve'], 'total_age': 28, 'total_people': 1, 'average_age': 28.0}, 'Statistics': {'New York': {'total_people': 2, 'average_age': 23.5}, 'Los Angeles': {'total_people': 2, 'average_age': 32.5}, 'Chicago': {'total_people': 1, 'average_age': 28.0}}}



```python
ingredients = ["butter", "white sugar", "light brown sugar", "vanilla extract", "eggs", "flour", "chocolate chips", "baking soda", "salt", "baking powder"]
# Print this list

# << CODE >>


# Create a list called bowl
# Your list must include:
# "flour"
# "baking soda"
# "salt"
# "baking powder"
# When creating this list, make sure to remove these items from the "ingredients" list!
# Print your list

# << CODE >>

# Create a list called cream
# Include:
# "butter"
# "white sugar"
# "light brown sugar"
# "vanilla extract"
# "eggs"
# When creating this list, make sure to remove these items from the "ingredients" list!
# Print your list

# << CODE >>

# Create a list called "dough"
# Combine the bowl list and cream list together
# Print your list

# << CODE >>

# Append chocolate chips to the dough list and remove it from the ingredients list
# Print the list

# << CODE >>

# Create a string that says "Now roll the dough into balls and place them on cookie sheets!"
# Print it

# << CODE >>

# Create an int called temperature and set it to 375
# Print "Place in a <<your integer goes here>> F oven for 8-10 minutes and remove just before they start to turn brown."

# << CODE >>

# Create an int called "cool down" using pascal case and set it to 2
# Print "Let them sit on the baking pan for <<your integer goes here>> minutes before removing to cooling rack."

# << CODE >>

# Create 5 string (use whatever casing you feel)
# First string should be "Enjoy"
# Second string should be "your"
# Third string should be "CHOCOLATE"
# Fourth string should be "CHIP"
# Fifth string should be "COOKIES!!!"
# Using ONE print statement, print ALL of these variables (with a space between each)

# << CODE >>

# JSON CHALLENGE
# can your do the whole project by using a JSON list?
# can you convert it to a python dictionary and do all these steps?

# Yes this is a real cookie recipe. You can find it below if you wanna make them! :)
# https://joyfoodsunshine.com/the-most-amazing-chocolate-chip-cookies/
# List of ingredients
ingredients = ["butter", "white sugar", "light brown sugar", "vanilla extract", "eggs", "flour", "chocolate chips", "baking soda", "salt", "baking powder"]

# Print the list of ingredients
print(ingredients)

# Create a list called "bowl" and remove the specified items from the "ingredients" list
bowl = ["flour", "baking soda", "salt", "baking powder"]
for item in bowl:
    ingredients.remove(item)

# Print the "bowl" list
print(bowl)

# Create a list called "cream" and remove the specified items from the "ingredients" list
cream = ["butter", "white sugar", "light brown sugar", "vanilla extract", "eggs"]
for item in cream:
    ingredients.remove(item)

# Print the "cream" list
print(cream)

# Create a list called "dough" by combining "bowl" and "cream"
dough = bowl + cream

# Print the "dough" list
print(dough)

# Append "chocolate chips" to the "dough" list and remove it from the "ingredients" list
dough.append("chocolate chips")
ingredients.remove("chocolate chips")

# Print the updated "dough" list
print(dough)

# Create a string for rolling the dough into balls
rolling_instructions = "Now roll the dough into balls and place them on cookie sheets!"

# Print the rolling instructions
print(rolling_instructions)

# Create an integer for the oven temperature
temperature = 375

# Print the baking instructions with the temperature variable
print(f"Place in a {temperature} F oven for 8-10 minutes and remove just before they start to turn brown.")

# Create an integer for the cool-down time
cool_down = 2

# Print the cool-down instructions with the cool_down variable
print(f"Let them sit on the baking pan for {cool_down} minutes before removing to a cooling rack.")

# Create strings for enjoyment
enjoy1 = "Enjoy"
enjoy2 = "your"
enjoy3 = "CHOCOLATE"
enjoy4 = "CHIP"
enjoy5 = "COOKIES!!!"

# Use one print statement to print all enjoyment strings with spaces in between
print(enjoy1, enjoy2, enjoy3, enjoy4, enjoy5)

# JSON Challenge: You can convert the list of ingredients to a JSON list, then parse it back to a Python list.
import json

# List of ingredients
ingredients = ["butter", "white sugar", "light brown sugar", "vanilla extract", "eggs", "flour", "chocolate chips", "baking soda", "salt", "baking powder"]

# Print the list of ingredients

# Convert the ingredients list to a JSON string
ingredients_json = json.dumps(ingredients)

# Print the JSON string representing the ingredients
print(ingredients_json)

# Parse the JSON string back to a Python list
ingredients_list = json.loads(ingredients_json)



```

    ['butter', 'white sugar', 'light brown sugar', 'vanilla extract', 'eggs', 'flour', 'chocolate chips', 'baking soda', 'salt', 'baking powder']
    ['flour', 'baking soda', 'salt', 'baking powder']
    ['butter', 'white sugar', 'light brown sugar', 'vanilla extract', 'eggs']
    ['flour', 'baking soda', 'salt', 'baking powder', 'butter', 'white sugar', 'light brown sugar', 'vanilla extract', 'eggs']
    ['flour', 'baking soda', 'salt', 'baking powder', 'butter', 'white sugar', 'light brown sugar', 'vanilla extract', 'eggs', 'chocolate chips']
    Now roll the dough into balls and place them on cookie sheets!
    Place in a 375 F oven for 8-10 minutes and remove just before they start to turn brown.
    Let them sit on the baking pan for 2 minutes before removing to a cooling rack.
    Enjoy your CHOCOLATE CHIP COOKIES!!!
    ["butter", "white sugar", "light brown sugar", "vanilla extract", "eggs", "flour", "chocolate chips", "baking soda", "salt", "baking powder"]

