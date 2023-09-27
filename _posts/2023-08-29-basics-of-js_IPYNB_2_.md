---
title: Basics of Javascript
hide: True
description: A Tech Talk on how to use javascript
type: ccc
permalink: /basics/javascript
author: Rohan Juneja
---

{% include nav_basics.html %}


# How to use javascript in any of your pages
- Simply add a ``<script></script>`` in your markdown or jupyter cells
- (Note: the %%html magic command allows us to add HTML and JavaScript into a jupyter notebook, the outputted "site" will be shown below the code)


```python
%%html
<h3>Page Heading</h3>
<p>Paragraph description of page</p>
<script>
    console.log("Output to console, showing that JavaScript code is running")
</script>

```


<h3>Page Heading</h3>
<p>Paragraph description of page</p>
<script>
    console.log("Output to console, showing that JavaScript code is running")
</script>



# Writing text to console.log
- The text written with `console.log` appears in the Console
- `console.log` allows you to write text -- but you don't see any text in above example until you view Console.
- Activate Console window
    - VSCode Help-Toggle Developer Tools allows you to see console.log output
    - Chrome and other browsers require right click -> inspect also allows access to console.log output
        - Safari users will need to enable developer settings before inspecting an element. To do this go to Safari settings -> advanced and check the box next to "Show develop menu in menu bar"
    - By default you usually need to click Console next to Elements, to see console.log output
    - Also, you may want to press clear console (cirlcl with slash) to clean up screen before analysis. 


## Try code with Console
- Developers typically keep console open
- In console window, you can run javascript code from prompt

# Storing data
- One of the most important things in programming is learning how data is stored, this is often called Data Abstraction (the ability to represent data in a programming language).

## Types of data
- Javascript has a few basic types of data, which align with what the types of data you might know yourself
- In javascript, these types are formalized as:
  - text = "string", number = "number", true/false = "boolean"

## Name the Data
- When you think of data, it has a name and a value.
- Using the "var" JavaScript syntax you create a `variable` with a name and a value.
- In javascript this can represented with the following: `var someName = value;`
  - The name cannot have spaces
  - Text values must be wrapped in single or double quotes to identify it as text (see exmaples below)

## Accessing data
- To access data (the value of a variable), simply just use the name of the variable
- For example, we can use the values from previously in a `console.log`


```python
%%html

<script>
// create variables
var firstName = "Rohan"
var lastName = 'Juneja'
var age = 17;
var isSchoolDay = true; 

// inspect values and type
console.log(firstName, typeof firstName)
console.log(lastName, typeof lastName)
console.log(age, typeof age)
console.log(isSchoolDay, typeof isSchoolDay)

</script>
```



<script>
// create variables
var firstName = "Rohan"
var lastName = 'Juneja'
var age = 17;
var isSchoolDay = true; 

// inspect values and type
console.log(firstName, typeof firstName)
console.log(lastName, typeof lastName)
console.log(age, typeof age)
console.log(isSchoolDay, typeof isSchoolDay)

</script>



# String Operators
- "+" concatenates string, same as combining text
- "==" checks if strings are the same, if so it outputs `true`, otherwise `false`
  - "!==" is "not equal to" (opposite of equal to)

## Assignment Operator
- "=" can be used to change the value of a variable
  - ie. if you already created "name1" you can reassign name1 = "New Name"


```python
%%html

<script>
// string assignment
var name1 = "Doe"
var name2 = "Doe"

// compare names
console.log("String Comparison")
console.log("name1", name1)
console.log("name2", name2)
console.log("name1 == name2", name1 == name2)

// changing the value of name1 and repeat compare
console.log("String Comparison after change")
name1 = "John"  // reassign
console.log("name1", name1)
console.log("name2", name2)
console.log("name1 == name2", name1 == name2)

console.log("String Concatenation")
console.log(name1 + " " + name2)
</script>

```



<script>
// string assignment
var name1 = "Doe"
var name2 = "Doe"

// compare names
console.log("String Comparison")
console.log("name1", name1)
console.log("name2", name2)
console.log("name1 == name2", name1 == name2)

// changing the value of name1 and repeat compare
console.log("String Comparison after change")
name1 = "John"
console.log("name1", name1)
console.log("name2", name2)
console.log("name1 == name2", name1 == name2)

console.log("String Concatenation")
console.log(name1 + " " + name2)
</script>



