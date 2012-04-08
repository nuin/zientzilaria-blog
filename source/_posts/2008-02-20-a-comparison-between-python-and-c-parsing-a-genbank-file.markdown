---
author: admin
date: '2008-02-20 14:07:11'
layout: post
slug: a-comparison-between-python-and-c-parsing-a-genbank-file
status: publish
title: 'A comparison between Python and C(++): parsing a GenBank file'
wordpress_id: '80'
? ''
: - benchmarking
  - c++
  - parsing genbank
  - Phase 2
  - python
---

Last time we saw how to extract all the protein sequences from a GenBank
genome file. A program is available in the
[WU-Blast](http://blast.wustl.edu/) package that does exactly the same
thing, called gt2fasta. Let's compare the performance of our Python
script and this compiled C++ (I believe it is C++, the source is not
available). I am using Python 2.5 on the same machine I am running the
already compiled gt2fasta, so don't worry about specs. The input file is
the *E. coli* genome which was linked in the previous post, and I am
timing with the `time` in Linux. Let's see how Python does (less time,
the better): 

gt2fasta	 0m0.123s  
Python 	0m5.466s  

Yep, that's 44 times
slower for Python. It is widely known that compiled languages are faster
than interpreted ones, but maybe 44 times it is an exaggeration, what
makes me think that there are ways to improve out Python script to make
it a little bit faster. After next post we will see if this is possible.
