---
author: admin
date: '2007-02-07 13:56:59'
layout: post
slug: reading-files-in-python-using-lists
status: publish
title: 'Reading files in Python: using lists'
wordpress_id: '12'
? ''
: - bioinformatics
  - list
  - python
  - read files
  - Section 1
---

Let's improve our previous script and put the contents of the file in a
variable similar to an array. Python understands different formats of
compound data types, and `list` is the most versatile. A `list` in
Python can be assigned by a series of elements (or values) separated by
a comma and surrounded by square brackets

{% codeblock lang:python %}shoplist = ['milk', 1, 'lettuce', 2, 'coffee', 3]{% endcodeblock %}

Now, we are going to read the same file and store the
DNA sequence in a `list` and output this variable. The beginning of the
script is the same, where we basically tell Python that the file name is
AY162388.seq.

{% codeblock lang:python %}\#! /usr/bin/env python
dnafile = "AY162388.seq"{% endcodeblock %}

We are going to change the way we
read the file. Instead of just opening and then reading line-by-line, we
are going to open it a read all the lines at once, by using this


{% codeblock lang:python %}file = open(dnafile,'r').readlines(){% endcodeblock %}

Notice the part in bold? In the previous
script, we open and store the contents of the file in a `file object`.
Now , we are opening the file and just after it is opened, we are
reading all the lines of the file at once and storing them in
`file object`, but is a Python's `list` of strings. Before, if we
wanted to manipulate our DNA sequence, we would had to read it, and then
in the loop store in a variable of our choice. In this script, we do
that all at once, and the result is a variable that we can change the
way we wanted. The code without the output part is

{% codeblock lang:python %}\#! /usr/bin/env python 
dnafile = "AY162388.seq"
file = open(dnafile, 'r').readlines(){% endcodeblock %}


Try putting a `print`
statement after the last line to print the `file` list. You will get
something like this

`['GTGACTT...TTGTTC\n', 'TTTAAATA....TAATC\n', 'AGTGA...CTATG\n', 'GAGCTCA....TATAGC\n', ...]`

which is exactly the description of a Python's list. You see all lines,
separated by comma and surrounded by square brackets. Notice that each
line has a carriage return (`\n`) symbol at the end. Let's make
the output a little nicer including a loop. Remember when I introduced
loop I wrote that Python iterates over "items in a sequence of items",
what is a good synonym for `list`. So the loop should be as
straightforward as 


{% codeblock lang:python %}for line in file:
    print line{% endcodeblock %}

Putting everything together gives us

{% codeblock lang:python %}
\#! /usr/bin/env python
dnafile = "AY162388.seq"
file = open(dnafile, 'r').readlines()
print file
for line in file:
    print line{% endcodeblock %}

