---
layout: post
title: Lists and search
description: Lists and Search Collegeboard units
toc: True
comments: True
categories: ['5.A', 'C4.1']
courses: {'csse': {'week': 8}, 'csp': {'week': 0, 'categories': ['6.B']}, 'csa': {'week': 9}}
type: hacks
---

# Made by: Ryan, Daniel, Saaras, Will, and Andrew

## Python lists Operations

### Append function
# From the Data Abstractions Unit we Learned bout lists and how they can store multiple variables 
# Today we're going to show you how to add items to lists utilizing the append option


```python

lst = []
lst.append("item1")
print(lst)
```

    ['item1']


### Insert function
- The insert function allows you to append items to different lists at a specific location.
- Let's first understand how it may work through pseudocode

#### Exmaple 1
INSERT alist, pos, value 
INSERT alist, 1, "hi" 
- Here the alist represents your list you want to append an item to
- The position is where on the list you may want to add your item 
- Finally, the value is the item actually is that your adding to your list
- So here in total in position 1 you insert the string "hi" into alist

### Your turn!!!!
- Turn this pseudocode into python
- How may we want to implement this on python? Think back to the data abstraction unit. 
- ( Hint: Think about the differences between psueodcode and python )


```python
# ANSWER: 
# Inserting items to a specific list, remember python is 0 based on the items!!
lst.insert(0, "item0")
print(lst)
```

    ['item1', 'item0']


### Remove function
- The remove functions allows you to remove specific items at a specific position on the list

#### Pseudocode example
- REMOVE aList, pos




```python
# Remove method 
lst.remove(0)
print(lst)

## You can also access the list by the position, this is called list indexing
print(lst[0])
```

### Let's do some Collegeboard exercises
- In the following list:
  - nums = [65, 89, 92, 35, 84, 78, 28, 75]
- Figure out what the minimum number in the list, WITHOUT using the other methods and premade functions.

### Second question:
- Let's say we have a list called "animals" from a survey that stores whether or not they prefer "cats" or "dogs" as strings in this list.
- Transverse this list and tell me the total amount cats and dogs in the list



```python
nums = [65, 89, 92, 35, 84, 78, 28, 75]

## Your code here
```


```python
animals = ["cats", "dogs"]
```
