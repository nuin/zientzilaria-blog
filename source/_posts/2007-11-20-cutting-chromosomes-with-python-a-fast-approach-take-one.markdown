---
author: Paulo Nuin
date: '2007-11-20 16:24:11'
layout: post
slug: cutting-chromosomes-with-python-a-fast-approach-take-one
status: publish
title: '"Cutting" chromosomes with Python: a fast approach, take one'
wordpress_id: '72'
? ''
: - Phase 2
---

Last couple of posts we started with some functional programming aspects
of Python. I was away last week and couldn't create anything related to
FP in the meantime, so I decided to post about a quick way to "cut", or
extract segments, from chromosomes stored as FASTA files. This is a
subject that I have been investigating for some time, as I needed a tool
that would get some segment from a chromosome for further analysis. I
have a short C++ code that does the trick and is really fast, but I
wanted to find a Pythonic way of doing it, and quick. I have been trying
different methods but no one were fast. Chromosomes are usually large,
and stored in large files, so reading line by line and using `readlines`
were extremely slow. 

Inspired by a
[post](http://www.goldb.org/goldblog/2007/11/07/PythonProcessingLargeTextFilesOneLineAtATime.aspx)
from Corey Goldberg, I decide to test the method explained there, with
wonderful results. Basically what we need to do is to use an iterator
protocol on the file object 


{% codeblock lang:python %} for line in open('foo.txt', 'r'):{% endcodeblock %} 


This processes the human chromosome 1
(the largest) in less than 2 seconds. Our first take will be how to
extract a segment, but not precisely (that we will see in a future
post). Basically we need a start and an end point and a FASTA file. All
three would be used as parameters and a loop should take care of the
rest. Our script should look like this 

{% codeblock lang:python %}
#! /usr/bin/env python
 
import sys
 
file = sys.argv[1]
start = int(sys.argv[2])
end = int(sys.argv[3])
 
size = 0
segment = ''
for line in open(file, 'r'):
    if not line.startswith('>'):
       size += len(line)
    else:
        name = line
    if size >= start and size <= end:
        segment += line
 
print name, segment{% endcodeblock %} 

We start getting the parameters from
the command line, assigning a couple of variables and we start the loop.
We open the file and use the file object iterator to check each line. We
check each line for a FASTA sequence title. If found we store tht title
in the variable `name`, and if not we check the size of the line and
increment the variable that will guide us on the file position. We use
`size` as a line by line increment and if it is between `start` and
`end` we store the read line into the `segment` variable. That's it. A
few drawbacks with this script: it will fail on FASTA files where the
sequence is stored in one line, there is no precision to get the actual
start and end points and it can only run on unique sequence files. On
the next post we will address some of these concerns.
