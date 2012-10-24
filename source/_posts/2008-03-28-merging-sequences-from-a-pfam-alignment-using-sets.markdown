---
author: admin
date: '2008-03-28 20:58:24'
layout: post
slug: merging-sequences-from-a-pfam-alignment-using-sets
status: publish
title: 'Merging sequences from a Pfam alignment: using sets'
wordpress_id: '92'
? ''
: - intersection
  - pfam
  - Phase 2
  - python
  - sets
---

A colleague came with a "problem": what would be the most efficient way
to merge [Pfam](http://pfam.sanger.ac.uk/) alignments? He had FASTA
files containing sequences and he wanted to find identical IDs in two
files and merge the related sequences from different domains of the same
protein. His C++ approach was taking too long to run so I jumped in to
help with some Python tricks. 

Fasta headers of Pfam alignments look like
this `>P00526.2|SRC_RSVP/147-229` where the first section, before the
pipe, is the protein family, the section between the pipe and the slash
is the protein ID and the after the slash are the start and end
positions. Basically we want to match the protein ID, between | and /,
which is the only section that should not change from one alignment from
the other, if there are similar sequences in both files. His dataset
size was around 8000 FASTA files and he wanted to compare
all-versus-all. 

The first idea that comes to mind is to read the two
files and basically run nested loops checking for matches between two
sequence names. Simple and easy. But it would be good to find something
else to do in the meantime, instead of checking for its progress.
Another idea, to simplify the process, is to read both files, extract
the protein IDs and check for the intersection of the two sets of IDs
and then just extract the sequences from a list of matches. 

{% codeblock lang:python %}
def merge_seqs(data1, data2):
 
    myset1, myset2 = Set([]), Set([])
 
    for i in data1:
        myset1.add(i.name[i.name.find('|')+1:i.name.find('/')])
 
    for i in data2:
        myset2.add(i.name[i.name.find('|')+1:i.name.find('/')])
 
    mylist = Set.intersection(myset1, myset2)
 
    flist = []
    for i in mylist:
        for j in data1:
            if j.name[j.name.find('|')+1:j.name.find('/')] == i:
                for k in data2:
                    if k.name[k.name.find('|')+1:k.name.find('/')] == j.name[j.name.find('|')+1:j.name.find('/')]:
                        tempname = j.name + '-' + k.name + '->' + str(len(j.sequence))
                        tempseq = j.sequence + k.sequence
                        flist.append(tempname + '\n' + tempseq)
 
    return flist

{% endcodeblock %}

This
is the function that matches the sequence IDs. As we are reading the
FASTA file with the functions/classes in the `fasta` module there is
no\* direct way to transform the list of sequence names into a set, that
would make easier to extract the intersection between two sets of IDs
from distinct files. In the above function, `data1` and `data2` are
instances of the `fasta` class, and we read these lists and add the
`fasta.name` to a couple of sets and get the intersection of them. The
`intersection` method returns a list that we use in the nested loops to
find the matching sequences, as we need to merge them, we add both names
and residues. Simple and easy. All merged sequences, and their
respective merged names, are appended to a list that is returned at the
end of the function. 

\**if there is a more direct way, just let me know*