# Number Operators
- "+" adds numbers together
- "-" subtracts numbers, "/" divides numbers, "*" multiples numbers
- "===" checks if two values are the same, if so it outputs `true`, otherwise `false`
  - "!==" is "not equal to" (opposite of equal to)
  - normal oeprators like "<", ">", ">=" (greater than or equal to), "<=" with numbers

## Assignment Operator
- "=" can be used to create or change the value of a variable


```python
%%html

<script>
var age1 = 17
var age2 = 16
var age3 = '17'

console.log("Number Comparisons")
console.log("age1:", age1)
console.log("age2:", age2)
console.log("age3:", age3)
console.log("age1 == age2", age1 == age2)
console.log("age1 == age3", age1 == age3)
console.log("age1 === age3", age1 === age3)
console.log("age1 > age2", age1 > age2)
console.log("age1 < age2", age1 < age2)

var num1 = 9
var num2 = 5
console.log("\n")
console.log("Arithmetic Operations")
console.log("num1:", num1)
console.log("num2:", num2)
console.log("num1 + num2", num1 + num2)
console.log("num1 - num2", num1 - num2)
console.log("num1 * num2", num1 * num2)
console.log("num1 / num2", num1 / num2)
console.log("num1 % num2", num1 % num2)

</script>
```



<script>
var age1 = 17
var age2 = 16
var age3 = '17'

console.log("Number Comparisons")
console.log("age1:", age1)
console.log("age2:", age2)
console.log("age3:", age3)
console.log("age1 == age2", age1 == age2)
console.log("age1 == age3", age1 == age3)
console.log("age1 === age3", age1 === age3)
console.log("age1 > age2", age1 > age2)
console.log("age1 < age2", age1 < age2)

var num1 = 9
var num2 = 5
console.log("\n")
console.log("Arithmetic Operations")
console.log("num1:", num1)
console.log("num2:", num2)
console.log("num1 + num2", num1 + num2)
console.log("num1 - num2", num1 - num2)
console.log("num1 * num2", num1 * num2)
console.log("num1 / num2", num1 / num2)
console.log("num1 % num2", num1 % num2)

</script>



# Conditional Statements
- Think about any actions that you take: you usually take them based on information you take in
  - If tommorow is a school day, set an alarm for tomorrow at 8am
- We can also add additional clauses at the end
  - If tommorow is a school day, set an alarm for tomorrow at 8am, otherwise (else) set an alarm for tommorow at 10am


```python
%%html

<script>
// the above example in code
console.log("Alarm Example")

var tommorowIsSchoolDay = false

if (tommorowIsSchoolDay) {
    // this code runs if tommorw is a school day
    console.log("Setting alarm for 8am")
} else {
    // this code runs if tommorow is not a school day
    console.log("Setting alarm for 10am")
}
</script>
```



<script>
// the above example in code
console.log("Alarm Example")

var tommorowIsSchoolDay = false

if (tommorowIsSchoolDay) {
    // this code runs if tommorw is a school day
    console.log("Setting alarm for 8am")
} else {
    // this code runs if tommorow is not a school day
    console.log("Setting alarm for 10am")
}
</script>



# Conditional Statements + Operators
- Since many operators return a true/false value (equals, gerater than, etc.) we can use them inside "if" statements


```python
%%html
<script>
console.log("If statements + Operators")
var age1 = 17
var age2 = 37

if (age1 > age2) {
    // runs if age1 is more than age2
    console.log("age1 is more than age2")

} else if (age1 == age2) {
    // runs if age1 and age2 are the same
    console.log("age1 is the same as age2")

// (age1 < age2)
} else  {
    // runs if age2 is more than age1
    console.log("age1 is less than age2")
}

</script>
```


<script>
console.log("If statements + Operators")
var age1 = 17
var age2 = 37

if (age1 > age2) {
    // runs if age1 is more than age2
    console.log("age1 is more than age2")

} else if (age1 == age2) {
    // runs if age1 and age2 are the same
    console.log("age1 is the same as age2")

// (age1 < age2)
} else  {
    // runs if age2 is more than age1
    console.log("age1 is less than age2")
}

</script>



# Hacks
- Write a JavaScript program that compares two variables, a and b. Log "a is greater" if a is greater than b, "b is greater" if b is greater than a, and "both are equal" if a and b are equal. Make sure to use if statements and console.log


```python
%%js
// put your javascript code here
```


    <IPython.core.display.Javascript object>

