---
author: Paulo Nuin
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
obtaining the motif quorums.

I will take advantage of his contribution
and post all of them, with some quick comments on each one of them (his
code comments were kept in each function). After, a small benchmarking
will be posted. Most of the functions need to import a couple of module


{% codeblock lang:python %}from collections import defaultdict, deque
from itertools import count, izip, tee{% endcodeblock %} 

and they have two
parameters, a sequence list and the length of the motifs. The first
function uses again the `defaultdict` and it is very similar to the one
used in the final version of the quorum script. The `defaultdict` is
initialized as a list and the ids are added to a the list, keys are
motifs, only if they are not already present in it. The sequence id is
generated in a variable incremented each time the loop iterates.


{% codeblock lang:python %}def get_quorums_01(seqs, mlen): 
	"""append seq id_no to list after checking to see if already present use explicit counter to create seq_no """ 
	quorum = defaultdict(list) 
	id_no = 0 
	
	for seq in seqs: 
		id_no += 1 
		for n in range(len(seq) - mlen): 
			if id not in quorum[seq[n:n+mlen]]: quorum[seq[n:n + mlen]].append(id_no)

	return quorum{% endcodeblock %} 

The second function is very similar to the
first one, with the caveat that sequence id numbers are generated with
`enumerate`. 

{% codeblock lang:python %}def get_quorums_02(seqs, mlen): 
	""" append seq id_no to list after checking to see if already present use 'enumerate' to create seq_no """ 
	quorum = defaultdict(list)

	for id_no, seq in enumerate(seqs): 
		for n in range(len(seq) - mlen): 
			if id_no not in quorum[seq[n:n+mlen]]:
				quorum[seq[n:n+mlen]].append(id_no) 
				
	return quorum{% endcodeblock %}


`enumerate` is a object based on another iterable object. When called
`enumerate` always returns a tuple of an indexed series. For instance,
in our case above, enumerate will return a series of tuples
`(0, sequence1), (1, sequence2) ... (n, sequenceN)`. That's the reason
the enumerate loop uses a tuple as its index 

{% codeblock lang:python %}for id_no, seq in enumerate(seqs){% endcodeblock %} 

Next couple of posts will cover the other functions sent by Mike. Then we
will go back to the statistical module.

