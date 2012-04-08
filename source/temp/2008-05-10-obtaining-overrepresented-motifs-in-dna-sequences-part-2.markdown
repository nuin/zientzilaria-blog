---
author: admin
date: '2008-05-10 21:56:51'
layout: post
slug: obtaining-overrepresented-motifs-in-dna-sequences-part-2
status: publish
title: Obtaining overrepresented motifs in DNA sequences, part 2
wordpress_id: '104'
? ''
: - bioinformatics
  - defaultdict
  - dna
  - motifs
  - motifs
  - Phase 2
  - Programming
  - python
---

We move one on our search for overrepresented motifs in DNA sequences. I
was preparing this entry when the comments to part 1 arrived. Because of
that we will modify our previous code to include some suggestions and
then we will change t a little bit to output the actual values we want.
As Titus pointed out in his comment, when we merge the sequences we
generate errors, because we artificially including motifs that are not
supposed to be there. But in the end we will see that we are no after
the actual number of times a motif appears in the sequence and what
matters is the motif quorum. The main focus of the part one was to show
the decrease in code length from C++ to Python, introduce generator
functions and yield and also show the nice permutation function. Turns
out by using the approach of the previous entry there is a big drawback
in code execution, which is around 60 times slower than C++. So we need
to find another approach, and Mike showed us how (with some small
modifications) [sourcecode language='python'] \#!/usr/bin/env python
from collections import defaultdict import sys import fasta seqs =
fasta.get\_seqs(open(sys.argv[1]).readlines()) length = int(sys.argv[2])
\#for a missing key, the dict entry is initialized to zero counts =
defaultdict(int) \#count the length-element subsequences in each
sequence for i in seqs: for n in range(len(i.sequence) - length):
counts[i.sequence[n : n + length]] += 1 \#counts.keys() will then return
the nucleotide sequences \#that were actually in merged\_seqs \#print
out the sequences that occur more than once for count in counts: print
''.join(count), counts[count][/sourcecode] This time the counting is
done with a defaultdict initialized with integers (all zeroes), and
instead of generating all possible combinations (which was cool and
fast, but in the end made our script slower) a window with the input
length is slided along the each sequence and the key of the default
dictionary is the motif and the value is the actual count incremented as
we determine each motif. Checking this code performance using Linux's
time, we get 0.2 seconds, an improvement of 5 fold on the C++ code and
300 fold on our previous Python code (Thanks Mike and everyone else for
the suggestions). What is different here is that the output is not
ordered and only the seen motifs are printed in the end. We will see
next time how to get the quorums.
[![image](http://img.zemanta.com/pixie.png?x-id=29d95384-32e6-4c9c-8e9b-140819e795d6)](http://www.zemanta.com/ "Zemified by Zemanta")
