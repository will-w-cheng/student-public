---
toc: True
comments: False
layout: post
title: Developing Algorithms
type: hacks
courses: {'csp': {'week': 9}}
---

## What are Algorithims?

Whats the difference between these two math problems:
(3+1)3 + 89 + 4(2+8)
3(1+3) + 8(1+4) + 89

Nothing! They are just two different ways of doing them!

Whats the difference between these two math problems:
3((9-6)+7) + 7 - (9+8)
3(9-(6+7)) + 7 - 9 + 8

A lot! This changes the output by quite a bit!

Here are examples of this basic concept in terms of programming:


```python
print("What is the temperature outside °F?")
temp = int(input())
if temp > 85:
    print("It is too hot outside!")
elif temp >= 65:
    print("Sure, I will play outside!")
else:
    print("It is too cold outside!")
```


```python
print("What is the temperature outside °F?")
temp = int(input())
if temp == 85:
    print("It is too hot outside!")
if temp == 65:
    print("Sure, I will play outside!")
if temp < 65:
    print("It is too cold outside!")
```

### Didn't get it?  
Hint: 
- What if I input 60 degrees °F?
- What if I input 90 degrees °F?


Hack #1: What is the difference between these two pieces of code? (in terms of their output)


```python
num = 1
while num <= 100:
    if num % 4 != 0:
        print(num, end=' ')
    num += 1
```

    1 2 3 5 6 7 9 10 11 13 14 15 17 18 19 21 22 23 25 26 27 29 30 31 33 34 35 37 38 39 41 42 43 45 46 47 49 50 51 53 54 55 57 58 59 61 62 63 65 66 67 69 70 71 73 74 75 77 78 79 81 82 83 85 86 87 89 90 91 93 94 95 97 98 99 


```python
def print_numbers():
    for i in range(1, 101):
        if i % 4 != 0:
            print(i)

print_numbers()
```

    1
    2
    3
    5
    6
    7
    9
    10
    11
    13
    14
    15
    17
    18
    19
    21
    22
    23
    25
    26
    27
    29
    30
    31
    33
    34
    35
    37
    38
    39
    41
    42
    43
    45
    46
    47
    49
    50
    51
    53
    54
    55
    57
    58
    59
    61
    62
    63
    65
    66
    67
    69
    70
    71
    73
    74
    75
    77
    78
    79
    81
    82
    83
    85
    86
    87
    89
    90
    91
    93
    94
    95
    97
    98
    99


So when developing algorithms, different pieces of code could do the same thing, and two similar pieces of code could do very different things. 

# Data Collections

### Purpose of Data Collection
To gather accurate and relevant information for specific purposes, such as solving problems, making informed decisions, or predicting future trends.

### Techniques
Surveys and Questionnaires: Structured methods for gathering data from a large number of respondents. They can be administered in-person, online, or through other mediums.

Observations: Watching and recording actions or behaviors in a systematic manner.

Experiments: Conducting controlled tests or trials to determine cause and effect relationships.

Simulations: Using models to imitate real-world situations.

Interviews: One-on-one or group discussions to gain in-depth insights.

Sensors and Automated Collection: Using electronic devices to automatically collect data, like temperature sensors or traffic cameras.

Sampling: Instead of studying an entire population, a subset (or sample) can be studied to make inferences about the entire group.

Techniques include random sampling, stratified sampling, and convenience sampling.

### Bias and Error
Data collection methods can introduce bias or error. It's crucial to be aware of potential sources of bias, like leading questions in surveys or non-random sampling methods.

### Privacy and Ethics
Always consider the ethical implications of data collection. Obtain consent when necessary, anonymize data to protect individuals' privacy, and be transparent about how data will be used.


Hack #2:


```python
def find_max(numbers):
    max_value = numbers[0]
    for number in numbers:
        if number > max_value:
            max_value = number
    return max_value
#List of numbers
numbers = [23, 45, 67, 89, 12, 34, 56, 78]

max_value = find_max(numbers)
print(max_value)

```

    89


List of numbers
numbers = [23, 45, 67, 89, 12, 34, 56, 78]

TODO: Modify the given algorithm to find the minimum value in the list of numbers.
Hint: You only need to change two lines of code.


