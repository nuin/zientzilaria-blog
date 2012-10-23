---
author: Paulo Nuin
date: '2007-11-26 16:41:57'
layout: post
slug: '%e2%80%9ccutting%e2%80%9d-chromosomes-with-python-a-fast-approach-take-two-including-precision'
status: publish
title: '“Cutting” chromosomes with Python: a fast approach, take two, including precision'
wordpress_id: '73'
? ''
: - bioinformatics
  - chromosomes
  - cut
  - Phase 2
  - python
---

On the last post we saw how to "cut"/extract a segment of a chromosome
quickly in Python. But our last code had no precision in the
cutting/extracting, because it didn't take in account the line size so
it would extract more information than actually requested. We need to
address precision them. First take into account the size of each line,
the number of nucleotides on each line. Then use this this information
to remove unwanted bases. Most of the changes we need to make on our
script is outside the main loop that cuts/extracts information. We need
to modify the post-processing of the sequence we nust read from the
chromosome. Also, instead of storing the sequence in a `string` it is
easier to use a `list` (in fact it is just a matter of personal taste,
and maybe a little be of being Pythonic). In the end our script would
look like 


{% codeblock lang:python %}
#! /usr/bin/env python
 
import sys
 
file = sys.argv[1]
start = int(sys.argv[2])
end = int(sys.argv[3])
 
size = 0
linesize = 0
segment = []
for line in open(file, 'r'):
    if not line.startswith('>'):
        size += len(line)
    else:
        name = line
        if size >= start and size <= end+linesize:
            segment.append(line.strip())
            linesize = len(line.strip())
 
startline = (start/linesize) + 1
endline = (end/linesize)+1
 
if not start % linesize == 0 and not end % linesize == 0:
    segment[0] = segment[0][startline*linesize-start:]
    segment[-1] = segment[-1][endline*linesize-end:]
elif not start %linesize == 0:
    segment[0] = segment[0][startline*linesize-start:]
elif not end % linesize == 0:
    segment[-1] = segment[-1][endline*linesize-end:]
 
print name, '\n'.join(segment)
{% endcodeblock %}


Notice that we added a new
variable `linesize`, to store the size of the sequence line. The loop is
almost identical to the one before. The only changes are the line that
checks for each line size (can be optimized somewhere else and removed)
and instead of a segment string, it is a list. 

The bulk of
changes/additions are after the loop. We first need to calculate the
initial and final lines of our cut/extracted segment. We just divide the
value of the start and end positions entered by the size of the line and
add 1 to them in order to get a correct line in case we the entered
values are not multiple of the line size. Dividing integers in Python
will return us an integer. After this checking we need to add some
processing conditionals to make sure we are returning the exact segment
requested. The `%` operator in Python return the remainder of a
division, even if the two values are integers. We need to check that the
entered starting and ending positions are or aren't multiple of the line
size. If one or both are multiples we don't need to process the segment.
On the other hand some processing is needed. Clearly we only need to cut
extra nucleotides from the first and last returned lines. That's why the
three clauses: one for both values not being multiple of line size, one
for just the start and another for the end position. And to remove
unwanted nucleotides we basically multiply the number of the
starting/ending line by the size of each line and subtract the actual
start/end position. 

This should give us the number of unwanted
nucleotides in those two lines. And the fact that we stored the segment
as a `list` makes our life easier as we access position 0 and -1 in our
list. On the final output, we print the name and join the list elements
by adding a new line between them.
