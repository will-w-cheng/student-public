---
comments: True
layout: post
title: Algorthmic Rhythm
description: Looking at the different sorting algorthims presented in a unique and funny way by the CSA students.
type: tangibles
courses: {'csp': {'week': 28}}
---

# Types of sorting

## Insertion Sort
- Insertion sorting in this example, included a bunch of different pool noodle lengths. The goal is to sort the noodle lengths in order. 
- You go through down the list, in this example you can insert the corresponding pool noodles based on the sizes of the previous elements.
- The worst possible case time scenario is O(N^2) because you might have a nested for loop to sort the element, thus it's not the fastest possible way to sort but it's a method. 

## Quick sort
- The pivot splits the array into two different arrays, one that is bigger goes into a bigger array, and the smaller one goes into the smaller sort. This process continues through rrecursion
- O(n*(log(n))) insanely quickly

## Bubble sort
- Worst case o(n^2) best case is o(n)
- Almost basically the same thing as insertion sort but it only looks at the one previous behind it. 

## Merge sort
- O(log * (n))
- Split the lists in half repeatedly until each list is split into a group of two
- Then that moves onto combining a group of four and then sorts within there continously having bigger groups of lists until the whole thing is sorted.

## Selection Sort
- Loop through the list in each sub-selection and place the the minimum in the beginning ofo the list in order to sort it. Then you can take the unsorted sub-selections of the list out to fix it. 
- O(N^2) time complexity
