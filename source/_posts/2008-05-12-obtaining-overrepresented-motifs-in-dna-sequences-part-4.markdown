---
author: Paulo Nuin
date: '2008-05-12 14:35:13'
layout: post
slug: obtaining-overrepresented-motifs-in-dna-sequences-part-4
status: publish
title: Obtaining overrepresented motifs in DNA sequences, part 4
wordpress_id: '106'
? ''
: - bioinformatics
  - dna
  - motifs
  - motifs
  - Phase 2
  - python
---

We found a way to make the Python script as good as or better than the
C++ executable. But for the analysis we need to do, motif counts are not
the value we want. We need the quorum: the number of sequences the motif
is present at least once. For instance, if the desired motifs was
`AAACCCTTTG` we will check in which sequences this word was present. Let's
say in a cluster of 10 sequences, we would find it in sequences 1, 2, 3,
4 and 5, giving us a quorum of 5 out of 10, or 50%. The quorum will be
used in the future in the statistical calculation in order to determine
the overrepresented motifs. With only a couple of modifications, we can
adapt the script used to get the motif counts to get the quorum.


{% codeblock lang:python %}
from collections import defaultdict
import sys
import fasta
 
seqs = fasta.get_seqs(open(sys.argv[1]).readlines())
length = int(sys.argv[2])
 
quorum = defaultdict(list)
 
seq_number = 0
for i in seqs:
    seq_number += 1
    for n in range(len(i.sequence) - int(length)):
        if not seq_number in quorum[i.sequence[n : n + length]]:
            quorum[i.sequence[n : n + length]].append(seq_number)
 
for i in quorum:
    print ''.join(i).upper(), len(quorum[i])

{% endcodeblock %}

 Basically, we change the way the
`defaultdict` is initialized, this time as a list instead of int and we
also change the procedure that used to get the counts. The loop does
identical work, iterating along the sequences, with a window (of the
input length) sliding on them and checking each word. This time instead
of incrementing the value of the `defaultdict`, we append to the list
the sequence number, obtained from a index integer variable (incremented
in each iteration of the loop), if this number is not already in the
list value. In the end each value of `quorum` will be a list os numbers
and by printing the list length we obtain the quorum. Testing the above
script there is no performance loss when comparing to the previous count
script. Next we will see which statistical method to use and start to
devising an script to calculate it.
