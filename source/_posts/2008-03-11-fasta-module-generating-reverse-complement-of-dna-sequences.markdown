---
author: Paulo Nuin
date: '2008-03-11 12:17:21'
layout: post
slug: fasta-module-generating-reverse-complement-of-dna-sequences
status: publish
title: 'Fasta module: generating reverse complement of DNA sequences'
wordpress_id: '88'
? ''
: - dna
  - fasta
  - Phase 2
  - python
  - reverse complement
---

As shown in the GenBank DNA parser script, it is really useful to have
the ability to get the reverse complement of some DNA sequences. The
reverse complement of a 5'-3' DNA sequence is on its complementary
strand. Using our `fasta` module it is easy to implement a function to
generate the antiparallel sequence Basically we can do this in two step,
one - obtaining the complement and two - reversing it. 

{% codeblock lang:python %}
def complement(seq): 
	abuffer = [] 
	for i in seq: 
		if i == 'A': 
			abuffer.append('T') 
		elif i == 'C': 
			abuffer.append('G') 
		elif i == 'T': 
			abuffer.append('A') 
		elif i == 'G': 
			abuffer.append('C') 

	return abuffer{% endcodeblock %}

That's not a Pythonic approach, but it works
reasonably well for short sequences. What would be a Pythonic approach
to it? Using dictionaries and list comprehension. From the Python online
documentation: *List comprehensions provide a concise way to create
lists without resorting to use of map(), filter() and/or lambda. The
resulting list definition tends often to be clearer than lists built
using those constructs. Each list comprehension consists of an
expression followed by a for clause, then zero or more for or if
clauses. The result will be a list resulting from evaluating the
expression in the context of the for and if clauses which follow it.* 

It
is basically a specific way to modify lists using a loop and if clauses
when needed. In a couple of lines we can do what we accomplished in 10
lines with the above excerpt. First we need a dictionary to set how the
nucleotides are related 

{% codeblock lang:python %}complement = {'A':
'T', 'C': 'G', 'G': 'C', 'T': 'A'}{% endcodeblock %} 

and then a list
comprehension to modify each nucleotide 

{% codeblock lang:python %}complseq = [complement[base] for base in seq]
{% endcodeblock %} 

The list comprehension means: for each base in the
sequence get the dictionary value for each key (a nucleotide in the
initial sequence). The complete function would be 

{% codeblock lang:python %}def complement(seq): complement = {'A': 'T', 'C': 'G',
'G': 'C', 'T': 'A'} complseq = [complement[base] for base in seq] return
complseq{% endcodeblock %} 

One step solved. We are already able to get the
complement, now we need to reverse it. Simple. A Python list method
automatically reverts list elements. Basically what we need then is
below 

{% codeblock lang:python %}def reverse_complement(seq): seq =
list(seq) seq.reverse() return ''.join(complement(seq)){% endcodeblock %}

The
call from any script to this function would be simply be 

{% codeblock lang:python %}fasta.reverse_complement('AACCGGTTTTGGCCAA'){% endcodeblock %}


Batteries included, indeed. 


*more can be found
[here](http://www.onlamp.com/pub/a/python/2002/10/17/biopython.html?page=4).
that served as an inspiration for the function*
