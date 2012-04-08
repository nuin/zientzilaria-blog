---
author: admin
date: '2007-02-13 14:24:35'
layout: post
slug: flow-control-in-python
status: publish
title: Flow control in Python
wordpress_id: '15'
? ''
: - Section 2
---

We start following the fifth chapter of BPB. The first item is about
flow control and code layout, which are very relevant for our tutorial.
We already introduced briefly both aspects in past entries on the site,
but it is always good to check. As the book, I will start with flow
control. **Flow control** is the way your instructions are executed by
the program. Most languages have a linear flow control, meaning every
line is executed from top to bottom. This linear flow control can be
disrupted by two types of statements: looping and branching. Looping
statements tell the computer to execute a determined set of commands
until certain condition is met. This can be a numeric value (ie from 1
to 100) or the number of items in a list (like our shop list from
before). Branching statements are also known as conditional statements,
tell the computer to execute/or not determined lines depending on
certain conditions. The `for` loop was shown before. In its for loop
Python iterates over the elements in a list like this [sourcecode
language='python']for lines in text: *do something*[/sourcecode] Notice
that the first line of the loop ends in a colon. This and the word `for`
in the line\> tell the interpreter that this a for loop and the
**indented** block below is the code to be executed repeatedly until the
last element in the list is reached. How Python knows where the loop
ends? Indentation. Many languages use curly braces, parentheses, etc. In
Python the loop ends by checking the indentation level of lines (this
will help us a lot when discussing code layout). We've already seen one
example of loop in Python, `for`, but Python accepts other types of loop
structures, such as `while`, that uses the same indented properties to
execute the commands. [sourcecode]mycounter = 0 while mycounter == 0: do
something[/sourcecode] Take a closer look at the `while` line. See
something different? Maybe not, if you are used to programming. In
Python equality is tested with a double equal sign (`==`), while a sole
equal sign (`=`) assigns a value to a variable. You can also test for
inequality, greater and less than, with `!=`, `<` and `>` respectively.

> Attention: is quite common to generate errors by substituting `==` by
> `=`, so pay attention when coding.

Branching statements are the conditional commands in a computer
language, usually governed by `if ... then ... else`. In Python a
branching statement would look like [sourcecode language='python']if
value == 1: do something elif value == 2: do something else else: do
even more[/sourcecode] Notice the colon ending each line of the
conditions and again the indented code, telling the interpreter where
the corresponding code for each condition ends. We are going to use a
lot of conditions and loops, but as you might have noticed Python has
some tricks that make us avoid these statements. About **code layout**
just one word: indentation. No brackets, parentheses, curly braces, etc.
Yes, we have seen brackets and parentheses, but not to tell the
interpreter where loops and conditions start and end. This is taken care
by indentation, making our life easier and the code more beautiful. Next
we will see Python's ability to find motifs in words, mainly on DNA
sequences.
