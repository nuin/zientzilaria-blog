---
author: Paulo Nuin
date: '2008-08-20 21:32:09'
layout: post
slug: obtaining-overrepresented-motifs-in-dna-sequences-part-13
status: publish
title: Obtaining overrepresented motifs in DNA sequences, part 13
wordpress_id: '149'
? ''
: - defaultdict
  - determination
  - dna
  - motifs
  - motifs
  - Phase 2
  - python
  - Section 3
  - Section 5
---

Now that we have the best quorum determination function and the ideal
function to calculate the [binomial
expansions](http://en.wikipedia.org/wiki/Binomial_theorem "Binomial theorem")
it is easy to program a script to calculate the *p* value of motifs in
DNA sequences. To the script *below in the code there are a couple of
errors that wordpress don't let me fix. The \> and < are replaced by
their literal html enconding. I am working on it, sorry* 

{% codeblock lang:python %}
#!/usr/bin/env python
 
import fasta
import sys
from collections import defaultdict
 
def choose(n, k):
    if 0 <= k <= n:
        ntok = 1
        ktok = 1
        for t in xrange(1, min(k, n - k) + 1):
            ntok *= n
            ktok *= t
            n -= 1
        #print ntok // ktok
        return ntok // ktok
    else:
        return 0
 
def get_quorums(seqs, mlen):
    """
    add seq id_no to a set
    use explicit counter to create seq_no
    """
    quorum = defaultdict(set)
    id_no = 0
    for seq in seqs:
        id_no += 1
        for n in range(len(seq) - mlen):
            quorum[seq[n:n + mlen]].add(id_no)
    return quorum
 
input_seqs = fasta.read_seqs(open(sys.argv[1]).readlines())
input_seqs2 = fasta.read_seqs(open(sys.argv[2]).readlines())
 
foreground = get_quorums(input_seqs, 10)
background = get_quorums(input_seqs2, 10)
 
N = len(input_seqs) + len(input_seqs2)
 
for i in foreground:
    term1 = choose(len(background[i]), len(foreground[i]))
    term2 = choose((N - len(background[i])), len(input_seqs)-1)
    term3 = choose(N, len(input_seqs))
    p = (float(term1) * float(term2)) / term3
    if 0 < p <= 0.0001:
        print i, len(foreground[i]), len(background[i]), p

{% endcodeblock %} 


We already defined choose in the last post (more information in the link
from the Python's cookbook) and earlier Mike sent us a series of
quorum-determination functions and one of the best was portrayed and
explained here.


We also need our fasta module to read the sequences (and only the
sequences) in order to use it in the quorum function. Basically we use
the foreground and background files as input, determine the quorum of
the different words (width 10) and then we iterate over the results,
calculating the *p* value for each motif found in the foreground set.
The tree terms of the Hypergeometric Distribution are calculated
separately and we test for a *p* value smaller that 0.0001 (this can be
modified) and we only print the results that fall in this category.

