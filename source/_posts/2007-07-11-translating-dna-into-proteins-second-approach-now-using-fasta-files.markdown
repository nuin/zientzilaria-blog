---
author: admin
date: '2007-07-11 15:10:09'
layout: post
slug: translating-dna-into-proteins-second-approach-now-using-fasta-files
status: publish
title: 'Translating DNA into proteins: second approach, now using FASTA files'
wordpress_id: '44'
? ''
: - Section 5
---

We have seen before how to translate DNA sequences into amino acids
sequences. We have even created a module that contains the dictionary
for the genetic code. Now we are going to combine both (very simple)
modules we created in one nice script for day-to-day use. So, we have
the [dnatranslate.py](http://python.genedrift.org/code/dnatranslate.py)
and the [fasta.py](http://python.genedrift.org/code/fasta.py) that we
are going to import into our script. And that's basically it: calling
function already created, stored in modules that can be reused anytime.
In the end our script that translates DNA sequences to proteins takes a
little bit more than a handful of lines. 

{% codeblock lang:python %}#!/usr/bin/env python 
import dnatranslate 
import sys
import fasta 

dna = fasta.read_fasta(open(sys.argv[1], 'r').readlines())

for item in dna: 
    protein = dnatranslate.translate_dna(item.sequence)
    print item.name 
    print protein{% endcodeblock %} 


That's it. A good example of
reusable code, that once created fits everywhere and handles most type
of data. We read the FASTA file in the first line, and iterate over the
items created translating them as we go. As an extra exercise, we can
include the output formatting function. First we need to update the
`fasta.py` module (already on the repository) and slightly change the
formatting function, that ends up looking like this 

{% codeblock lang:python %}def format_output(sequence, length): 
    temp = [] 
    for j in range(0,len(sequence),length): 
        temp.append(sequence[j:j+length])
    return '\n'.join(temp){% endcodeblock %} 

For this case the ideal formatting
function would go through the "longer" route mentioned before, because
the final printing should be done by the main script and not by the
imported module. This gives us more control on what we want to do with
the resulting string. The `format_output` function receives two
arguments: the first is the actual DNA/protein sequence to be formatted
and the length we want to output it. We had to remove the loop too, so
only one sequence can be sent to the function and, as pointed, the
function returns a string with the formatted sequence. In the end our
post's initial sequence has one modification only 

{% codeblock lang:python %}#!/usr/bin/env python 
import dnatranslate 
import sys
import fasta 

dna = fasta.read_fasta(open(sys.argv[1], 'r').readlines())
for item in dna: 
    protein = dnatranslate.translate_dna(item.sequence)
    print item.name 
	print fasta.format_output(protein, 60){% endcodeblock %} 
	
the last line, that instead of printing directly the result of the
translation, sends the sequence to the formatting function before.
