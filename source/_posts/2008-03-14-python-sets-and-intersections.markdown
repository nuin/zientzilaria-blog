---
author: Paulo Nuin
date: '2008-03-14 14:36:11'
layout: post
slug: python-sets-and-intersections
status: publish
title: Python sets and intersections
wordpress_id: '90'
? ''
: - bioinformatics
  - CD-HIT
  - intersection
  - Phase 2
  - python
  - sets
---

Sometime ago we saw how to use sets and
 uniquify lists. This time we will see another example of the use of sets. 

*Note: in the
previous example we saw sets imported as an extra module. This has to be
done for Python versions 2.3 and under. There is a difference between
both: when sets are imported the object is noted `Set` with capital S
while on Python 2.4 and above, set objects are noted with a small s,
`set`. In order to make the post as global as possible for people that
does not have the latest version of Python I will use the 2.3 notation
and import* 

This time we will see a different example of set usage that
includes some methods available for this type of objects. The initial
problem was how to determine which genomes are represented in
protein/DNA clusters obtained with [CD-HIT](http://bioinformatics.ljcrf.edu/cd-hi/). Basically CD-HIT uses
a multiple fasta file to generate clusters of proteins/DNA using their
sequence identity. It clusters the sequences, keeping their fasta title
and assigning an ID for each cluster obtained. We won't see how is
CD-HIT's output, not how to parse it. For this example, let's say three
genomes (A, B and C) were analysed in CD-HIT and we want to determine
which clusters contain sequences from the combinations AB, AC and CB (we
won't touch unique items and clusters with sequences from all genomes
this time). After reading the clusters and sequence IDs in each one of
them we basically need to create unique lists of cluster IDs for each
one of the genomes. That's where `sets` are used 

{% codeblock lang:python %}
from sets import Set 

genA, genB, genC = Set([]), Set([]), Set([]){% endcodeblock %} 

We declare three emtpy sets, that will
store cluster IDs for each one of the genomes. The important part here
is that the sequences' fasta titles should have a unique identifier for
each one of the genomes, just to make it easier to read each cluster
contents. In each of our genomes the sequences were tagged with their
letter in the first character

`>genA_sequence1 ACGT 

>genB_sequence1 ACGTT 

>genC_sequence1 ACGTT ...`

We run CD-HIT and parse the results, maybe creating a class to store
information about each cluster and its sequences. Then we analyse this
list 

{% codeblock lang:python %}
for i in clusters:
    for id in i.sequence_id:
        if id.startswith('>genA'):
            genA.add(i.cluster_number)
        elif id.startswith('genB'):
            genB.add(i.cluster_number)
        elif id.startswith('genC'):
            o.add(i.cluster_number)

{% endcodeblock %}

 Remembering
that `sets` are unordered unique lists, we don't expect to see repeated
cluster IDs in each of the three sets. Now to the fun part. Our first
thought to determine how many clusters contain sequences of A and B
would be to create two loops and iterate checking for equalities in
cluster IDs. But with sets, our task is easier. What we need is the
intersection from genA and genB, and that's the method available to do
that. 

{% codeblock lang:python %}print len(Set.intersection(genA, genB)) 
print len(Set.intersection(genA, genC)) 
print len(Set.intersection(genB, genC)){% endcodeblock %} 

That's it. Three lines of
code, one method. The output will be the number of clusters that contain
sequences of A and B, A and C and B and C, respectively. 

*PS: If anyone
is interested in the CD-HIT output parsing class/function just let me
know.*
