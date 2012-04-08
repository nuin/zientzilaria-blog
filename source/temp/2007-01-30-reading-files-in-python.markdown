---
author: admin
date: '2007-01-30 13:53:56'
layout: post
slug: reading-files-in-python
status: publish
title: Reading files in Python
wordpress_id: '11'
? ''
: - python
  - read files
  - Section 1
---

We are currently following Chapter 4 of Beginning Perl for
Bioinformatics, which is the first chapter of the book that actually has
code snippets and real programming. The last exercises in this chapter
deal with the ability to read files and operate with information
extracted from these files, to create arrays and scalar list in perl. We
are going to check how to read files in python. The book tells you how
to read protein sequences. Here we are going to read DNA and protein
sequences from files and change them. Let say you have a file with a DNA
sequence in some directory in your hard disk. The file cannot be a FASTA
type (we will see later how to handle FASTA files), just pure sequence,
something like this:
`GTGACTTTGTTCAACGGCCGCGGTATCCTAACCGTGCGAAGGTAGCGTAATCACTTGTTC TTTAAATAAGGACTAGTATGAATGGCATCACGAGGGCTTTACTGTCTCCTTTTTCTAATC AGTGAAACTAATCTCCCGTGAAGAAGCGGGAATTAACTTATAAGACGAGAAGACCCTATG GAGCTTTAAACCAAATAACATTTGCTATTTTACAACATTCAGATATCTAATCTTTATAGC ACTATGATTACAAGTTTTAGGTTGGGGTGACCGCGGAGTAAAAATTAACCTCCACATTGA AGGAATTTCTAAGCAAAAAGCTACAACTTTAAGCATCAACAAATTGACACTTATTGACCC AATATTTTGATCAACGAACCATTACCCTAGGGATAACAGCGCAATCCATTATGAGAGCTA TTATCGACAAGTGGGCTTACGACCTCGATGTTGGATCAGGG`
You can download the file
[here](http://python.genedrift.org/codepy/AY162388.seq). This is a
partial sequence of a mitochondrial gene from a South American frog
species called [*Hylodes
ornatus*](http://calphotos.berkeley.edu/imgs/128x192/0000_0000/1101/0201.jpeg).
For our purposes you can save the file in the same directory you are
going to run the script from, or if you are using the Python interpreter
start it in the directory that contains the file. The file name is not
important but we will use AY162388.seq from now on. The first thing we
have to do is to open the file for reading. We define a string variable
that will contain the file name. [sourcecode language='python']dnafile =
"AY162388.seq"[/sourcecode] In order to open the file, we can use the
command `open`, that receives two strings: the first is the file name
(it can be the whole location too) to be opened and the *mode* to be
used, which is what you want to do with the file. The *mode* can be one
or more letters that tell the interpreter what to do. For now we are
going to use the `r` *mode* , which tells Python to read the file, and
only do that. So our code is [sourcecode language='python']file =
open(dnafile, 'r')[/sourcecode] `file` is a file object that contains
the directives to read our DNA sequence file. Now, we have actually read
the contents of the file but they are stored in a file object and we did
not accessed it yet. We can achieve that by using a myriad of commands.
We will start with the commonest one: read the file line by line. `file`
is our file object. We have just opened it, but Python already knows
that any file contains lines (remember that this is a regular ASCII
file). We are going to use a loop to read each line of the file, one by
one [sourcecode language='python'\>for line in file: print
line[/sourcecode] In Python, the `for` loop/statement iterates over
items in a sequence of items, usually a string or a list (we will see
Python's `list` soon), instead of iterating over a progression of
numbers. Basically, our `for` above will iterate over each line in the
file until EOF (end-of-file) is reached. Our simple script to read a DNA
sequence from a file and output to the screen is [sourcecode
language='python']\#! /usr/bin/env python dnafile = "AY162388.seq" file
= open(dnafile, 'r') for line in file: print line[/sourcecode] You can
download the above script
[here](http://python.genedrift.org/codepy/code_04.py). To run it have
the AY162388.seq in the same directory.
