---
layout: post
title: Developing Procedures
description: College Board 3.12 and 3.13
toc: True
comments: True
type: hacks
courses: {'csp': {'week': 10}}
---

## What is a procedure?
A procedure is a named group of programming instructions with a purpose and is called to perform a task based on the commands. 


It is extremely important to name the procedure something that describes the purpose, method, or function because it makes it easier for others to read your code and for yourself when you revisit old code. Additionally, when there is an effefctively named procedure, it is much simpler to correct bugs and errors.

### Which code is better?
<img src="https://media.discordapp.net//attachments/909575347773775953/1166199627083698217/namingprocedures.png?ex=65499f0a&is=65372a0a&hm=6a7d0bf546b51e54837e3cd8d5993063d9ab28ac4f19bd6e49b6a540424a30a5&">

### Hack 1: Naming Procedures
Rename the procedure below with a name that better describes the purpose of the procedure. 

The procedure is currently just called "procedure." It compares the current grade with the existing quiz grade and replaces the original score if the current is higher.


```python
def grade_comparer(quiz_grade, current_points, total_points):
    # calculate current grade
    current_grade = (current_points / total_points) * 100

    if current_grade > quiz_grade:
        quiz_grade = current_grade

    return quiz_grade

quiz_grade = 85  # Initial quiz grade
current_points = 90  # Current points earned
total_points = 100  # Total points for the quiz

new_quiz_grade = grade_comparer(quiz_grade, current_points, total_points)

print(f"Old quiz grade: {quiz_grade}")
print(f"New quiz grade: {new_quiz_grade}")

```

    Old quiz grade: 85
    New quiz grade: 90.0


## Function Parameters
A function can have one or more parameters that can be passed into the function as local variables to use in the procedural function. The variables that can be passed in the function are called parameters. The data passed in when the function is called are called arguments.


Parameters: input values of a procedure


Arguments: specify the parameter values when a procedure is called


```python
def triangle_area(length, width): # parameters passed in two variables: length and width, returns area
    area = 1/2 * length * width # calculates area from the length and width
    print("length:", length)
    print("width:", width)
    return area # returns area

# examples
print(triangle_area(3, 4)) # the arguments here are 3 and 4, which becomes the parameters length and width respectively
print(triangle_area(6, 8))
print(triangle_area(12, 89))
```

    length: 3
    width: 4
    6.0
    length: 6
    width: 8
    24.0
    length: 12
    width: 89
    534.0


## Procedure Algorithm / How Procedures Work
Remember that procedures are essentially a set of programming instructions, or lines of code, that accomplish a goal. When executed, each line of code is executed in order (step after step after step) to get to the goal.

### Regular code/Python


```python
# Procedure called "applyTax" that applies a percent tax to a price
def applyTax(price, percentTax): # When writing a procedure, first decide what parameters you will need to accomplish your goal
    # Step 1: Calculate the amount taxed
    taxAmount = price * percentTax/100

    # Step 2: Add the amount taxed to the price to get the end amount
    endAmount = price + taxAmount

    return endAmount

# Use procedure to apply a 50% tax to a price of $10
cost = applyTax(10, 50)
print(cost)
```

    15.0


### CollegeBoard Pseudo-Code
- Note that the pseudo-code below has the exact same purpose as the actual code above. Ignore the breaks and spaces since they are used for formatting.
> Differences between prseudo-code and Python:
- Pseudo-code uses "PROCEDURE" instead of "def"
- Pseudo-code uses "<--" instead of "="
- Pseudo-code uses "{}" instead of ":" to mark where a procedure starts and ends
<br>

> Pseudo-code example <br>

PROCEDURE applyTax (price, percentTax) <br>
{ <br>
&nbsp;&nbsp;&nbsp;&nbsp;taxAmount <-- price * percentTax/100 <br>
&nbsp;&nbsp;&nbsp;&nbsp;endAmount <-- price + taxAmount <br>
&nbsp;&nbsp;&nbsp;&nbsp;return endAmount <br>
}

### Hack 2: Robot Pseudo-Code
<img src="https://media.discordapp.net/attachments/1143438030749847604/1165903186473783317/image.png?ex=65488af5&is=653615f5&hm=349a4cfef60546b6f85e59a2448ac85ed4fd0181d63f70456904909e46401d74&=">

> Instructions:
- The blue triangle represents a robot that moves in a grid of squares. The tip of the triangle indicates where the robot is facing.
- Write a procedure that allows the robot to make a detour around a block by moving to the left.

> Commands
- MOVE_FORWARD() - Moves the robot forward one square
- MOVE_BACKWARD() - Moves the robot backward one square
- ROTATE_LEFT() - Rotates the robot 90 degrees left
- ROTATE_RIGHT() - Rotates the robot 90 degrees right

> Your code here:



