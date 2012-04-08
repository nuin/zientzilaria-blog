---
author: Paulo Nuin
date: '2007-10-09 16:13:30'
layout: post
slug: splitting-a-multiple-sequence-fasta-file-making-it-better
status: publish
title: Splitting a multiple sequence FASTA file, making it better
wordpress_id: '61'
? ''
: - fasta
  - Phase 2
  - split
---

On the last entry we saw how to split a multiple FASTA file with our
previous FASTA module. The previous script saved a sequence per file,
where the filename was identical to the original file with the exception
of a number added to the end. Let's say we have the file mysequences.fa,
our script would save mysequences.fa1, mysequences.fa2, ...,
mysequences.fa*n*. This is fine, but we need to make it better. Ideally
we should ask the user for a prefix or a filename for the output. On the
other hand, it would be an improvement if we put the number before the
file tag. We will do that in a couple of lines. First we need to find
the tag and the actual filename. We could go through a longer route if
we used the `find` method to find the dot and then extract portions of
the string to the actual name and tag. 

But we can use `split`

{% codeblock lang:python %}file = sys.argv[1] 
temp = file.split('.')
filename = temp[0]
tag = temp[1]{% endcodeblock %} 

We split the original
string at the dot and the first item or the returned list is the file
name and the second item is the tag. Now we just need to change a little
bit the code for the output and we are done. The final script is

{% codeblock lang:python %}\#!/usr/bin/env python
import sys
import fasta 
file = sys.argv[1] 
temp = file.split('.') 
filename = temp[0] 
tag = temp[1] 
sequences = fasta.read_fasta(open(file, 'r').readlines()) 
count = 1 
for i in sequences: 
	#this is the only different line 
	output = open(filename+'_'+str(count)+'.'+tag, 'w') 
	output.write(i.name+'\\n')
	output.write(i.sequence) 
	count += 1{% endcodeblock %}
