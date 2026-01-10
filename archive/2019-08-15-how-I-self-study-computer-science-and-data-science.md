---
layout: post
subtitle: "The Lord of self-studying: The Fellowship of studying"
tags: [cs, learning, data]
comments: true
bigimg: /img/note/bg.png
note1: /img/note/note1.jpeg
note2: /img/note/note2.jpeg
---
Today, a friend asked me how to study computer science well - a popular question
that many others wonder too. Thus, I decided to write an **all-in-one
note** to explained detailed about learning computer science and data science as well.
I'm not excellent in computer science at all, and this note is only sharing some
experiences I have.

### Before you start
___
Knowing where you are is important. You need to understand how much cs knowledge
you have. This journey is long and exhausted but I can ensure it'll be fun as well, 
if you really like those stuff.

Prepare some things:
- A notebook and a pen to note and **visualize** important things 
while you learn such as how HTTP requests are sent and received, 
how CPU and RAM works, and so on. Visualization always helps you understand
things faster and easier. Examples: Some things I drew when learning about
CPU and RAM

![note1]({{ page.note1 }}#post_img)

![note2]({{ page.note2 }}#post_img)

- A laptop/computer with Linux/OSX operation system. Yup, you can use Window
if you like, but I prefer Linux to learn programming.

- A lot of time

- And last but not least, a superior unbreakable **persistent mind**

There are 3 parts of this note:
- Learning **Maths**

- Learning **Computer Science**

- Learning **Data Science**

Maths is basic stuff that support everything else, so I put it into an independent part.

> All 3 parts will only contains *materials* which I *personally* like and find them useful
the most.

> **Bold courses** are must-taken or you should be familiar with the outcomes of those courses (so you don't have to re-take it).  
Other courses are useful and good to learn.

### Learning Path
___

For whom want to learn programming applied in non-cs area (like business, finance, health care, ...)
this is learning path I think able to help you learn effectively.

1. Read 2 starter books
2. Do maths courses **Math_01** -> **Math_02** -> **Math_03** or make sure you understand all the conceps in each course.
3. Do core courses in Computer Science: **1** -> **2** -> **3** -> **8** (in course 8 only need Lecture 1 to 8)
4. Learn Python: **Py_2** -> **Py_5** (do all projects)
5. Learn DS and Algorithm: **Al_01** -> **Al_02** -> **Al_05**
6. Do real projects

To get some certifications, some courses below are recommend:
1. Algorithms: <https://www.coursera.org/specializations/algorithms> Standford Course - Intermediate Level
**You should learn basic algorithms before taking this one** Example: Al_01 is good start.
2. C Programming: <https://www.edx.org/professional-certificate/dartmouth-imtx-c-programming-with-linux> Dartmouth Course - Intermediate Level
At least you should read the book **C_1** in C sections below before take this course.
Self-pace and **$308** fee
3. C++ Programming: Series 3 courses from Microsoft  
Intro C++ <https://www.edx.org/course/introduction-to-c-5>   
Intermediate C++ <https://www.edx.org/course/intermediate-c-3>   
Advanced C++ <https://www.edx.org/course/advanced-c-3>  
4. Python: <https://www.coursera.org/specializations/data-science-python> Python for data science series from University of Michigan  

### Mathematics
___
The courses below should be taken in order.

|No.| Course | Link | What you expected to learn |
|----- | ------ |--- | --- |
|**Math_01**| **Single Variable Calculus** | <https://ocw.mit.edu/courses/mathematics/18-01sc-single-variable-calculus-fall-2010/> | Limit, Derivatives, Chain Rules, Approximation, Mean Value Theorem, Riemann Sums, The Fundamental Theorem of Calculus, Integrals and Application, L'Hospital's Rule, Infinite Series, Taylor's Series|
|**Math_02**| **Multivariable Calculus** | <https://ocw.mit.edu/courses/mathematics/18-02sc-multivariable-calculus-fall-2010/> | Vectors and operators on vectors, Determinants and Matrices (Basics), Partial Derivatives, Second Derivative Test, Total Differentials and the Chain Rule, Gradient, Lagrange Multipliers, Double Integrals, Vector Fields, Curl, Green's Theorem, Triple Integrals, Flux, Stokes' Theorem| 
|**Math_03**| **Math 54 Linear Algebra and Differential Equations** | <https://math.berkeley.edu/~apaulin/54_002(Spring2018).html> | Vectors Spaces and Linear transformations, subspaces, kernels, range, eigenvalues and eigenvectors, The Gram-Schmidt Process, Least-Squares Problems, Linear Systems of Differential Equations, Fourier Series |
|**Math_04**| Math 55 - Discrete Mathematics (useful for computer science. If you learn cs70 below, you don't really need this) | <https://math.berkeley.edu/~williams/55.html> | Propositional logic and equivalences, Sets and set operations, Functions, sequences, cardinality, Solving congruences, Mathematical induction, recursive, Counting, Permutations and combinations, Graphs and graph models, Graph isomorphism |

### Computer Science
___
#### Before studying courses

You need to read a few books to understand the big pictures of computer science. And read those books
in the order too.

1. _**Code: The Hidden Language of Computer Hardware and Software**_  
A great book that provides you the first sense of computer science, what is binary,
how machine understand something like binary and more.  
I like how authors respresent physics mechanism of computer here, so if you are not
so good at physics, this book is even better for you.
This book is only 400 pages long, easy to read, therefore I highly recommend it as
your first read when start learning cs.

2. _**Structure and Interpretation of Computer Programs**_  
A legendary book, SICP is kind of book that is recommended from everywhere in cs world.
It covers a lot of programming aspects from functional programming, abstraction, instruction processor
to compilers. This might be quite hard for complete beginner and because this book is used Scheme programming language
, it's pretty hard to read as well.

#### Jump into some courses
___

> **Disclaimer**: There are many things have not covered in this path yet (after complete CS61 series).
So if you want to discover other courses about security, networks, machine learning, looking for it
on Internet or search in this awesome guide <https://hkn.eecs.berkeley.edu/courseguides>

#### 1. **CS50's Introduction to Computer Science - Harvard**
> Link: <https://www.edx.org/course/cs50s-introduction-computer-science-harvardx-cs50x>

Arguably the best intro course for cs I've ever learnt.

>>What you can learn from it:
- basic understanding of computer science and programming
- basic algorithms and solving problem thinking
- some concepts like abstraction, data structures, encapsulation, web development
- learn Python, C, Sql, Javascript

#### 2. **CS 61A Structure and Interpretation of Computer Programs - Berkeley**
> Link: <https://inst.eecs.berkeley.edu/~cs61a/sp15/>

A truly great course which makes me extremely eager to learn everything from Berkeley. However, to
really enjoyed it as well as get useful knowledge, you need to put a quite large amount of effort, should definitely commit to do all the homeworks, assignments,
and take all the exams. Might take you few months to actually get things done.

>>What you can learn from it:
- Python and its implementation
- Higher-Order Functions, Recursion, Environment diagrams, 
- Data Abstraction
- Scheme, Exceptions, Iterators, Streams, SQL

#### 3. **CS 61B Data Structures - Berkeley**
> Videos: <http://www.infocobuild.com/education/audio-video-courses/computer-science/cs61b-spring2015-berkeley.html>  
Courses: <http://datastructur.es/sp15/>

This one is quite hard for me because I don't like learning Java much. But I think it's useful
if you want to learn data structure.

>>What you can learn from it:
- Basic Java
- Some data structures like Lists, Abstract Classes, Trees, BST, Graphs
- Some algorithms like Sorting and Algorithmic Bounds

#### 4. **CS 70 Discrete Mathematics and Probability Theory - Berkeley**
> Videos: <http://www.infocobuild.com/education/audio-video-courses/computer-science/CS70-Spring2015-Berkeley/lecture-01.html>  
Courses: <https://inst.eecs.berkeley.edu/~cs70/sp15/>

I've not done this course, discrete maths is cool and probability is interesting so I'll finish this course soon.

>>What you can learn from it:
- Induction and Recursion
- Graphs, Eulerian Tour
- Modular Arithmetic
- Polynomials, Secret Sharing, Erasure Codes
- Probability: Counting, Sample Spaces, Events, Independence, Conditional Probability
- Inference

#### 5. **CS 61C Great Ideas in Computer Architecture (Machine Structures) - Berkeley**
> Videos: <http://www.infocobuild.com/education/audio-video-courses/computer-science/cs61c-spring2015-berkeley.html>  
Courses: <http://inst.eecs.berkeley.edu/~cs61c/sp15/>

My favorite one, because you will learn a lot about how machine works under the hood. Not dig too deep but quite good.

>>What you can learn from it:
- C programming
- Assembly Language, MIPS Intro

#### 6. **CS 162 Operating Systems and Systems Programming - Berkeley**
> Videos: <http://www.infocobuild.com/education/audio-video-courses/computer-science/cs162-spring2015-berkeley.html>  
Courses: <https://inst.eecs.berkeley.edu/~cs162/sp15/>

A very tough course that I've finished yet. More details about operating system than cs61c.

>>What you can learn from it:
- Processes, Fork, I/O, Files 
- Thread, Scheduling, Address Translation, Caching
- Performance, StorageDevices, Queueing theory
- Distributed Systems, TCP/IP

#### 7. **CS164 Programming Languages and Compilers - Berkeley**
> Videos: <http://www.infocobuild.com/education/audio-video-courses/computer-science/cs164-spring2012-berkeley.html>  
Courses: <https://sites.google.com/a/bodik.org/cs164/>

I have not learned this course, but knowing about programming languages and compilers surely useful for being software engineer.

>>What you can learn from it:
- Unit Calculator 
- Scoping and desugaring
- Coroutines and Lazy Iterators
- Regular expressions
- CYK and Earley Parsers

#### 8. **CS169 Software Engineering - Berkeley**
> Videos: <http://www.infocobuild.com/education/audio-video-courses/computer-science/cs169-spring2015-berkeley.html>  
Courses: <https://sites.google.com/site/ucbcs169fa15/lectures>

I have not learned this course, just read the syllabus and think this's practical and useful.

>>What you can learn from it:
- Unit Testing 
- Git
- UML
- Software processes
- MVC, Web development

___
#### Strengthen your knowledge

I will consider 8 courses above are core courses that you should take all of those seriously.
After that, you now have good understanding about computer science and ready to improve yourself
even more.

The first thing I want to dig into is **programming language**, I'm gonna cover few most popular ones
like C, C++, Python.

To practice coding, you should join some popular competitive coding sites like <https://codeforces.com>,
<https://www.topcoder.com/> and practice there, quite helpful.

|No.| Language | Books/Course | Link | What you expected to learn | Hard Level |
| ----- | ------ |--- | --- | --- | --- |
| C_1 | C | Dennis M. Ritchie - The C programming language | <https://www.amazon.com/Programming-Language-2nd-Brian-Kernighan/dp/0131103628> | Most popular C book out there, nothing much to talk, it's great, I learned basic concepts about C here. It's short and don't take much time to read | ★★☆☆☆ |
| C_2 | C | Practical Programming in C | <https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-087-practical-programming-in-c-january-iap-2010/assignments/> | A course about C from MIT, not much teaching material but good practice problems with solutions | ★★★☆☆ |
| C++_1 | C++ | Learn C++ | <https://www.learncpp.com/> | Great and detailed tutorial about C++ | ★★☆☆☆ |
| C++_2| C++ | Accelerated C++ | <https://www.amazon.com/Accelerated-C-Practical-Programming-Example/dp/020170353X> | Practices and examples | ★★★☆☆ |
| C++_3| C++ | The C++ Programming Language | <https://www.amazon.com/C-Programming-Language-4th/dp/0321563840/> | Detailed book from author of C++ itself, well-explained | ★★★☆☆ |
| Py_1 | Python | Official Docs | <https://docs.python.org/3/tutorial/index.html> | This's where I've started learning Python, detailed, up-to-date | ★★★☆☆ |
| Py_2 | Python | Learn python the hard way | <https://learnpythonthehardway.org/python3/> | Simple intro to python | ★☆☆☆☆ |
| Py_3 | Python | Real Python | <https://realpython.com/> | Detailed examples for you to practice | ★★☆☆☆ |
| Py_4 | Python | Full stack Python | <https://www.fullstackpython.com/> | Help you learn what need to build Python app | ★★★★☆ |
| Py_5 | Python | Automate the Boring Stuff with Python | <https://automatetheboringstuff.com/> | Learn build Python cool stuff | ★★☆☆☆ |

Secondly, we need to learn more about **data structure and algorithm**

| No.| Books/Course | Link | What you expected to learn |
| ----- | ------ |--- | --- |
| Al_01 | Introduction to Algorithms | <https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-006-introduction-to-algorithms-fall-2011/> | Basic about algorithms from MIT |
| Al_02 | Design and Analysis of Algorithms | <https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-046j-design-and-analysis-of-algorithms-spring-2015/index.htm> | Part 2 from the MIT series, more advanced algorithms: divide and conquer, dynamic programming, complexity and so on |
| Al_03 | Advanced Algorithms | <https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-854j-advanced-algorithms-fall-2008/> | Part 3 from MIT series with advanced algorithms |
| Al_04 | Data Structures and Algorithms - Richard Buckland | <https://www.youtube.com/playlist?list=PLE621E25B3BF8B9D1> | Basic data structures |
| Al_05 | CS 186: Introduction to Database Systems | <http://www.infocobuild.com/education/audio-video-courses/computer-science/cs186-spring2015-berkeley.html> | Database management system, SQL and so on |

### Data Science
___

>**Probability and Statistics**

#### 1. Probability and Statistics - Stanford Online Lagunita
Link: <https://lagunita.stanford.edu/courses/course-v1:OLI+ProbStat+Open_Jan2017/about>


#### 2. Probabilistic Systems Analysis and Applied Probability
Link: <https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-041sc-probabilistic-systems-analysis-and-applied-probability-fall-2013/>  
This course and the standford one can be taken seperately (you can choose one of them, it's ok too).
But for me, I take both of those and study at the same time.
The MIT course is more engineering and the Standford course is more statistics.