PROCEDURE RobotDetour <br>
{ <br>
&nbsp;&nbsp;&nbsp;&nbsp;ROTATE_LEFT() <br>
&nbsp;&nbsp;&nbsp;&nbsp;MOVE_FORWAWRD() <br>
&nbsp;&nbsp;&nbsp;&nbsp;ROTATE_RIGHT() <br>
&nbsp;&nbsp;&nbsp;&nbsp;MOVE_FORWARD() <br>
&nbsp;&nbsp;&nbsp;&nbsp;MOVE_FORWARD() <br>
&nbsp;&nbsp;&nbsp;&nbsp;ROTATE_RIGHT() <br>
&nbsp;&nbsp;&nbsp;&nbsp;MOVE_FORWARD() <br>
}

## Procedure Return Values
When a procedure is run, it executes a series of calculations or commands and at some point and needs to provide a useful result. The return statement is what allows us to return a useful value back to the calling code. The returns statement can return various types of values such as booleans, integers, strings, etc.

## Procedure Calls
Calling: This involves specifying the function name followed by parentheses, and passing any required arguments inside the parentheses.


When a function is called, the program control jumps to the function definition, and the statements inside the function are executed.
After the function completes its task, the control returns to the point where the function was called.

### Hack 3: Create and Call a Procedure
Define a function named calculate_grade that takes a student's score as a parameter and returns 'Pass' if the score is 50 or more, and 'Fail' otherwise.


```python
def calculate_grade(score):

    if score >= 50:
        return "Pass"
    else:
        return "Fail"
    
    
print(calculate_grade(51))
```

    Pass


# Homework
## Instructions
There are two total problems:
1.  An easy regular code (Python) problem
2.  A medium pseudo-code problem
3. A hard regular code (Python) problem


Completing question 1 and 2 gets you 0.9/1 if you do it correctly. Completing/attempting question 3, adding creativity, and adding good comments will potentially raise you above 0.9.

### Question 1
Write a procedure to apply a percent discount to a set price. See the example about applying tax if you're stuck.


```python
def PercentDiscount(percent, original):
    '''

    HOW IT WORKS:

    Ok so to calculate percent discount you find what percentage 
    you are disccounting of the original price and then subtract it from the original price 
    so here we first pass in two parameters: percent we are discounting and the original price
    I find the discount and then subtract this from original price then print end price yay
    
    '''
    end_price = original - ((percent / 100) * original )
    return(end_price)

print(PercentDiscount(15, 20))
```

    17.0


### Question 2
Create your own robot problem! Include a picture with a square grid to represent the map and triangle to represent the robot. Add a flag to a square to represent the end-point and a shaded-in block to represent a detour. Write a procedure in pseudo-code to move the robot from the start, past the detour, and to the end point.

Add your image here by adding the link between the "" and removing the comment formatting:
### Robot problem
<img src="https://media.discordapp.net/attachments/975585693751455764/1167148404724469770/grid_a.png?ex=654d12a8&is=653a9da8&hm=880c8e446a5dabfc3da25dde181d44b3a2b8180c7557a8fe481da99acf425fd9&=">



```python


PROCEDURE manueverGrid{
    # Using iteration, the triangle will move forward two times
    REPEAT 2 TIMES {
        MOVE_FORWARD()
        # Move forward 2 times
    }

    # Rotate towards the right
    ROTATE_RIGHT()

    # Using iteration again we can move the triangle forward four times
    REPEAT 4 TIMES {
        MOVE_FORWARD()
    }

    # Rotate towards the right,
    ROTATE_RIGHT()

    # For two times move forward to get to the end location and spot
    REPEAT 2 TIMES {
        MOVE_FORWARD()
    }    

}
```


```python

```

### Question 3
Create a program that asks for user input of an integer *n*, and return an array that contains all the prime numbers up to the number *n* (inclusive). Remember to use multiple different functions to better organize the code and increase efficiency.


```python
def primes(n):
    # if the number is less then 2 then it is a prime number hehe ehehhehehehehehhehe

    if n < 2:
        return []
    else:
        # Create a boolean list to mark numbers as prime or not, so it'll be like [1, 1, 1, 1, 1, 1, 1, 1]
        is_prime = [True] * (n + 1)
        is_prime[0] = is_prime[1] = False  # 0 and 1 are not prime numbers, so you put them in the boolean list as [0, 0] 

        # Start with the first prime number, 2 because that is ia prime number
        for p in range(2, int(n**0.5) + 1):
            if is_prime[p]:  # Loop through the numbers that are above two and then find multiples
                # Mark all multiples of p as non-prime 
                for i in range(p * p, n + 1, p): 
                    is_prime[i] = False
    return is_prime
    

'''
ok so here we basically make a new final answer list and then we add it based on the index of the location_bool numbers and by looping through the index and based on the index
We get a number and then print out that list :))))
meow meow meow meow meow


'''
final_ans = []
number = int(input())
primeBools = primes(number)
for x in range(0, len(primeBools)):
    if primeBools[x] == True:
        final_ans.append(x)
print(final_ans)
```

    [2, 3, 5, 7]



```python

```
