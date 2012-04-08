---
author: admin
date: '2008-05-02 10:11:47'
layout: post
slug: revisiting-pfam-alignments
status: publish
title: 'Revisiting Pfam alignments: using defaultdicts, chains ...'
wordpress_id: '97'
? ''
: - alignment
  - chain
  - defaultdict
  - merging
  - pfam
  - Phase 2
---

I haven't posted in a while, so let's get back to the last topic covered
here, merging sequences from Pfam alignments. Two comments to my last
post suggested some changes to the original code, and both comments made
a considerable improvement to script. But following our line of thought
here, there were many things in both posts that we haven't covered in
the series. In order to make it clear to anyone that is chronologically
following the entries, we will see what new things were suggested in the
comments. We will start with Mike's comment. The code is below.
[sourcecode language='python']def merge\_seqs(data1, data2): from
collections import defaultdict from itertools import chain data =
defaultdict(list) for item in chain(data1, data2): ident =
item.name[item.name.find('|') + 1 : item.name.find('/')]
data[ident].append((item.name, item.sequence)) format =
"%s-%s-\>%d\\n%s%s" flist = [] for key, value in data.iteritems(): if
len(value) == 2: jname, jseq = value[0] kname, kseq = value[1]
flist.append(format % (jname, kname, len(jseq), jseq, kseq) ) return
flist[/sourcecode] Mike's code would only run on Python 2.5, due to the
import of `collections`. He imports only `defaultdict` from collections,
which is similar to a regular dictionary except for the fact that is
takes an extra argument, a `factory function` (that we will examine
soon), and this `factory function` is called everytime a dict key is
found for the the first time, initializing the object. The line
[sourcecode language='python']data = defaultdict(list)[/sourcecode]
creates and intializes a `defaultdict` from an empty list. This
defaultdict is used to store data from a `chain` formed by both input
files being compared. A `chain` makes an iterator that "returns elements
from the first iterable until it is exhausted, the proceeds to the next
iterable" (from Python docs). Basically a `chain` in our case will make
the loop iterate first through `data1` until its last item then will
start the iteration through `data2`. In the loop it will use the region
in the FASTA sequence name as a defaultdict key, and store the fasta
name and sequence as the value. Notice that the defaultdict, as it has
been initialized as a list, allows appending more than one value to each
key, so every time that it finds a sequence with a name identical to
some key already present in the defaultdict, it will append the
information to the value of that key in a list. So, all the matching is
done with this short loop, we only need then to iterate through the keys
and print the result. For the results, Mike set up a format string (we
will see in a future post) that receives the merged sequences and their
names in a formatted way. The iteration along the defaultdict checks for
both keys and values and every time it finds a value with a length of 2
(meaning two sequences shared identical names) it puts the items of the
defaultdict's value list into two tuples. These tuples, containing
sequence and name, are then formatted for output and appended to a list
of merged sequences. There are a lot of new concepts, objects and
methods but Mike's suggestion shows how powerful Python is. For a set of
25 alignments, there is little performance improvement, but our coding
ability improves exponentially with clever suggestions. I will comment
and explain Luke's comments later.
