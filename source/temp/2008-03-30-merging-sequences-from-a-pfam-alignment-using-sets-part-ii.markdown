---
author: admin
date: '2008-03-30 19:30:49'
layout: post
slug: merging-sequences-from-a-pfam-alignment-using-sets-part-ii
status: publish
title: 'Merging sequences from a Pfam alignment: using sets, part II'
wordpress_id: '94'
? ''
: - alignments
  - bioinformatics
  - pfam
  - Phase 2
  - python
---

Mike and Luke left comments and suggestions on how to attack the problem
from the previous entry. I copied their comments here in order to
maintain code formatting a little bit better (comments do not have code
highlighting and formatting). Mike: Why not build a dictionary of the
fasta data keyed by protein ID. The value of each dictionary entry would
be a list of (name,sequence) tuples. Then iterate over the dictionary
items and build the output list from dictionary entries of length == 2.
Obviously, I don’t have any data sets to test it on, but something like
this might work: [sourcecode language='python']def merge\_seqs(data1,
data2): from collections import defaultdict from itertools import chain
data = defaultdict(list) for item in chain(data1, data2): ident =
i.name[i.name.find(’|')+1:i.name.find(’/')] data[ident].append( (i.name,
i.sequence) ) format = “%s-%s-\>%d\\n%s%s” flist = [ ] for key,value in
data.iteritems(): if len(value) == 2: jname,jseq = value[0] kname,kseq =
value[1] flist.append(fmt % (jname, kname, len(jseq), jseq, kseq) )
return flist[/sourcecode] Luke: Are there duplicate IDs in a single
file? If not, no reason to perform the intersection twice (once by set,
once by nested loop). Sets and dictionaries are both hashes, so just
remember the instances with the id: [sourcecode language='python']def
merge\_seqs(data1, data2): first, second = dict(), dict() for i in
data1: first[i.name[i.name.find(’|')+1:i.name.find(’/')]] = i for i in
data2: second[i.name[i.name.find(’|')+1:i.name.find(’/')]] = i
shared\_ids = set(first).intersection(set(second)) flist = [] for i in
shared\_ids: j = first[i] k = second[i] tempname = j.name + ‘-’ + k.name
+ ‘-\>’ + str(len(j.sequence)) tempseq = j.sequence + k.sequence
flist.append(tempname + ‘\\n’ + tempseq) return flist[/sourcecode] If
there are duplicate IDs in a file, and you want the behavior of your
original script of giving every combination \_between\_ files, how about
a dictionary of lists and the cross-product of j & k? (I’m going to use
python2.5’s collections.defaultdict, if you’re on an earlier version use
.setdefault . The cross product brings back a nested loop, but it’s only
over values we want rather than the whole datasets.) [sourcecode
language='python']from collections import defaultdict def
merge\_seqs(data1, data2): first, second = defaultdict(list),
defaultdict(list) for i in data1:
first[i.name[i.name.find(’|')+1:i.name.find(’/')]].append(i) for i in
data2: second[i.name[i.name.find(’|')+1:i.name.find(’/')]].append(i)
shared\_ids = set(first).intersection(set(second)) flist = [] for i in
shared\_ids: cross = [(a,b) for a in first[i] for b in second[i]] for
j,k in cross: tempname = j.name + ‘-’ + k.name + ‘-\>’ +
str(len(j.sequence)) tempseq = j.sequence + k.sequence
flist.append(tempname + ‘\\n’ + tempseq) return flist[/sourcecode] And
if you want combinations from within a file as well, just use one
dictionary of lists and cross each list value with itself, excluding
identical elements: [sourcecode language='python']cross = [(a,b) for a
in data[i] for b in data[i] if a.name != b.name][/sourcecode] To your
question of more directly creating the sets of names, can’t be much more
direct, but perhaps more concise using a generator (or list, with the
extra cost) comprehension: [sourcecode language='python']myset1 =
set(i.name… for i in data1)[/sourcecode] Could do equivalently for the
dict-based first example above, noting that the dict() constructor can
take a sequence of (key, value) tuples. This would not work for the
defaultdict or setdefault based version.
