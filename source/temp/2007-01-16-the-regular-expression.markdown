---
author: admin
date: '2007-01-16 13:49:07'
layout: post
slug: the-regular-expression
status: publish
title: The Regular Expression
wordpress_id: '9'
? ''
: - python
  - regular expression
  - Section 1
---

As mentioned above, regex in Python are provided by the `re` module,
which provides an interface for the regular expression engine. First
thing we have to do is to tell the interpreter what to do and what
expression to use. Let's start with a DNA sequence. [sourcecode
language='python']myDNA = 'ACGTTGCAACGTTGCAACGTTGCA'[/sourcecode] How to
transcribe it to RNA? Transcription creates a single-strand RNA molecule
from the double-strand DNA; basically the final result is a similar
sequence, with all `T`'s changed to `U`'s. So our regular expression has
to find all `T` nucleotides in the above sequence and then replace them.
Regular expressions in Python need to be compiled into a RegexObject,
that contains all possible regular expression operations. In our case we
need to search and replace, what can be done by using the `sub()`
method. According to the Python's [Regular Expression
HOWTO](http://www.amk.ca/python/howto/regex/regex.html) `sub()` returns
the string obtained by replacing the leftmost non-overlapping
occurrences of the RE in string by the replacement replacement. If the
pattern isn't found, string is returned unchanged. Let's put everything
above in real code. First we need to compile a new RegexObject that will
search for all thymines in our sequence. It can be achieved by using
this: [sourcecode language='python']regexp =
re.compile('T')[/sourcecode] Simple as that. This line of code tells the
Python interpreter that our "regular expression" is every T in our
string. Now, we have to make replace those Ts with Us. In order to do
that we just tell the interpreter: [sourcecode language='python']myRNA =
regexp.sub('U', myDNA)[/sourcecode] Let's look at the last two lines of
code. On the first line we created a new RegexObject, `regexp` (that
could have any name, as any variable) and compiled it, making our
regular expression to be every T in our string. On the second line, we
assigned our soon to be created RNA sequence to a new string (remember
that strings in Python are immutable) and used the command `sub` to
replace in the Ts by Us present in our original DNA string. Putting all
together our transcription code will be [sourcecode
language='python']\#! /usr/bin/env python import re myDNA =
'ACGTTGCAACGTTGCAACGTTGCA' regexp = re.compile('T') myRNA =
regexp.sub('U', myDNA) print myRNA[/sourcecode] You can download the
resulting script [here](http://python.genedrift.org/codepy/code_03.py).