```python
def find_min(numbers):
    min_val = numbers[0]
    for number in numbers:
        if number < min_val:
            min_val = number
    return min_val
#List of numbers
numbers = [23, 45, 67, 89, 12, 34, 56, 78]

min_val = find_min(numbers)
print(min_val)

```

    12


Solution:

Modified Algorithm to find the minimum value.


```python
def find_min(numbers):
    min_value = numbers[0]
    for number in numbers:
        if number < min_value:
            min_value = number
    return min_value

#alling the function
min_value = find_min(numbers)
print(min_value)  # Output: 12 
```

    12


# Creating/Modifying Algorithms

Important steps for creating an algorithm:
- Define functions
- Initialize ways to store data (array, lists, dictionaries, etc…)
- Depending on the context, use iteration to specify conditions for variable
- Output generated values from the algorithm

Helpful tips for modifying algorithms:
- Understand the algorithm so you're able to easily apply changes to it.
- Break the program down into chunks.
- Focus on each small part of the algorithm to get it to work.
- Make sure to test individual components, and then the whole code together (This makes identifying errors, and correcting mistakes easier).

Example (The sum of all even numbers between 1 and a given positive integer):



```python
def sum_of_evens(n):
    total = 0
    for i in range(2, n + 1, 2): #Note the 2 and the very end initializes a step size of 2 for the function
        total += i
    return total

n = int(input("Enter a positive integer: "))
result = sum_of_evens(n)
print(f"The sum of even numbers from 1 to {n} is {result}")
```

Hack #3:

TODO: Adapt the above algorithm to output for the sum of odd numbers between 1 and a given integer. 

Try to come up with a unique algorithm (way) to achieve the above task.


```python
def sum_of_evens(n):
    total = 0
    for i in range(1, n+1): #Note the 2 and the very end initializes a step size of 2 for the function
        if i % 2 != 0:
            total += i
    return total

n = int(input("Enter a positive integer: "))
result = sum_of_evens(n)
print(f"The sum of even numbers from 1 to {n} is {result}")
```

    The sum of even numbers from 1 to 5 is 4


Solution:

Think about how you would define an odd number, and output the sum of each element.


```python
def sum_of_odd_numbers(n):
    total = 0

    for i in range(1, n + 1):
        if i % 2 != 0:  # Check if the number is odd
            total += i

    return total

n = int(input("Enter a value for n: "))
result = sum_of_odd_numbers(n)
print(f"The sum of odd numbers from 1 to {n} is: {result}")
```

    The sum of odd numbers from 1 to 6 is: 9


# Random Number Generation

RANDOM (a, b) generates a number from a to b inclusive.
Each result from the randomization is equally likely to occur.
Using random number generation in a program means each execution may produce a different result.
We can use the results from randomization to program simulations.

What are the possibities for Answ3?
Answ1 (0,2) #This means Answ1 can be anywhere from 0 to 2
Answ2 (1,5) #This means Answ1 can be anywhere from 1 to 5
Answ3 = Answ1 + Answ2

﻿The lowest number answ1 will generate is 0 and the lowest number answ2 will generate is 1.
Therefore, the lowest number answ3 could be is 1.
The highest number answ1 will generate is 2 and the highest number answ2 will generate is 5.
Therefore, the highest number answ3 could be is 7.

Generating Random Values:
 - In AP CSP, students learn to generate random values using certain code constructs, like the random module in Python which allows for random integer generation between specified values using random.randint(a, b)​1​. This random number generation introduces an element of unpredictability, vital for many programming applications.
Application in Simulations:
- Random values are crucial in simulations, mimicking real-world unpredictability. They help in creating diverse scenarios in simulations like weather patterns or game dynamics, thus providing a more realistic or varied simulation experience.
Evaluating Code Segments:
- Utilizing random values can aid in evaluating code segments by testing how code reacts to varied input, which is particularly useful in identifying potential bugs or inefficiencies.


If you roll a die 3 times, and take the sum of all your rolls, what is the highest possible amount and the lowest possible amount you can get? 

Roll 1 (1,6)
Roll 2 (1,6)
Roll 3 (1,6)

Lowest: 3
Most: 18


```python
import random

def generate_random():
    value = random.randint(1, 100)
    print(f'Random value between 1 and 100: {value}')

    dice_roll = random.randint(1, 6)
    print(f'Dice Roll: {dice_roll}')

# Call the function
generate_random()
```

    Random value between 1 and 100: 75
    Dice Roll: 6


