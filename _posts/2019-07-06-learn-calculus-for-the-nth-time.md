---
layout: post
subtitle: When 1 thing changes how others change.
tags: [calculus, maths]
comments: true
riemann_sum: /img/calculus/riemann_sum.png
---
I've learned and works with calculus for years, but recently, I re-studied it
for extend my knowledge about it to support my data science career.

Some cool things as below.

## Riemann Sum
___
When I studied integral for the first time, nobody told me about this. What a pity.

The idea of integral comes from calculating area/volumn of some irregular shape/object.
To do that task, we *divide* the shape into smaller pieces, and calculate sum of those.

![Riemann Sum]({{ page.riemann_sum }}#post_img)

To calculate the area below the curve in the figure, we divide it to many rectangles, and
the sum of all areas of those rectangles is *approximately* the area what we need to calculate.

That sum is Riemann Sum, an **approximation** of the integral by a finite sum.

I like how calculus is used for *__approximation__*, because in many cases we can not
or hard to calculate the exact integral of a function. So we use approximation,
we have riemann sum, and depends on how
we divide the curve/shape, how we draw those rectangles, we will have different kinds of
approximations.

We have Left Riemann sum, Right Riemann sum, Midpoint and Trapezoidal sum, four main ways
to *draw* the rectangles.

Another famous method of approximation is Newton method, but I will talk about it later.

## Infinite Series
___
The crazy thing about calculus, I think, laying on infinite series.

The first time I've worked on it, it completely blown my mind. How the hell a sum of an
infinite series can be a finite number. And in physics, some diverge series have sum 
is a finite number too, like $$1 + 2 + 3 + ... = \frac{-1}{12}$$, what the hell.

For basic level, we calculus infinite sum with some basic type of series like

Geometric Series  
$$a + ar + ar^2 + ar^3 + ...$$ with any $$a$$ and $$-1 < r < 1$$

To deal with more complicated series, I need to learn more about complex number, and other
techniques. I'm reading the lecture notes of Feymann for this. And that note is super cool.

Even more insane than anything I've learned is **Riemann series theorem** (Yup, that Riemann
guy again, he's basically one of the greatest mathematicians in the history, so no surprise
he can came up with all of amazing things)  

It says that if an infinite series of real numbers is **conditionally convergent** then
its terms can be **arranged** in a permutation so that 
the new series converges to **any real number**  

Yup, any real number. Basically, give me a conditionally convergent series, I will somehow
arrange its terms to produce for you any real number. Like black magic.

## Vector Field and Gradient
___
When I was taught multivariables calculus, I didn't know about gradient or something like
this. Yup, my bad, a very important thing and I just missed it.

## Lagrange Multipliers
___

## Green's Theorem
___

**_Updating..._**

