---
author: admin
date: '2007-10-09 15:22:39'
layout: post
slug: splitting-a-multiple-sequence-fasta-file
status: publish
title: Splitting a multiple sequence FASTA file
wordpress_id: '60'
? ''
: - fasta
  - Phase 2
  - split
---

starting the new phase of the website, we are going to see some random
thought in Python and Bioinformatics. Any ideas would be highly
appreciated, and I will use some terms used in searches that ended up
finding this blog or [this](http://blindscientist.genedrift.org) or
[this](http://infasta.genedrift.org). We will also see some of the ideas
that are being developed in [Infasta](http://infasta.genedrift.org). We
will see the easiest way to split a FASTA file. There are many ways to
name each file after the split, and we will use a simple *original
filename* + number. We also going to use the FASTA class and functions
defined previously in `fasta.py`. To refresh our memories here is the
code [sourcecode language='python']class Fasta: def \_\_init\_\_(self,
name, sequence): self.name = name self.sequence = sequence def
read\_fasta(file): items = [] index = 0 for line in file: if
line.startswith("\>"): if index \>= 1: items.append(aninstance) index+=1
name = line[:-1] seq = '' aninstance = Fasta(name, seq) else: seq +=
line[:-1] aninstance = Fasta(name, seq) items.append(aninstance) return
items[/sourcecode] So, basically we need to create a script that reads
the file and then in a loop saves every sequence in a separate file. For
the sake of simplicity all saved files will be in the same directory. To
the script [sourcecode language='python']\#!/usr/bin/env python import
sys import fasta \#define a variable with the input filename file =
sys.argv[1] \#open the file and read the sequences in one line sequences
= fasta.read\_fasta(open(file, 'r').readlines()) \#counter to keep the
number the sequences and to \#be written to the output files count = 1
for i in sequences: \#open a file to output output =
open(file+str(count), 'w') \#write the name and sequence
output.write(i.name+'\\n') output.write(i.sequence) \#increment the
counter count += 1[/sourcecode] Very simple but nice script. In the end
we will have a list of files with only one sequence in it, with
identical name of the original file but with a number in the end. Next
we will see how to modify the filename and even extract some information
from the FASTA sequence to use as a filename.
