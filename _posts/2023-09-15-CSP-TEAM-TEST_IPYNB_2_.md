---
title: CSP team test
toc: True
description: Program with function and purpose that I personally worked on with my team test, this is my part!
courses: {'csp': {'week': 4}}
type: hacks
---

```python
!jt -t chesterish
```


```python
# Program with Output
print("Program with Output")
print("Hello, world")
```

    Program with Output
    Hello, world



```python
# Program with Input and Output
print("\nProgram with Input and Output")
name = input("Enter your name: ")
print("Hello, " + name + "!")
```


```python
# Program with a List
print("\nProgram with a List")
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```


```python
# Program with a Dictionary
print("\nProgram with a Dictionary")
student = {"name": "John", "age": 25, "grade": "A"}
print("Student Information:")
for key, value in student.items():
    print(key + ": " + str(value))
```


```python
# Program with Iteration
print("\nProgram with Iteration")
for i in range(1, 6):
    print("Number:", i)
```


```python
# Program with a Function to perform mathematical and/or statistical calculations
print("\nProgram with a Function for Calculation")
def calculate_average(numbers):
    total = sum(numbers)
    average = total / len(numbers)
    return average
```


```python
# Program with a Function to perform mathematical and/or statistical calculations
print("\nProgram with a Function for Calculation")
def calculate_average(numbers):
    total = sum(numbers)
    average = total / len(numbers)
    return average

data = [10, 15, 20, 25, 30]
avg = calculate_average(data)
print("Average:", avg)
```


```python
# Program with a Selection/Condition
print("\nProgram with Selection/Condition")
num = int(input("Enter a number: "))
if num % 2 == 0:
    print(num, "is even.")
else:
    print(num, "is odd.")
```


```python
# Program with Purpose
print("\nProgram with Purpose")
def find_factorial(n):
    if n == 0:
        return 1
    else:
        return n * find_factorial(n - 1)

number = int(input("Enter a number to find its factorial: "))
factorial = find_factorial(number)
print("Factorial of", number, "is", factorial)
```
