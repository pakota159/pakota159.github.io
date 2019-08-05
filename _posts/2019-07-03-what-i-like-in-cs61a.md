---
layout: post
subtitle: One of the first courses I've learned about computer science
tags: [cs61a, cs, berkeley]
comments: true
---
Back to 2015/16 when I started learning about programming, I did some coding in Python
and Javascript. But later on, I figured out that it's necessary to understand some 
basic/fundamental stuff and follow formal instructions/courses.

That leads me to the UC Berkeley program, although self-learning it online without going
to class is quite challenged and insufficient.

This course is one of the first computer science courses from UC Berkeley that I fortunately
found the resource available on the Internet.

CS61A - Structure and Interpretation of Computer Programs introduces some basic concepts
of computing, programming like abstraction, recursion, scope and so on.

## Functions and Scope
***
In Python, we have some kind of *function* is defined like this:
```python
def square(x):
    return x**2
``` 
What it does is simple: receive an *input* **x** and produce an *output* __$$x^2$$__.

We give the function a *name*, an input or more precisely a *parameter* and that function
will *do something* for us to *return* a result.

That's how I understood the funtion at the very beginning.

I also knew that function is some kind of object, an instruction that is stored at a
memmory address, and whenever the function is **called**, CPU will execute that instruction.
But the details of what happens at low level I'd learned in another course.

At cs61A, what makes me *wow* the most is how people explain the concept of function and how
it work by **environment diagram**.

If we only work with simple, one-level function as *square* above, so no need for environment
diagram here. But what if we have to deal with function that require pass function as parameter,
or return function as output; then call itself inside of itself.

**_Updating..._**