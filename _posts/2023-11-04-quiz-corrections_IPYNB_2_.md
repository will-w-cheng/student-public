---
toc: True
comments: True
layout: post
title: Quiz Corrections
description: Done extremely late in the night and questions that I could improve on
courses: {'csp': {'week': 10}}
type: tangibles
---

# I got a 61/66 on the CB quiz



### Question 1
Directions: For the question or incomplete statement below, two of the suggested answers are correct. For this question, you must select both correct choices to earn credit. No partial credit will be earned if only one correct choice is selected. Select the two that are best in each case.

The procedure Smallest is intended to return the least value in the list numbers. The procedure does not work as intended.

The program consists of 12 lines. Begin program Line 1: PROCEDURE Smallest, open parenthesis, numbers, close parenthesis Line 2: open brace Line 3: min, left arrow, numbers, open bracket, 1, close bracket Line 4: FOR EACH number IN numbers Line 5: open brace Line 6: IF, open parenthesis, number is less than min, close parenthesis Line 7: open brace Line 8: RETURN, open parenthesis, number, close parenthesis Line 9: close brace Line 10:close brace Line 11: RETURN, open parenthesis, min, close parenthesis Line 12: close brace End program.

For which of the following values of One word, the List will Smallest, open parenthesis, one word, the List, close parenthesis NOT return the intended value?

Select two answers.

A
One word, the List, left arrow, open bracket, 10, 20, 30, 40, close bracket
B
One word, the List, left arrow, open bracket, 20, 10, 30, 40, close bracket
C
One word, the List, left arrow, open bracket, 30, 40, 20, 10, close bracket
D
One word, the List, left arrow, open bracket, 40, 30, 20, 10, close bracket


### Correction:
Answer D
This option is correct. The procedure returns the first number it encounters that is less than the first number in the list. For the list open bracket, 40, 30, 20, 10, close bracket, the procedure returns 3 0, which is not the least value in the list.

### Question 2:
Directions: For the question or incomplete statement below, two of the suggested answers are correct. For this question, you must select both correct choices to earn credit. No partial credit will be earned if only one correct choice is selected. Select the two that are best in each case.

A program is created to perform arithmetic operations on positive and negative integers. The program contains the following incorrect procedure, which is intended to return the product of the integers x and y.

The program consists of 11 lines. Begin program Line 1: PROCEDURE Multiply, open parenthesis, x comma y, close parenthesis Line 2: open brace Line 3: count, left arrow, 0 Line 4: result, left arrow, 0 Line 5: REPEAT UNTIL, open parenthesis, count equals y, close parenthesis Line 6: open brace Line 7: result, left arrow, result plus x Line 8: count, left arrow, count plus 1 Line 9: close brace Line 10: RETURN, open parenthesis, result, close parenthesis Line 11: close brace End program.

A programmer suspects that an error in the program is caused by this procedure. Under which of the following conditions will the procedure NOT return the correct product?

Select two answers.

### Corection: 
Answer B
This option is correct. If y is negative, then the condition count equals y will never be met since count begins at 0 and repeatedly increases.

Answer D
This option is correct. If y is negative, then the condition count equals y will never be met since count begins at 0 and repeatedly increases.


### Question 3:
Directions: The question or incomplete statement below is followed by four suggested answers or completions. Select the one that is best in each case.

A program contains the following procedures for string manipulation.

A table is shown with 2 columns and 3 rows. The first row of the table contains the column headers, from left to right, Procedure Call and Explanation. The table is as follows: Concat, open parenthesis, s t r 1 comma s t r 2, close parenthesis, Returns a single string consisting of s t r 1 followed by s t r 2. For example, Concat, open parenthesis, quotation mark, key, quotation mark, comma, quotation mark, board, quotation mark, close parenthesis, returns, quotation mark, keyboard, quotation mark. Substring, open parenthesis, s t r, comma, start, comma, length, close parenthesis, Returns a substring of consecutive characters from s t r, starting with the character at position start and containing length characters. The first character of s t r is located at position 1. For example, Substring, open parenthesis, quotation mark, delivery, quotation mark, comma, 3, comma, 4, close parenthesis returns quotation mark, live, quotation mark.

Which of the following expressions can be used to generate the string Open quotation, Happy, close quotation?

