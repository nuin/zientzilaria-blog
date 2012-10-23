---
author: Paulo Nuin
date: '2007-10-09 15:22:39'
layout: post
slug: splitting-a-multiple-sequence-fasta-file
status: publish
title: Splitting a multiple sequence FASTA file
wordpress_id: '60'
? ''
: - fasta
  - Phase 2
  - split
---

Starting the new phase of the website, we
will see the easiest way to split a FASTA file. There are many ways to
name each file after the split, and we will use a simple *original
filename* + number. We also going to use the FASTA class and functions
defined previously in `fasta.py`. 


To refresh our memories here is the code 

{% codeblock lang:python %}
class Fasta:
    def __init__(self, name, sequence):
        self.name = name
        self.sequence = sequence
 
def read_fasta(file):
    items = []
    index = 0
    for line in file:
        if line.startswith(">"):
           if index >= 1:
               items.append(aninstance)
           index+=1
           name = line[:-1]
           seq = ''
           aninstance = Fasta(name, seq)
        else:
           seq += line[:-1]
           aninstance = Fasta(name, seq)
 
    items.append(aninstance)
    return items
{% endcodeblock %}



So, basically we need to create a script that reads
the file and then in a loop saves every sequence in a separate file. For
the sake of simplicity all saved files will be in the same directory. To
the script 

{% codeblock lang:python %}
#!/usr/bin/env python 
import sys 
import fasta 

#define a variable with the input filename 
file = sys.argv[1] 
#open the file and read the sequences in one line 
sequences = fasta.read_fasta(open(file, 'r').readlines()) 
#counter to keep the number the sequences and to #be written to the output files 
count = 1
for i in sequences:
	#open a file to output output =
	open(file+str(count), 'w') 
	#write the name and sequence
	output.write(i.name+'\n') 
	output.write(i.sequence) 
	#increment the counter 
	count += 1
{% endcodeblock %}

Very simple, but nice script. In the end
we will have a list of files with only one sequence in it, with
identical name of the original file but with a number in the end. Next
we will see how to modify the filename and even extract some information
from the FASTA sequence to use as a filename.
