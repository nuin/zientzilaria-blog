---
author: Paulo Nuin
date: '2007-10-29 11:37:07'
layout: post
slug: splitting-a-fasta-file-using-awk-no-sed-required-or-do-we-care-about-csplit
status: publish
title: Splitting a FASTA file using awk (no sed required), or do we care about csplit?
wordpress_id: '66'
? ''
: - off topic
  - Phase 2
---

We saw that "[top notch bioinformaticians](http://eridanus.net/)" use
csplit to split FASTA files, so I decided to 
[post as many as possible alternatives](http://python.genedrift.org/2007/10/10/alternative-methods-to-split-a-fasta-file/)
to split these files. As csplit, awk is something found with more
frequency in Linux machines than Windows, but it can be installed on
Windows (even Vista) and it runs fine. 

Awk is usually shown in parallel
with sed, as both utilities have the main objective of text processing.
I browsed the web searching for a sed/awk solution to split FASTA files
something that I thought could be done in one line. And I found
[it](http://www.unix.com/shell-programming-scripting/14576-split-file-using-awk.html).

With a little tweak I ended up with a one-liner using awk that split the
sequences in multiple files: 

`awk '/^>/{f="fasta."++d} {print > f}' `


Awk breaks each line of its input into fields that can be checked,
printed or ignored. In the command line above. awk's commands are in
between the single quotes. The first command is a regex that matches
initial `>`. Inside the curly braces we assign a variable `f` to store
the output filename we want and also have an integer that is incremented
every time we pass through it. The second curly braces are for the
actual output, where we use awk's `print` command and redirect output to
a file named after the variable we created in the first commands in
between curly braces. Finally, we assign an input file, outside the
region delimited by single quotes. And that's it. As output we will have
a series of files called fasta each one containing one sequence.
