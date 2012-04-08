---
author: admin
date: '2007-02-09 14:01:39'
layout: post
slug: manipulating-python-lists-i
status: publish
title: '"Manipulating" Python lists I'
wordpress_id: '13'
? ''
: - Section 1
---

Now, I want to manipulate my DNA sequence, extract some nucleotides,
check lines, etc. Simple things. We start with the same basic code to
read the file: [sourcecode language='python']\#! /usr/bin/env python
dnafile = "AY162388.seq" file = open(dnafile,
'r').readlines()[/sourcecode] Our nucleotides are stored in the variable
`file`. Remember that each line is one item of the list and the lines
still contain the carriage return present in the ASCII file. Let's get
the first and the last lines of the sequence. The first line is easy to
get, as Python's lists start at 0. To access one list item just add
square brackets with the index number of the item you want to get (this
is also known as slicing). Something like this [sourcecode
language='python']file[0][/sourcecode] will return the item 0 from the
list, that in our case is the firs line of the sequence. If you add a
`print` command [sourcecode language='python']print file[0][/sourcecode]
you should expect `GTGACTTTGTTCAACGGCC....CGTAATCACTTGTTC` The last line
is a little bit trickier. Let's assume that we don't know the number of
lines in the list, and here we want to make our script as general as
possible, so it can handle some simple files later. It is also good code
practice to think ahead and plan what you want, first to have a detailed
project to follow, and second it allows you to be prepared to
errors/bugs that your code might have or situations not expected in your
original plan. In our file, we have **eight** lines of DNA, so it would
be just adding this `print file[7]` and we would output the last line.
But, the right way to do it is to check the length of the list and
output the item which has an index equal to the list length. In Python,
you can check the length of a list by adding the built-in function `len`
before the list name, like this [sourcecode
language='python']len(file)[/sourcecode] So who do we print the last
line of our sequence? Simple. `len(file)` should return an integer of
value 8, which is the actual number of elements in our list. We already
know that to access any item in a list we just add its index (that has
to be an integer) to the list name. One idea then would be to use
`len(file)` as the index, like this [sourcecode language='python']print
file[len(file)][/sourcecode] Why would that be wrong? Our list has eight
items, but the indexes are from 0 to **7**. So eight would be one index
over the list length, which is not accessible because it does not exist.
Solution? Let's use the list length minus one: [sourcecode
language='python']print file[len(file)-1][/sourcecode] and there you
are, the last line of the sequence. But as we want the last line of the
file, which is a list there is an easier way to output just the last
line: [sourcecode language='python']print file[-1][/sourcecode] which
tells the interpreter to print the last item of a list. Putting
everything together, we have [sourcecode language='python']\#!
/usr/bin/env python dnafile = "AY162388.seq" file = open(dnafile,
'r').readlines() print 'I want the first line' print file[0] print 'now
the last line' print file[-1][/sourcecode] Two points worth mentioning:
differently of strings, Python's lists are mutable, items can be
removed, deleted, changed, and strings also can be sliced by using
indexes that access characters. Next we will see some more features of
lists and strings, and how to manipulate them. It will probably be the
last entry in the first section as we finish the Chapter 4 in the book.
As you may have noticed some items in the perl book will not be covered,
at least not immediately. We will jump back and forth sometimes.
