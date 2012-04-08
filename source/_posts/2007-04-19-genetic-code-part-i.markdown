---
author: Paulo Nuin
date: '2007-04-19 16:53:29'
layout: post
slug: genetic-code-part-i
status: publish
title: 'Genetic code: part I'
wordpress_id: '35'
? ''
: - Section 5
---

The Python dictionary data-type is like hash in Perl. It is a very
similar structure, where each element in the variable is composed of two
values, more specifically a key-value pair. This is the ideal data type
to store the genetic code. As you might know the genetic code governs
the translation of DNA into proteins, where each codon (3 bases or
nucleotides in the DNA sequence) correspond to an amino acid in the
protein sequence. So for every sequence of 3 nucleotides (key) will
represent an amino acid (value). Important things: dictionaries do not
accept duplicated key values, and every time a new value is assigned to
a key the old value is erased. To create a new dictionary use the curly
brackets 

{% codeblock lang:python %}first_dictionary = {}{% endcodeblock %}

 inside the curly braces we first assign a key and
separated by a colon (:), while multiple pairs should be separated by
comma. Both key and value have to be between single or double quotes.
Let's see how we will represent the genetic code in a Python dictionary,
assigning values to keys 

{% codeblock lang:python %}gencode = {
'ATA':'I', #Isoleucine 
'ATC':'I', #Isoleucine 
'ATT':'I', # Isoleucine
'ATG':'M', # Methionine 
'ACA':'T', # Threonine 
'ACC':'T', # Threonine
'ACG':'T', # Threonine 
'ACT':'T', # Threonine 
'AAC':'N', # Asparagine
'AAT':'N', # Asparagine 
'AAA':'K', # Lysine 
'AAG':'K', # Lysine
'AGC':'S', # Serine 
'AGT':'S', # Serine 
'AGA':'R', # Arginine
'AGG':'R', # Arginine 
'CTA':'L', # Leucine 
'CTC':'L', # Leucine
'CTG':'L', # Leucine 
'CTT':'L', # Leucine 
'CCA':'P', # Proline
'CCC':'P', # Proline 
'CCG':'P', # Proline 
'CCT':'P', # Proline
'CAC':'H', # Histidine 
'CAT':'H', # Histidine 
'CAA':'Q', # Glutamine
'CAG':'Q', # Glutamine 
'CGA':'R', # Arginine 
'CGC':'R', # Arginine
'CGG':'R', # Arginine 
'CGT':'R', # Arginine 
'GTA':'V', # Valine
'GTC':'V', # Valine 
'GTG':'V', # Valine 
'GTT':'V', # Valine
'GCA':'A', # Alanine 
'GCC':'A', # Alanine 
'GCG':'A', # Alanine
'GCT':'A', # Alanine 
'GAC':'D', # Aspartic Acid 
'GAT':'D', # Aspartic Acid 
'GAA':'E', # Glutamic Acid 
'GAG':'E', # Glutamic Acid 
'GGA':'G', # Glycine 
'GGC':'G', # Glycine 
'GGG':'G', # Glycine 
'GGT':'G', # Glycine 
'TCA':'S', # Serine 
'TCC':'S', # Serine 
'TCG':'S', # Serine
'TCT':'S', # Serine 
'TTC':'F', # Phenylalanine 
'TTT':'F', # Phenylalanine 
'TTA':'L', # Leucine 
'TTG':'L', # Leucine 
'TAC':'Y', # Tyrosine 
'TAT':'Y', # Tyrosine 
'TAA':'_', # Stop 
'TAG':'_', # Stop
'TGC':'C', # Cysteine 
'TGT':'C', # Cysteine 
'TGA':'\', # Stop
'TGG':'W', # Tryptophan }{% endcodeblock %} 

Simple, yet efficient. But this
is the type of functionality that would be great to have at hand
every time you write a script to translate DNA into proteins. And it is
not something that you would like to type (or even copy-and-paste) all
the time. On the next post we will create the translation script and
will also create our first Python module.
