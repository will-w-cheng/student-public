---
title: CSP team test
toc: True
description: Program with function and purpose that we personally worked on with my team test, this is our part!
courses: {'csp': {'week': 4}}
type: hacks
---

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

    
    Program with Input and Output
    Enter your name: will
    Hello, will!



```python
# Program with a List
print("\nProgram with a List")
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

    
    Program with a List
    apple
    banana
    cherry



```python
# Program with a Dictionary
print("\nProgram with a Dictionary")
student = {"name": "Will", "age": 25, "grade": "A"}
print("Student Information:")
for key, value in student.items():
    print(key + ": " + str(value))
```

    
    Program with a Dictionary
    Student Information:
    name: Will
    age: 25
    grade: A



```python
# Program with Iteration (stop here will), one based numbering
print("\nProgram with Iteration")
for i in range(1, 6):
    print("Number:", i)
```

    
    Program with Iteration
    Number: 1
    Number: 2
    Number: 3
    Number: 4
    Number: 5



```python
# Program with a Function to perform mathematical and/or statistical calculations
print("\nProgram with a Function for Calculation")
def calculate_average(numbers):
    total = sum(numbers)
    average = total / len(numbers)
    return average
```

    
    Program with a Function for Calculation



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

    
    Program with a Function for Calculation
    Average: 20.0



```python
# Program with a Selection/Condition
print("\nProgram with Selection/Condition")
num = int(input("Enter a number: "))
if num % 2 == 0:
    print(num, "is even.")
else:
    print(num, "is odd.")
```

    
    Program with Selection/Condition
    17 is odd.



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

    
    Program with Purpose
    Enter a number to find its factorial: 18
    Factorial of 18 is 6402373705728000

