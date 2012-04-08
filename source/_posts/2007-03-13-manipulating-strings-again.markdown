---
author: admin
date: '2007-03-13 14:30:54'
layout: post
slug: manipulating-strings-again
status: publish
title: 'Manipulating strings: again'
wordpress_id: '24'
? ''
: - Section 2
---

As I have not updated the website in a couple of weeks, I will try to
catch up with the book instead of revisiting (for the time being) our
past scripts. I am going to finish the book's chapter 5 (our section 2)
in the next post, where I will give a small introduction on how to
output data to a file in Python. On this post we will check some of the
methods that can be used to manipulate strings. The book gives only a
couple of methods to be used in perl on string, but here I will show a
longer list of Python methods that can be used on its immutable strings.

A full list of the methods can be found
[here](http://docs.python.org/lib/string-methods.html) and I will will
give brief explanations on the ones I think are key for bioinformatics.

Remember that string cannot be changed in Python, so we will always
going to use a buffer/temp variable to store our changed string when
needed. - **count** this method returns the number of times you see a
substring (a letter/number, a word, etc) in another string. You can also
specify a start and an end positions to look for. This is handy if you
are counting nucleotides/aaminoacids in a sequence. This method returns
an integer - **endswith** this method checks the end of your string for
a determined substring. Very handy of you need to check the tail end of
your sequence right away. - **find** returns the position of the
substring being searched, and -1 if it is not found. It is similar to
the re.search we used before. This is very useful if you are looking for
a determined motif/subsequence in a hurry. - **islower** returns a true
bool (true or false) if all characters in the string are lowercase.
False if at least one of the characters is uppercase. Very handy if you
need to convert lowercase to UPPERCASE files for input in some
application. Works in conjunction with the **isupper** which is
basically the opposite. - **join**. We have seen this before: it
concatenates strings using a determined separator. - **lower** and
**upper**, that as their name might indicate return the string converted
to lowercase/uppercase.This is also good for the conversion of sequence
format in input files. 

I will stop here. There are many other methods
that can be used. Some of the above were already covered here and in the
next posts we will take a look at the other ones, creating an
application that actually performs some useful function.
