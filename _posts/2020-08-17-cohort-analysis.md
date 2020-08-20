---
layout: post
subtitle: How cohort analysis helps to improve retention
tags: [sql, data, index]
comments: true
bigimg: /img/cohort/bg.png
acquisition: /img/cohort/acquisition.png
---

The first data analysis technique I have ever learned is *Cohort analysis*. So what is it and what is it used for?

Imagine you have a fantastic mobile app and it's your start-up product. You do marketing, invite people to use your app, but after a while you realise the number of active users is decreasing.

How can that happen when you regularly promote and acquire new users to your app?

To answer that question, we need to know when people start to leave your app since the first day they installed it.  
And second question, where the users drop the app, which stage of your user flow is wrong.

Cohort analysis is created to answer those questions. So,let's dig deeper into this concept and how to implement it in your application.

____

A **cohort** is a group of people who share a common characteristic or experience within a defined period

For example: people who are born in the same year are the birth cohort. Students who graduated in a same year are a graduated cohort. People who sign up the 1st time in an app in the same day are a sign-up cohort.

Cohort analysis is a study that focuses on the activities of a particular cohort.

For example, we can do cohort analysis to find how user behave after signing up.

![acquisition]({{ page.acquisition }}#acquisition)

Explaination: 
- The users are group by **first date signed up** means there are **1098 new users** sign up for the app on **Jan 25**. Similarly, on Jan 26, there are another **1358 new users signed up**.
- The triangle heat map show us how those users-group behave. In the first line, the group of 1098 users who register on Jan 25, stop using the app in the next day (Jan 26) dramatically by **66.1%** and remain only 33.9 percent. In the next day, it's getting worse when only 23.5% users of those 1098 users are still using the app.
- So thank for the heat map, we can see that after the first day of register, most of group of users are leaving the app. So we answer the question, when our customers leave our platform. The next question is how we investigate that first day of using the app to define why they stop using our app.

**Updating...**

____
READ MORE:  

1. [Why cohort analysis?](https://www.onebigfluke.com/2012/11/why-cohort-analysis.html)

2. [Cohort analysis](https://www.stitchdata.com/cohort-analysis/)

3. [Cohort Analysis: Beginners Guide to Improving Retention](https://clevertap.com/blog/cohort-analysis/)

____