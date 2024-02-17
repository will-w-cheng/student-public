---
toc: True
comments: True
layout: post
title: Computing Bias
description: Computing Bias
type: hacks
courses: {'csp': {'week': 13}}
---

# Big Idea 5.3 Computing Bias- Tanay

Overview/Definition: Computing Biasses are the numerous Biasses in application that are based on human prefrences.

- Computing innovations can reflect existing human biases because of biases written into the algorithms or biases in the data used by the innovation
- Programmers should take action to reduce bias in algorithms used for computing innovations as a way of combating existing human biases
- Biases can be embedded at all levels of software development

## Types of Computing Bias - Tarun

- Data Bias: The data does not accurently represent the values of the real world
    ex. If data is taken from a sample size that doesn't reflect the actual population
        - If you wanted data to represent the population in America but your sample that is being surveyed is from a Texas. The population in Texas does not accurately reflect the entire population of America. 
- Human Bias: Those who make programs may be influenced by their own biases 
    ex. If a development team are experts in using a certain language and their algorithm demonstrates that language, they will feel that people who specialize in that language are qualified and better. This is essentially bringing in their personal biases and applying to a larger amount of people. 

## Explicit data vs Implicit data:  - Pranavi

Explicit data:
- takes the data that you give
- When watching a video, and it asks "are you enjoying this?", and you respond with either a thumbs up or down, you are giving them explicit data

Implicit data:
- When you watch or search up certain things, data can be deduced on what is the "norm" for the person

Example: Netflix
- When browsing through Netflix, they show Netflix exclusives, they do this because they want your subscriptions 
- showing the netflix exclusives is the bias in this scenario

![Screenshot 2023-12-12 at 1.22.41 PM.png](<attachment:Screenshot 2023-12-12 at 1.22.41 PM.png>)



```python

```

## Popcorn Hack:

In what other applications could have intential bias?
- Other applications that could have intentional bias includes the Chinese version of google, Baidu. Baidu filters out a lot of applications and in general will collect a lot of bias data that directly benefit's the Chinese government of the CCP. 

## Intentional Bias vs Unintentional Bias - Tanvi

Example 1: Hypothetical Loan company
- Suppose a software was created to assist loan officers, and certain trends of successful loans were taken
- If people are rejected of those who don't fit in their trends of either age, gender, race, etc.
- This software is biased in the way that it only chooses candidates who will have higher chances in successful loans

Example 2: Candy Crush vs Call of Duty
- Call of Duty is geared towards the teenage boy demographic, 18-24, with more grunge type of music
- Candy Crush is more visually appearing to younger audience as it includes pictures of candies and playful music 
- This is biased as the games include aspects and characteristics that will seem appealing to a specific audience 

![Screenshot 2023-12-12 at 1.23.36 PM.png](<attachment:Screenshot 2023-12-12 at 1.23.36 PM.png>)

![Screenshot 2023-12-12 at 1.23.42 PM.png](<attachment:Screenshot 2023-12-12 at 1.23.42 PM.png>)


## Popcorn Hack:
How is their unintentional bias in apps such as TikTok or Instagram or otehr social media apps?

- Unintentional bias in apps such as TikTok or Instagram

## Mitigation Strategies - Shubhay 

- Utilize data from various sources
- Pre-Processing: A way to check the inputs for bias before it is being used as data
- In-processing: This algorithm changes the data during analysis of the data to keep the data consistent
- Post-Processing: # step check to make sure the model is fair and accurate
    - Input Correction: This strategy makes adjustments to the data to make the data more comparable
    - Classifier Correction: polishing and adjusting the algorithm after it has been trained to reduce the biases
    - Output Correction: The predictions made by the model is modified to eliminate biases

## Homework:

1. Is bias enhancing or intentionally excluding?
- Bias can be  unintentionally introduced and can modify certain perspectivve or groups over others. For example, if a recommendation algorithm learns from European historical data that favors a particular group, it may unintentionally favor the bias of Europeans and may develop an extremely Eurocentric view. Bias can be deliberately introduced to exclude or marginalize certain groups. A prime example of intentional bias is Baidu which is monitored by China's CCP.
2. Is bias intentionally harmful/hateful? 
- Bias becomes a concern when it leads to unfair or discriminatory treatment of individuals or groups. In some cases, bias can be unintentional, stemming from ingrained cultural or societal norms. However, when biases are intentional and result in harmful actions or decisions, they can be considered harmful or even hateful. For example, in the example I gave above having bias data collection for an AI to analyze may make it more prejudice and favor European people that experience Eurocentric views. 
3. During software development are your receiving feedback from a wide variety of people?
- During software development you should collect feedback from a wide variety of people. Different individuals bring diverse perspectives based on their backgrounds, experiences, and expertise. This diversity can help uncover blind spots, identify potential biases, and bring in fresh ideas.Engaging with a diverse user base ensures that the software is accessible and inclusive. Feedback from users with different abilities and needs can lead to improvements in usability and accessibility features.
4. What are the different biases you can find in an application such as Youtube Kids?
- The content recommendation algorithm may intentionally favor certain types of content over others, leading to a bias in the types of videos that are suggested to children. This allows for youtube to still monopolize on their target but specifically make their application to filter to more appropriately for kids

Answer in complete sentences, due Sunday 11:59 pm