Hack #4

Lets continue the fun...
Make an algorithm that assigns 5 days with a random temperatures between 60-90 degrees Fahrenheit! 


```python
import random

def generate_random():
    for x in range(1, 6):
        temperature = random.randint(60, 90)
        print(f'On day {x}, the temperature is {temperature}°F')


# Call the function
generate_random()
```

    On day 1, the temperature is 87°F
    On day 2, the temperature is 60°F
    On day 3, the temperature is 71°F
    On day 4, the temperature is 66°F
    On day 5, the temperature is 65°F


Solution: 

How can you iterate between a range of 5 days, along with generate a random temperature between 60-90?


```python
import random

def simulate_weather():
    for day in range(1, 6):
        temperature = random.randint(60, 90)
        print(f'Day {day}: Temperature: {temperature}°F')

# Call the function
simulate_weather()
```

# Homework: 

1. Create a program that follows the Collatz Conjecture. 

If a number is even, divide by 2.

If a number is odd, multiply by 3 and add 1.

If implemented correctly this algorithm will eventually go to 1. Try defining the initial number with any number beside 1 to see an interesting ouput. Output the result as a list. You may set a starting value for the list, so that the program can generate the list of numbers created when following the process. 

Ideas for above 90%:
Try implementing user input into this program. Ask the user to enter a number they would like to start with. 



```python
user_inp = int(input("Please input an integer: "))


def Collatz_sequence(Collatz_lst, user_inp):
    if user_inp % 2 == 0:
        user_inp = user_inp // 2
    else:
        user_inp = user_inp * 3 + 1
    Collatz_lst.append(user_inp)
    if user_inp != 1:
        Collatz_sequence(Collatz_lst, user_inp)


if user_inp <= 0:
    print("Put an actual integer breh")
else:
    
    Collatz_lst = [user_inp]
    Collatz_sequence(Collatz_lst, user_inp)
    print("Sequence in play: ", Collatz_lst)



```

    Sequence in play:  [15, 46, 23, 70, 35, 106, 53, 160, 80, 40, 20, 10, 5, 16, 8, 4, 2, 1]


2. Create an algorithm that generates terms to the Fibonacci Sequence which outputs a specific number of terms defined in your code. The sequence starts off like 1, 1, 2, 3, 5, … each following term being the sum of the previous two.

Ideas for above 90%:

- Add user input
- Display error message when an invalid input is specified
- Find a way for the program to only specify a specific term in the sequence


```python
import random
x = int(input("input a valid integer number"))
flag = 0
try:
    if x < 0:
        print("Error: Please input a valid number")
        flag = 1
except ValueError:
    print("Error: Value error breh please input a positive integer blud")
    flag = 1
    
x = x - 2

if flag == 0:
    lst = [1, 1]
    for num in range(0, x):
        lst.append(lst[-2] + lst[-1])
    print(lst)
```

    [1, 1, 2]


# Place your code here...

3. Make a statistics calculator that calculates the mean, median, and mode of a specific series. Do this using iteration and without the use of imported modules (like the statistics one) that allows you to call pre defined functions like mean, median, and mode. Each of these calculations follows an algorithm. 

Ideas for above 90%:

- Randomly generate a list of numbers (you can define it as a list of 5) to apply the calculator to.
- If you can, generate a random number of elements in the data set as well (keep it between 5-10 elements). 


```python
# Place your code here...
import random

data_length = random.randint(5, 10)
data = [random.randint(1, 100) for _ in range(data_length)]

mean = sum(data) / len(data)

sorted_data = sorted(data)
mid = len(sorted_data) // 2
median = (sorted_data[mid] + sorted_data[-mid - 1]) / 2 if len(sorted_data) % 2 == 0 else sorted_data[mid]

count_dict = {}
for num in data:
    count_dict[num] = count_dict.get(num, 0) + 1
mode = [num for num, count in count_dict.items() if count == max(count_dict.values())]

print("Generated Data:", data)
print("Mean:", mean)
print("Median:", median)
print("Mode:", mode)
```

    Generated Data: [20, 47, 86, 56, 63, 26, 55, 20, 19]
    Mean: 43.55555555555556
    Median: 47
    Mode: [20]

