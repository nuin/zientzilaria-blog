---
author: admin
date: '2008-12-06 11:07:08'
layout: post
slug: scripts-and-python-30-part-1
status: publish
title: Scripts and Python 3.0, part 1
wordpress_id: '206'
? ''
: - print
  - Python 3.0
  - python2.x
  - python3.0
---

Yes, Python 3.0 was released earlier than Perl ... what version was it?
6? 7? Anyway, I decided to go back to most of the scripts that were
posted here. In the github repo we have 50 files in the "original
scripts" directory. Let's check how do they fare on Python 3.0 and what
type of changes we need to do in order to make them work. Starting with
code\_01.py, which is a couple of lines long [sourcecode
language='python']myDNA = "ACGTACGTACGTACGTACGTACGT" print
myDNA[/sourcecode] Here we have one of the most evident differences
between Python 2.x and 3.0. Now `print` is a [function not a statement
anymore](http://docs.python.org/dev/3.0/whatsnew/3.0.html#print-is-a-function),
so whatever we want to print now should be passed as a function
parameter. The above code would be changed to [sourcecode
language='python']myDNA = "ACGTACGTACGTACGTACGTACGT"
print(myDNA)[/sourcecode] That simple ins this case. But what are the
advantages of `print` being a function over a statement? More
flexibility, as can be seen in the link above. It is possible now to
send different parameters to print and make the output richer by
customizing separators between items, directing the output, etc. A
similar change would have to be made n our code\_02.py. There are two
`print` statements there that should be translated to the function.
Trivial, so far. The original code [sourcecode language='python']myDNA =
"ACGTACGTACGTACGTACGTACGT" myDNA2 = "TCGATCGATCGATCGATCGA" print "First
and Second sequences" print myDNA, myDNA2 myDNA3 = myDNA + myDNA2 print
"Concatenated sequence" print myDNA3[/sourcecode] and to work on Python
3 [sourcecode language='python']myDNA = "ACGTACGTACGTACGTACGTACGT"
myDNA2 = "TCGATCGATCGATCGATCGA" print("First and Second sequences")
print(myDNA, myDNA2) myDNA3 = myDNA + myDNA2 print("Concatenated
sequence") print(myDNA3)[/sourcecode] This is would be the biggest (or
at least the most common) change that we would need to make in the
scripts posted here. Follow the repo to get the newer versions.
