---
author: Paulo Nuin
date: '2007-05-24 16:19:10'
layout: post
slug: translating-dna-into-proteins
status: publish
title: Translating DNA into proteins
wordpress_id: '38'
? ''
: - Section 5
---

After a long time away, I am back. Things have been hectic in the lab
and there is a shortage of free time to do everything else. Let's get
back to Python. Last time we have seen a dictionary structure that
contained our genetic code. We are going to see a script that will
translate DNA into proteins and we are also going to see how to create a
module in Python that can be imported in any script. This module will
contain the function that translates the DNA, and for the time being
only that. Let's see how our module looks like: 
{% codeblock lang:python %}def translate_dna(sequence): 
    gencode = { 'ATA':'I',
    'ATC':'I', 'ATT':'I', 'ATG':'M', 'ACA':'T', 'ACC':'T', 'ACG':'T',
    'ACT':'T', 'AAC':'N', 'AAT':'N', 'AAA':'K', 'AAG':'K', 'AGC':'S',
    'AGT':'S', 'AGA':'R', 'AGG':'R', 'CTA':'L', 'CTC':'L', 'CTG':'L', 
    'CTT':'L', 'CCA':'P', 'CCC':'P', 'CCG':'P', 'CCT':'P', 'CAC':'H', 
    'CAT':'H', 'CAA':'Q', 'CAG':'Q', 'CGA':'R', 'CGC':'R', 'CGG':'R', 
    'CGT':'R', 'GTA':'V', 'GTC':'V', 'GTG':'V', 'GTT':'V', 'GCA':'A', 
    'GCC':'A', 'GCG':'A', 'GCT':'A', 'GAC':'D', 'GAT':'D', 'GAA':'E', 
    'GAG':'E', 'GGA':'G', 'GGC':'G', 'GGG':'G', 'GGT':'G', 'TCA':'S', 
    'TCC':'S', 'TCG':'S', 'TCT':'S', 'TTC':'F', 'TTT':'F', 'TTA':'L', 
    'TTG':'L', 'TAC':'Y', 'TAT':'Y', 'TAA':'\_', 'TAG':'\_', 'TGC':'C', 
    'TGT':'C', 'TGA':'_', 'TGG':'W', } 
    print sequence 
    proteinseq = '' 

    for n in range(0,len(sequence),3): 
        if gencode.has_key(sequence[n:n+3]) == True: 
            proteinseq += gencode[sequence[n:n+3]] 
    return proteinseq{% endcodeblock %} 


One function, called `translate_dna`, that
receives a DNA sequence and outputs a protein sequence. It is a "long"
function because we have in the middle the genetic code in Python's
dictionary format. Our translation loop is very simple, it reads the DNA
sequence three nucleotides at a time 

{% codeblock lang:python %}for n in range(0,len(sequence),3):{% endcodeblock %} 

means that it will loop from 0
to the size of the DNA sequence in steps of 3, so basically we start at
0 and then jumping directly to 3. This is done to obey the translation
structure based on codons of three nucleotides. Sometimes the DNA
sequence entered does not have a size multiple of three and that's the
reason we use an error checking before accessing the dictionary

{% codeblock lang:python %}if gencode.has_key(sequence[n:n+3]) == True:{% endcodeblock %}

This will test for any possible error, or codons that
are smaller than three nucleotides. If the key exists it is returned and
addes to our protein string. The code that will use this function is
this: 

{% codeblock lang:python %}#!/usr/bin/env python 
import dnatranslate 
dnafile = open("AY162388.seq", 'r').readlines() 
sequence = '' 
for line in dnafile: 
    sequence += line.strip() 

protein = dnatranslate.translate_dna(sequence) 
print sequence, len(sequence)
print 
print protein, len(protein){% endcodeblock %}

No secrets or new things
here. Just notice that we import a module which is not part of the
common Python modules, but was created by us. In this case the
identification in the import will be the name of the `.py` file that
contains the function(s) we are going to use. This file also needs to be
located in the same directory of the script, if not installed in the
Python libraries/modules directory. Notice that to use the function we
need to call 

{% codeblock lang:python %}protein = dnatranslate.translate_dna(sequence){% endcodeblock %} 

as we would do with
the `sys` or the `re` modules. We can now create any modules that will
contain different functions that can be reused anytime without need of
extra coding. For instance, someone can create a module that would read
a FASTA file and return sequences and sequence names in string or a list
and send it to anyone interested in the same functionality. Everything
we would need to do is to have this file installed in Python or in the
same directory of our script and we would take advantage of all
functionality contained in the module. That easy.
    