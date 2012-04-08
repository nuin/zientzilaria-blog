---
author: Paulo Nuin
date: '2008-05-12 13:16:29'
layout: post
slug: obtaining-overrepresented-motifs-in-dna-sequences-part-3
status: publish
title: Obtaining overrepresented motifs in DNA sequences, part 3
wordpress_id: '105'
? ''
: - bioinformatics
  - dna
  - motifs
  - motifs
  - Phase 2
  - python
---

We take a break of developing code and check for performance (non-scientific testing!). 

In the previous entry a simple file was used
as input: 8 DNA sequences of 500 bases each. That's not enough to test
the performance of the Python script against the C++ compiled
executable. So, we use a larger file; two larger files to be more exact.


First, we use a 555 sequence file with the sequences averaging 19371
nucleotides and another with 3854 sequences averaging 20000 nucleotides
in length. 

Those files were the largest foreground and background
clusters used in analysis. Let's see how the Pyhton and C++ fared
(Linux's time was used in the comparison, for simplicity). 

**Foreground cluster** Average of 10 runs   
C++: 45.66 seconds  
Python: 36.4 seconds  

**Background cluster** Average of 10 runs   
C++: 5 minutes and 4 seconds  
Python: 2 minutes and 44 seconds   

The C++ analysis of the background
cluster was done on a cluster's node, and not on my desktop computer,
due to the fact that my desktop could not handle it. C++ defense: the
code was developed by me and I am not a computer scientist. Clearly
there is room for improvement and performance gain. But, definitely we
can see that by using some advanced techniques in Python we are able to
outperform C++ (at least C++ code developed by me) and still have a
short and easy to read script. Next time we will change the Python's
script output.
