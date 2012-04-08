---
author: admin
date: '2006-12-14 15:30:32'
layout: post
slug: sequences-and-strings-part-ii
status: publish
title: Sequences and Strings - part II
wordpress_id: '6'
? ''
: - bioinformatics
  - python
  - Section 1
  - sequence
  - strings
---

Another important task for many biologists is to merge/concatenate
different strings of DNA in one unique sequence. We can modify the
previous script to concatenate two distinct DNA sequences in one. We
start using code\_01 structure, adding some extra elements (line 3):

{% codeblock lang:python %}
#! /usr/bin/env python 
myDNA = 'ACGTACGTACGTACGTACGTACGT' 
myDNA2 = "TCGATCGATCGATCGATCGA" 
print myDNA, myDNA2
{% endcodeblock %}



So far, we added a new string containing an extra
DNA sequence and we `print` both sequences. In Python `print` statement
automatically adds a new line at the end of the string to be printed,
unless you add a comma (,) to the end. The comma is also needed if you
are going to print more than one string in order to separate them (*try
removing the comma from the code above*). Now, how do we merge myDNA and
myDNA2? Easy in Python: just *sum* them with a plus signal: 


{% codeblock lang:python %}
myDNA3 = myDNA + myDNA2 
print myDNA3
{% endcodeblock %}



Notice that in Python strings are immutable, meaning they cannot be
changed. This immutability confers some advantages to the code where
strings (*in Python strings are not **variables***) cannot be modified
anywhere in the program and also allowing some performance gain in the
interpreter. So, in order to have our sequences merged we create a third
sequence that receives both strings. Finally our code will be (some
captions were added): 

{% codeblock lang:python %}
#! /usr/bin/env
python myDNA = "ACGTACGTACGTACGTACGTACGT" 
myDNA2 = "TCGATCGATCGATCGATCGA" 
print "First and Second sequences"
print myDNA, myDNA2 
myDNA3 = myDNA + myDNA2 
print "Concatenated sequence"
print myDNA3
{% endcodeblock %}

Easy, eh? Of course these two simple scripts do no
scratch the surface of Python programming, but they are a start.
