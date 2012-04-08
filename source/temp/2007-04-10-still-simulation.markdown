---
author: admin
date: '2007-04-10 17:23:57'
layout: post
slug: still-simulation
status: publish
title: Still simulation
wordpress_id: '34'
? ''
: - Section 4
---

We use our last code as a starting point in order to generate some real
information from our simulated sequence sets. Our approach here will be
the same: functions to do all the work for us and a very simple main
code. We also reuse some code with applied before to count the
nucleotides. Let's see the code, discussion just after it. [sourcecode
language='python']\#!/usr/bin/env python import random import sys def
simulate\_sequence(length): dna = ['A', 'C', 'G', 'T'] sequence = '' for
i in range(length): sequence += random.choice(dna) return sequence def
nucleotide\_percentage(sequence): print str(sequence.count('A')) + ' As
', print str(sequence.count('C')) + ' Cs ', print
str(sequence.count('G')) + ' Gs ', print str(sequence.count('T')) + '
Ts' def sequence\_identity(set): iden = [] count = 0.0 for x in
range(len(set)-1): print str(x), str(x+1) for n in range(len(set[x])):
if set[x][n] == set[x+1][n]: count += 1 iden.append(count/len(set[x]))
count = 0.0 return iden setsize = int(sys.argv[1]) minlength =
int(sys.argv[2]) maxlength = int(sys.argv[3]) sequenceset = [] for i in
range(setsize): rlength = random.randint(minlength, maxlength)
sequenceset.append(simulate\_sequence(rlength)) identity =
sequence\_identity(sequenceset) for i in range(len(sequenceset)): print
sequenceset[i] if i < len(sequenceset)-1: print 'sequence identity to
next sequence : ' + str(identity[i])
nucleotide\_percentage(sequenceset[i]) print[/sourcecode] Well, not many
new things here. The main one might the be the assignment of the
variable `count`, which receives initially a value of `0.0`, which in
this case is a float. This variable is used the calculate the sequence
identity which is a percentage, or a relative value. If we had
initialized `count` with zero, our division `count/len(set(x)` would
always be zero, due to the fact that count would have been an integer.
The ideal input for this script would have equal minimum and maximum
sequence lengths, as it the simulated set would look more like an
alignment with no indels. Something like: [sourcecode
language='python']python simulation.py 10 30 30[/sourcecode] As is
pointed out in BPB, this example is more an indication that we are able
to use our Python skills to actually make some real code, with some real
output. One issue with this example is the fact that we only calculate
sequence identity of two sequences at a time. It would be ideal to have
sequence identity between all simulated sequences. This would require
much more code, of course a good educational step, but it is something
that can be easily obtained with classes and we will see this later on.
With this entry, we finished our Section 4 and we will start Section 5
with Python's dictionaries, moving to FASTA files and classes next.