A
Concat, open parenthesis, Substring, open parenthesis, open quotation, Harp, close quotation, comma 1 comma 1, close parenthesis, comma, Substring, open parenthesis, open quotation, Puppy, close quotation, comma, 2 comma 4, close parenthesis, close parenthesis
B
Concat, open parenthesis, Substring, open parenthesis, open quotation, Harp, close quotation, comma 1 comma 2, close parenthesis, comma, Substring, open parenthesis, open quotation, Puppy, close quotation, comma, 3 comma 3, close parenthesis, close parenthesis
C
Concat, open parenthesis, Substring, open parenthesis, open quotation, Harp, close quotation, comma 1 comma 2, close parenthesis, comma, Substring, open parenthesis, open quotation, Puppy, close quotation, comma, 4 comma 2, close parenthesis, close parenthesis
D
Concat, open parenthesis, Substring, open parenthesis, open quotation, Harp, close quotation, comma 2 comma 2, close parenthesis, comma, Substring, open parenthesis, open quotation, Puppy, close quotation, comma, 4 comma 2, close parenthesis, close parenthesis

### Correction:
Answer C
This option is incorrect. This expression returns the string Open quotation, Hapy, close quotation.

### Question 4:
Directions: The question or incomplete statement below is followed by four suggested answers or completions. Select the one that is best in each case.

A student wrote the procedure below, which is intended to ask whether a user wants to keep playing a game. The procedure does not work as intended.

The program consists of 13 lines. Begin program Line 1: PROCEDURE, one word Keep Playing, open parenthesis, close parenthesis Line 2: open brace Line 3: DISPLAY, open parenthesis, open quotation, Do you want to continue playing, open parenthesis, y slash n, close parenthesis, question mark, end quotation, close parenthesis Line 4: response, left arrow, INPUT, open parenthesis, close parenthesis Line 5: IF, open parenthesis, open parenthesis, response equals, open quotation, y, close quotation, close parenthesis, AND, open parenthesis, response equals, open quotation, yes, close quotation, close parenthesis, close parenthesis Line 6: open brace Line 7: RETURN, open parenthesis, true, close parenthesis Line 8: close brace Line 9: ELSE Line 10: open brace Line 11: RETURN, open parenthesis, false, close parenthesis Line 12: close brace Line 13:close brace End program.

Which of the following best describes the result of running the procedure?

A
The procedure returns true when the user inputs the value Open quotation, y, close quotation and returns false otherwise.
B
The procedure returns true when the user inputs the value Open quotation, n, close quotation and returns false otherwise.
C
The procedure returns true no matter what the input value is.
D
The procedure returns false no matter what the input value is.

### Correction:
Answer A
This option is incorrect. The procedure always returns false.

### Question 5:
Directions: The question or incomplete statement below is followed by four suggested answers or completions. Select the one that is best in each case.

A programmer is developing a word game. The programmer wants to create an algorithm that will take a list of words and return a list containing the first letter of all words that are palindromes (words that read the same backward or forward). The returned list should be in alphabetical order. For example, if the list contains the words Open bracket, open quotation, banana, close quotation, open quotation, kayak, close quotation, open quotation, mom, close quotation, open quotation, apple, close quotation, open quotation, level, close quotation, close bracket, the returned list would contain Open bracket, open quotation, k, close quotation, open quotation, l, close quotation, open quotation, m, close quotation, close bracket(because Open quotation, kayak, close quotation, Open quotation, level, close quotation, and Open quotation, mom, close quotationare palindromes).

The programmer knows that the following steps are necessary for the algorithm but is not sure in which order they should be executed.

A table is shown with 2 columns and 4 rows. The first row of the table contains the column headers, from left to right, Step and Explanation. The table is as follows: Shorten, Takes a list of words and returns a new list that contains only the first letter of each word from the input list Keep palindromes, Takes a list of words and returns a list that contains only the palindromes from the input list Sort, Takes a list of words and returns a copy of the list in alphabetical order

Executing which of the following sequences of steps will enable the algorithm to work as intended?

I. First shorten, then keep palindromes, then sort

II. First keep palindromes, then shorten, then sort

III. First sort, then keep palindromes, then shorten

A
I only
B
II only
C
I and III
D
II and III

### Correction:
Answer C
This option is incorrect. Option III works correctly, but option I does not. Option I does not work because it performs the "shorten" step before the "keep palindromes" step.



