---
author: admin
date: '2008-05-03 08:39:31'
layout: post
slug: revisting-pfam-alignments-again
status: publish
title: Revisting Pfam alignments, again ...
wordpress_id: '98'
? ''
: - defaultdict
  - merging
  - pfam
  - Phase 2
  - Programming
  - python
---

Continuing on the [Pfam](http://en.wikipedia.org/wiki/Pfam "Pfam")
alignment sequence merge, Luke provided two solutions, one for case
where we have duplicates in the file (that happens) and another one
where duplicates are not tested. First for the case with no duplicates:


{% codeblock lang:python %}def merge_seqs(data1, data2): 
	first, second = dict(), dict() 
	
	for i in data1: 
		first[i.name[i.name.find('|') + 1:i.name.find('/')]] = i 
	
	for i in data2: 
		second[i.name[i.name.find('|') + 1:i.name.find('/')]] = i 
		
	shared_ids = set(first).intersection(set(second)) 
	
	flist = [] 
	for i in shared_ids:
		j = first[i] 
		k = second[i] 
		tempname = j.name + '-' + k.name + '-\>' + str(len(j.sequence)) 
		tempseq = j.sequence + k.sequence
		flist.append(tempname + '\\n' + tempseq) 
	
	return flist{% endcodeblock %}

Basically, his approach is to create two dictionaries, `first` and
`second` to store the data from our lists of
[FASTA](http://fasta.bioch.virginia.edu/ "FASTA") objects. The
dictionaries keys are the sections for each sequence name, and the values
are the FASTA object created when we read the file. After that, a `set`
of both dictionaries is created, and this represents everything we need
in order to find shared sequences between both files. The output is
trivial, basically iterating the set and getting the values from both
dictionaries. But, in some cases there are some duplicates in each Pfam
alignment, and this would make the above approach to miss some
sequences. Luke also provided a solution for this case 

{% codeblock lang:python %}from collections import defaultdict 
def merge_seqs(data1, data2): 
	first, second = defaultdict(list), defaultdict(list) 
	
	for i in data1: 
		first[i.name[i.name.find('|') + 1:i.name.find('/')]].append(i) 
	for i in data2:
		second[i.name[i.name.find('|') + 1:i.name.find('/')]].append(i)

	shared_ids = set(first).intersection(set(second)) 
	flist = [] 
	
	for i in shared_ids: 
		cross = [(a,b) for a in first[i] for b in second[i]] 
		for j,k in cross: tempname = j.name + '-' + k.name + '-\>'’ + str(len(j.sequence)) 
		tempseq = j.sequence + k.sequence
		flist.append(tempname + '\\n' + tempseq) 
		
return flist{% endcodeblock %} 


which
is similar to what Mike suggested. In his approach `defaultdict` is used
instead of a regular dict, initialized as a list. Again we can take
advantage of the fact that we that the value of `defaultdict` has the
same features as the object that was used to initialized it. The same
`set` approach is used and we have a nice set of merged sequences from
two Pfam alignments. Remember that `defaultdict` were introduced in Python
2.5, it won't work on older versions.

