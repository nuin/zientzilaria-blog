---
author: admin
date: '2007-03-22 09:04:10'
layout: post
slug: python-functions-simple-example
status: publish
title: 'Python functions: simple example'
wordpress_id: '26'
? ''
: - Section 3
---

Python subroutines do not exist. [Everything is a function, all
functions return a value (even if it's None), and all functions start
with `def`](http://www.diveintopython.org/getting_to_know_python/declaring_functions.html).
This statement is from Dive into Python, a book on Python programming
available for free. As mentioned Python functions start with the word
`def`, which is followed by the function name that is followed by the
arguments the function receives in between parentheses. Something like
{% codeblock lang:python %}def my_first_function(somevalue):{% endcodeblock %} 


Usually Python coders
(sometime called Pythonistas, among others), following the Python coding
style (that states: *Function names should be lowercase, with words
separated by underscores as necessary to improve readability*) name
their functions with words separated by underscores. And we are going to
use this style here, whenever a function becomes handy. The parameters
passed to the function (above `somevalue`) do not have a datatype,
Python should handle it whatever is being passed. It is also attribute
of your code to handle the parameter/value passed inside the function
and avoid errors. Functions also follow the same indentation of normal
programming and the line after the declaration should be indented with
four spaces 

{% codeblock lang:python %}def my_first_function(somevalue):
    do_something{% endcodeblock %}

So, let's
warmup with functions. The following script is just the start: it adds a
poly-T tail to a DNA sequence. We are going to use our old friend
AY162388.seq. I will be back after the script 


{% codeblock lang:python %}#! /usr/bin/env python
def add_tail(seq):
    result = seq + 'TTTTTTTTTTTTTTTTTTTTT' 
    return result

dnafile = 'AY162388.seq'
file = open(dnafile, 'r')
sequence = ''
for line in file:
    sequence += line.strip() 
    print sequence 
    sequence = add\_tail(sequence)
    print sequence{% endcodeblock %}

Not very useful, at first sight, but gives us an
impression of what a function looks like. Basically we define a function
`add_tail` that receives `seq` as a parameter. Don't worry about
variable scope now, we will see it later. The rest of the script is just
like things we saw before, except for the line
`sequence = add_tail(sequence)`. Here we are saving memory (yep, not
that much and not even impressive) by assigning the return value of the
function to the same string where we have the sequence stored. Run the
scritp and get ready for the command line arguments.
