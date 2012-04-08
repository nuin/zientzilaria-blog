---
author: admin
date: '2009-02-09 13:29:24'
layout: post
slug: expert-python-programming-by-tarek-ziade-a-review-of-chapter-3
status: publish
title: Expert Python Programming by Tarek Ziadé - a review of Chapter 3
wordpress_id: '237'
? ''
: - off topic
---

The chapter 3 review that I promised for "tomorrow" (last Saturday) was
lazily postponed until today. So, let's get to it. Tarek in this chapter
continues with syntax best practices, but at this time at class level.
As expected the chapter requires that you have a minimal knowledge of
Python classes, so I can say it's geared to somewhat experienced
programmers, and not to newcomers. There is a short explanation on
sub-classing that warms up things for the next sections. Next is the
built-in method (type?) `super`, which was new to me. Basically `super`
gives you access a method or attribute of a class by calling its parent
directly. This is a segue into understanding the Method Resolution Order
in Python, which is understanding which class has precedence over the
others. For me, I haven't dealt with such structures before it was a
good and straight explanation, especially when he explains about
possible pitfalls of using `super`. A short list of best practices
helps:

-   -   Multiple inheritance should be avoided:
-   super usage has to be consistent: Mixing super and classic calls is
    a confusing practice.
-   Don't mix old-style and new-style classes
-   Class hierarchy has to be looked over when a parent class is called

After dealing with MRO, comes what I think is one of the best sections
of the book so far, where Tarek explains about object descriptors and
gives a little bit of the Python's approach to introspection. This short
section is basically all code, but it's good to have a good best
practices reference, including here properties and slots. The last part
of the chapter covers meta programming, and as Chris pointed in the
comments, that's a difficult area of Python (maybe for the ones like me
that don't have a CS formation). I would have to try the examples by
hand and maybe define areas in my code where I can use it, so to take
fully advantage and fully understand it. Overall, the chapter gives a
good series of topics about Python classes and I enjoyed learning a
little bit more things that I couldn't understand previously. Next we
will see a review of chapter 4, that deals with PEP 8 and naming best
practices.
