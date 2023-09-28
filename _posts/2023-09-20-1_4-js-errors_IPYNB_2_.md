---
layout: post
title: 1.4 Correcting errors
description: Practice with identifying and correcting code blocks
type: ccc
author: Safin Singh and Rohan Juneja
permalink: /basics/js-debug
hide: True
---

{% include nav_basics.html %}

[College Board Big Idea 1](https://apclassroom.collegeboard.org/103/home?unit=1)

## Identifying and Correcting Errors (Unit 1.4)

> Become familiar with types of errors and strategies for fixing them

- Review CollegeBoard videos and take notes on blog
- Complete assigned MCQ questions if applicable

# Code Segments

Practice fixing the following code segments!

## Segment 1: Alphabet List

Intended behavior: create a list of characters from the string contained in the variable `alphabet`

### Code:


```python
%%js

var alphabet = "abcdefghijklmnopqrstuvwxyz";
var alphabetList = [];

for (var i = 0; i < 10; i++) {
	alphabetList.push(alphabet[i]);
}

console.log(alphabetList);
```


    <IPython.core.display.Javascript object>


### What I Changed

Originally this function printed the a list of numbers from 0-9. Instead I changed the alphabetList.push(i) section to alphabet.push(alphabet[i]) so that instead of printing the numbers, it will bring the letters from variable alphabet. It only takes the letters from 0-9.

## Segment 2: Numbered Alphabet

Intended behavior: print the number of a given alphabet letter within the alphabet. For example:
```
"_" is letter number _ in the alphabet
```

Where the underscores (_) are replaced with the letter and the position of that letter within the alphabet (e.g. a=1, b=2, etc.)

### Code:


```python
%%js

// Copy your previous code to built alphabetList here
var alphabet = "abcdefghijklmnopqrstuvwxyz";
var alphabetList = [];

let letterNumber = 5

for (var i = 0; i < alphabet.length; i++) {
	if (i === letterNumber) {
		console.log(" e is letter number 5 in the alphabet")
	}
}

// Should output:
// "e" is letter number 5 in the alphabet
```


    <IPython.core.display.Javascript object>


### What I Changed
I added the alphabet variable so that ther is no more sytax error and I also changed i < alphabet.length so that 0 is looping the length of the alphabet variable not the alphabetList variable. I also changed the message that is shown if the loop is true so that it prints the correct message. 

## Segment 3: Odd Numbers

Intended behavior: print a list of all the odd numbers below 10

### Code:


```python
%%js

let odds = [];
let i = 1;

while (i <= 10) {
  odds.push(i);
  i += 2;
}

console.log(odds);
```


    <IPython.core.display.Javascript object>


### What I Changed

Orginally it prints all of the even numbers between 0 and 10. I changed the variable name to odds because it makes more sense considering we're trying to print odd numbers. I changed i to be defined as 1 instead of zero so that i when I increment by two it would only show the odd numbers and not the even ones. 

# BELOW NOT EDITED

The intended outcome is printing a number between 1 and 100 once, if it is a multiple of 2 or 5 
- What values are outputted incorrectly. Why?
- Make changes to get the intended outcome.


```python
%%js

var numbers = [];
var uniqueNumbers = []; // Array to store unique numbers
var i = 0;

while (i < 100) {
    numbers.push(i);
    i += 1;
}

for (var i of numbers) {
    if (numbers[i] % 5 === 0 && uniqueNumbers.indexOf(numbers[i]) === -1) {
        uniqueNumbers.push(numbers[i]);
    }
    if (numbers[i] % 2 === 0 && uniqueNumbers.indexOf(numbers[i]) === -1) {
        uniqueNumbers.push(numbers[i]);
    }
}

console.log(uniqueNumbers);


```


    <IPython.core.display.Javascript object>


### What I Changed
I added an additional array to keep track of the duplicates. Before pushing numbers into the new array (uniqueNumbers) it checks for dupliactes using the indexOf method.

# Challenge

This code segment is at a very early stage of implementation.
- What are some ways to (user) error proof this code?
- The code should be able to calculate the cost of the meal of the user

Hint:
- write a “single” test describing an expectation of the program of the program
- test - input burger, expect output of burger price
- run the test, which should fail because the program lacks that feature
- write “just enough” code, the simplest possible, to make the test pass

Then repeat this process until you get program working like you want it to work.


```python
%%js

var menu =  {"China": 3.99,
         "U.S.A": 1.99,
         "Russia": 0.99}
var total = 0

//shows the user the menu and prompts them to select an item
console.log("Menu")
for (var item in menu) {
    console.log(item + "  $" + menu[item].toFixed(2)) //why is toFixed used?
}
//ideally the code should support mutliple items
var item = "China"

//code should add the price of the menu items selected by the user 
console.log(total)
```

## Hacks
- Fix the errors in the first three segments in this notebook and say what you changed in the code cell under "What I Changed" (Challenge is optional)
