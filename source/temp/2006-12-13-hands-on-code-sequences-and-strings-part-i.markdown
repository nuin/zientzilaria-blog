---
author: admin
date: '2006-12-13 22:27:48'
layout: post
slug: hands-on-code-sequences-and-strings-part-i
status: publish
title: 'Hands on code: Sequences and strings - part I'
wordpress_id: '5'
? ''
: - bioinformatics
  - python
  - Section 1
  - sequence
  - strings
---

As pointed in **Beginning Perl for Bioinformatics**, a large percentage
of bioinformatics procedures deals with strings, especially DNA and
amino acids sequence data. As is largely known DNA is composed of four
different nucleotides: A, C, T and G and proteins can contain up to 20
amino acids. Each one of these elements have one letter of the alphabet
assigned to them. In the DNA case some letters represent one or more
nucleotides that can be present at some sequence position (click
[here](http://www.cns.fr/externe/English/Projets/Resultats/iupaciub.html)
for more ). 

So, as the amino acid is the basic building block of
proteins (AKA polypeptides), strings containing sequence is our most
basic block, from where all the bioinformatics magic will work on.
Usually in Perl a string is represented by the dollar sign in front of
the variable name, like this `$sequence`. Python is dynamically typed,
meaning variable types are assigned/discovered by the interpreter at run
time. This means that the value after the equal sign will tell the
interpreter what variable type you are declaring. So in Python if you
want to store a DNA sequence you can just enter 

{% codeblock lang:python %}
mydna="ACGTACGTACGTACGTACGTACGT"
{% endcodeblock %}


*a quick
note: Python can be used with the interpreter command line or by
previously saved scripts. I will try to use the latter in the code
examples.*


OK, we are ready to create our first Bioinformatics Python
Hello World script. Let's get the sequence above and print it on the
screen. The first line will tell the operating system what to use and
where to find the Python interpreter 

{% codeblock lang:python %}#! /usr/bin/env python{% endcodeblock %}

Next we will create the variable myDNA
and assign the corresponding sequence 

{% codeblock lang:python %}
myDNA = "ACGTACGTACGTACGTACGTACGT"
{% endcodeblock %}


And finally, we will print the contents of the variable to the screen:

{% codeblock lang:python %}print myDNA{% endcodeblock %}



As mentioned above, Python mandates that you have your code indented, but in our
final script this is not needed: 

{% codeblock lang:python %}#!/usr/bin/env 
python myDNA = "ACGTACGTACGTACGTACGTACGT" print myDNA
{% endcodeblock %}



The first line tells your operating system that this
is a Python script and to use the interpreter located in that directory;
line two declares a variable called `myDNA` and assigns the sequence
string to it and the last line simply output this variable to the
screen. That simple! To run this (extremely simple) script you can copy
and paste the code above to your favourite text editor save the file
with a `.py` extension (recommended but not necessary). To run the
script, as long as you have Python installed, just open a shell and type
on the command line: 

{% codeblock lang:bash %}> python code_01.py{% endcodeblock %}