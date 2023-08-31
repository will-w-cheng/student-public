---
layout: post
title: Just a quiz me and saaras made
description: Clean and optimized just like my website
toc: True
comments: True
categories: ['5.A', 'C4.1']
courses: {'csse': {'week': 0}, 'csp': {'week': 1, 'categories': ['6.B']}, 'csa': {'week': 0}}
type: hacks
---

## Python Input/Output:
- We were able to utilize our pre-requisite, knowledge of functions to create a set of questions and answers in a more optimal fashion where it is less lines of code and looks more aesthetic to the eye.




```python
import getpass, sys, os
def ask_question(question, correct_answer):
    user_response = input(f"Question: {question}\nYour Answer: ")
    if user_response.lower() == correct_answer.lower():
        print(f"Correct!\n")
        return 1
    else:
        print(f"Sorry, that's incorrect. The correct answer is: {correct_answer}\n")
        return 0
    
def main():
    questions = [
        ("Is Python a programming language?", "yes"),
        ("Can you store multiple values in a list?", "yes"),
        ("Does Python use indentation to define code blocks?", "yes"),
    ]

    print(f"Hello, {getpass.getuser()} running {sys.executable}")
    print(f"You will be asked {len(questions)} questions.")
    input("Press Enter to start the test...")
    correct_count = sum(ask_question(q, a) for q, a in questions)
    percentage = (correct_count / len(questions)) * 100
    print(f"{getpass.getuser()}, you scored {correct_count}/{len(questions)} which is {percentage:.2f}%.")

if __name__ == "__main__":
    main()
```
