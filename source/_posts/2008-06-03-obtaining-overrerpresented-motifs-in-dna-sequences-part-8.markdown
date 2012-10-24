---
author: admin
date: '2008-06-03 12:49:53'
layout: post
slug: obtaining-overrerpresented-motifs-in-dna-sequences-part-9
status: publish
title: Obtaining overrerpresented motifs in DNA sequences, part 9
wordpress_id: '110'
? ''
: - bioinformatics
  - dna
  - motifs
  - motifs
  - overrepresented
  - Phase 2
  - python
---

We keep on introducing Mike's functions. This time there are a couple of
Python methods that we haven't seen here and need some introduction,
`izip` and `count`. To use these two we also need to import new modules


{% codeblock lang:python %}from itertools import count, izip{% endcodeblock %}

 `count` returns consecutive integers starting at a
defined point (the method's parameter). If empty it starts from zero.
Basically, by starting a `count` it will give an iterable with a
increasing integer values, in a fashion similar to a function with
yield. Every time our loop accesses the `count` it will "remember" the
last return value and increment it by one. `izip` also returns an
iterator, but from a list of iterables. It is basically used to iterate
through a list of many iterables at the same time. In the function below
it is used twice: one to generate a tuple (with `count`) with a sequence
number and the sequence itself. The sequence in the tuple is then used
in another `izip` to create the windows on the sequences to count
motifs. 

{% codeblock lang:python %}
def get_quorums_06(seqs, mlen):
    """
    add seq id_no to a set
    use 'izip(count(),...) to create seq_no
    use 'izip(count(),range(...)) to create start/stop indices for motifs
    """
    quorum = defaultdict(set)
    for id_no, seq in izip(count(), seqs):
        for s, e in izip(count(), range(mlen, len(seq))):
            quorum[seq[s:e]].add(id_no)
    return quorum

{% endcodeblock %} 
	
In the next couple of posts we still be
checking motif quorum functions. Stay tuned.
