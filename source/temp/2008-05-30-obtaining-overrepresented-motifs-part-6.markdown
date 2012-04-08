---
author: admin
date: '2008-05-30 21:30:44'
layout: post
slug: obtaining-overrepresented-motifs-part-6
status: publish
title: Obtaining overrepresented motifs in DNA sequences, part 6
wordpress_id: '108'
? ''
: - bioinformatics
  - defaultdict
  - enumerate
  - motifs
  - motifs
  - Phase 2
  - python
---

We will take a break on developing the statistical module to obtain
overrepresented motifs (I will introduce mul in the next stats post),
and take a deeper look at the possibilities on obtaining the motif
quorums. Mike DeHaemer, a regular commenter and contributor to the blog,
sent me a [Python](http://python.org/ "Python (programming language)")
script with 8 different ways distributed in 13 distinct functions for
obtaining the motif quorums. I will take advantage of his contribution
and post all of them, with some quick comments on each one of them (his
code comments were kept in each function). After, a small benchmarking
will be posted. Most of the functions need to import a couple of module
[sourcecode language='python']from collections import defaultdict, deque
from itertools import count, izip, tee[/sourcecode] and they have two
parameters, a sequence list and the length of the motifs. The first
function uses again the defaultdict and it is very similar to the one
used in the final version of the quorum script. The defaultdict is
initialized as a list and the ids are added to a the list, keys are
motifs, only if they are not already present in it. The sequence id is
generated in a variable incremented each time the loop iterates.
[sourcecode language='python']def get\_quorums\_01(seqs, mlen): """
append seq id\_no to list after checking to see if already present use
explicit counter to create seq\_no """ quorum = defaultdict(list) id\_no
= 0 for seq in seqs: id\_no += 1 for n in range(len(seq) - mlen): if id
not in quorum[seq[n:n+mlen]]: quorum[seq[n:n + mlen]].append(id\_no)
return quorum[/sourcecode] The second function is very similar to the
first one, with the caveat that sequence id numbers are generated with
`enumerate`. [sourcecode language='python']def get\_quorums\_02(seqs,
mlen): """ append seq id\_no to list after checking to see if already
present use 'enumerate' to create seq\_no """ quorum = defaultdict(list)
for id\_no, seq in enumerate(seqs): for n in range(len(seq) - mlen): if
id\_no not in quorum[seq[n:n+mlen]]:
quorum[seq[n:n+mlen]].append(id\_no) return quorum[/sourcecode]
`enumerate` is a object based on another iterable object. When called
`enumerate` always returns a tuple of an indexed series. For instance,
in our case above, enumerate will return a series of tuples
`(0, sequence1), (1, sequence2) ... (n, sequenceN)`. That's the reason
the enumerate loop uses a tuple as its index [sourcecode
language='python']for id\_no, seq in enumerate(seqs)[/sourcecode] Next
couple of posts will cover the other functions sent by Mike. Then we
will go back to the statistical module.
[![Zemanta
Pixie](http://img.zemanta.com/pixie.png?x-id=056c1508-ad72-47fe-b53c-1b2c241e5ee6)](http://www.zemanta.com/ "Zemified by Zemanta")
