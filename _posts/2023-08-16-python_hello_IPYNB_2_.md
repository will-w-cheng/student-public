---
layout: post
title: Python IO
description: These examples show the basic language structures and constructs of Python using input and output (print) commands.
courses: {'csp': {'week': 1, 'categories': ['1.A', '3.A', '4.B']}}
categories: ['C4.0']
type: ccc
---

### Print command using Static Text which performs output
The classic introduction to a programming language is to output a "Hello, World!" message.  In Python, this is a print statement.   
- The <mark>command or function</mark> is print()
- "Hello, World" is a String literal. This is the referred to as <mark>Static text</mark>, as it does not change.
- "Hello, World" is a parameter to the print function in Python.
- The <mark>print command outputs</mark> the parameter to the terminal, as you see it in this Jupyter document
- <mark>Output</mark> in Jupyter Notebook is below the code cell.  Output will vary depending on tools and development intentions. Python print typically outputs to a terminal, we will see that when students start using Visual Studio Code.


```python
print("Hello World!")
```

    Hello World!


### Dynamic example showing variables, input and output
This second example is a <mark>sequence of code</mark>, two or more lines forms a sequence.  This example takes input from the user and stores the input into a variable called msg (short for message), then outputs the msg to terminal.  - This example is <mark>Dynamic as the input and output can change</mark> each time the code is run.
- A variable "msg" is part of both statement 
    - The variable "msg" is used to capture the input command
    - The variable "msg" is then used as a <mark>parameter to print command</mark>, causing input to be <mark>output to terminal</mark>, or in Jupyter Notebook below the code cell.
- The "input" command activates the jupyter notebook input box, which obtains <mark>input from the user</mark> (try it!)
    - the "msg" variable is the dynamic result of the input command
- The print command outputs the "msg" variable captured in the input statement
    - note, msg is a <mark>parameter to the print function</mark>  
- <mark>Input and Output</mark> in Jupyter Notebook Input is NOT in line with Output, this is a little annoyance and requires familiarity.  Input and Output will vary depending on tools and development intentions. Python print typically obtains input and outputs to a terminal, students will see that when they run Python programs using Visual Studio Code.


```python
msg = input("Enter a greeting: ")
print(msg)
```

### Building a Function
This example adds to the basics of the <mark>Python anatomy</mark>, a function. Input, output, and grouping commands in functions is the key to most programming languages.  This example simulates a free response answer to a question.  
- The "def question_and_answer(prompt)" now contains multiple indented commands,  the commands  print and input were learned previously.
- Grouping a sequence of commands, often used repeatedly, is called <mark>procedural abstraction</mark>.
- Procedure, Function, def are all synonyms in the Python language. 
- The <mark>"def" is a key word in Python that defines a function</mark>.  Using this keyword defines a group of commands, but does not run them initially. 
- The name of the function in this example is "question_and_answer".  In essence, we are defining our own command within the Python language.
- The three "question_and_answer" commands that follow the function and indented commands allow this function to be run.
- This code of the function is then run multiple times, each command line providing a unique "prompt" as a result of the literal parameter passed to the function.
- The <mark>function takes a parameter</mark> called "prompt", which is a message output to the user to describe the input requested.  
- <mark>String concatenation</mark> "+" prefixes the prompt with the literal message "Question: ".
- The "msg" variable is captured as a result of the jupyter notebook input supplied by the user
- The input "msg" is output back to the user with "Answer: " concatenated to the front.


```python
def question_and_answer(prompt):
    print("Question: " + prompt)
    msg = input()
    print("Answer: " + msg)

question_and_answer("Name the Python output command mentioned in this lesson?")
question_and_answer("If you see many lines of code in order, what would College Board call it?")
question_and_answer("Describe a keyword used in Python to define a function?")
```

### Imports, Selection, and Logical Expressions
In Python anatomy of you will be <mark>importing libraries and functions</mark>.  This is code that is developed by others.  In this example we are importing from a library called "os", this library extracts properties from the operating system of your existing system.   Additionally, this example uses the custom function defined earlier in the Jupyter document.  Python and Jupyter docs requires you to reference imports and definitions above the referencing line of code.
- import os, sys obtain functions and variables from running environment
- print('Hello, ' + getpass.getuser() + " running " + sys.executable + " on " + sys.platform + "!"), is a concatenated statement that outputs properties from the import

Next, this example defines a new function "question_with_response", <mark>this function returns a value</mark> input by the user.  This allows programmer to evaluate the response.  The purpose of obtaining the return value is to evaluate if correct response was given to the question.
- response from "question_with_response" is captured in a variable called "rsp"
    - return command in function returns msg input by user
    - assignment to "rsp" is allowed a function is returning a value, names do not need to match (but could)
- <mark>if command</mark> is next command in sequence after "rsp" assignment
   - this command contains an expression, rsp == "import" which compare what is typed to the string literal answer
   - an <mark>if expression</mark> is evaluated for true or false
   - true takes branch of code directly under if
   - false takes branch of code directly under <mark>else command</mark>

The grand finally of this example is calculating the right/total.
- question = 3 is <mark>defined as number</mark> of questions
- correct = 0 is defined as running score
- correct += 1 is the way to <mark>add one to the score</mark>, this code is placed in sequence under correct expression evaluation
- since question and correct are numbers, versus strings, to place them in concatenation in print statements you must inclose them in Python <mark>function str()</mark> which turns number into string.
- final print statement is concatenated and formatted to give user and right over wrong


```python
import getpass, sys

def question_with_response(prompt):
    print("Question: " + prompt)
    msg = input()
    return msg

questions = 3
correct = 0

print('Hello, ' + getpass.getuser() + " running " + sys.executable)
print("You will be asked " + str(questions) + " questions.")
question_and_answer("Are you ready to take a test?")

rsp = question_with_response("What command is used to include other functions that were previously developed?")
if rsp == "import":
    print(rsp + " is correct!")
    correct += 1
else:
    print(rsp + " is incorrect!")

rsp = question_with_response("What command is used to evaluate correct or incorrect response in this example?")
if rsp == "if":
    print(rsp + " is correct!")
    correct += 1
else:
    print(rsp + " is incorrect!")

rsp = question_with_response("Each 'if' command contains an '_________' to determine a true or false condition?")
if rsp == "expression":
    print(rsp + " is correct!")
    correct += 1
else:
    print(rsp + " is incorrect!")

print(getpass.getuser() + " you scored " + str(correct) +"/" + str(questions))
```

## Hacks
Test running a Python file directly
- From python directory run quiz.py in VS Code, this will show workflow of Input and Output in terminal

Build your own Jupyter Notebook meeting these College Board and CTE competencies
- Build your own quiz, including my questions and show outputs
- Create both Markdown for description and Code for execution
- Structure your Python code with comments "#" to complement Markdown descriptions

Additional requirements
- Build your quiz so that it captures the key Vocabulary from this Jupyter document
- Calculate the percentage of your quiz
- Review College Board Big Idea outline, see if you can reference locations in Markdown that support vocabulary

Extra credit, Advanced
- Do you see repeating pattern of code?  Try to implement solution to avoid the repeating pattern (hint: list and iteration)
