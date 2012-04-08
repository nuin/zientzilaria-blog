---
author: admin
date: '2007-07-04 12:33:41'
layout: post
slug: reading-fasta-files-2
status: publish
title: Reading FASTA files
wordpress_id: '40'
? ''
: - Section 5
---

We now have an idea on how to create a class in Python. For our FASTA
reader we will use a very similar approach as the employee class created
before. Based on the simplicity of the FASTA format it is easy to see
what attributes we need in our class: sequence title (header) and
sequence. That's it. Speeding up, our class will look like this
[sourcecode language='python']class Fasta: def \_\_init\_\_(self, name,
sequence): self.name = name self.sequence = sequence[/sourcecode] That's
all we need for now. Of course we could include sequence length,
sequence type, or any other relevant information as a class attribute.
But we will stick with those for the time being. NOw that we have the
class declared, we need to read the file and create instances of the
`Fasta` class to store all our sequences. We already know how to open
and read a file and create functions. We put everything together in a
simple script: [sourcecode language='python']import sys \#class
declaration with both attributes we need class Fasta: def
\_\_init\_\_(self, name, sequence): \#this will store the sequence name
self.name = name \#this will store the sequence itself self.sequence =
sequence \#this function will receive the list with the file \#contents,
create instances of the Fasta class as \#it scans the list, putting the
sequence name on the \#first attribute and the sequence itself on the
second \#attribute def read\_fasta(file): \#we declare an empty list
that will store all \#Fasta class instances generated items = [] index =
0 for line in file: \#we check to see if the line starts with a \> sign
if line.startswith("\>"): \#if so and our counter is large than 1 \#we
add the created class instance to our list \#a counter larger than 1
means we are reading \#from sequences 2 and above if index \>= 1:
items.append(aninstance) index+=1 \#we add the line contents to a string
name = line[:-1] \#and initialize the string to store the sequence seq =
'' \#this creates a class instance and we add the attributes \#which are
the strings name and seq aninstance = Fasta(name, seq) else: \#the line
does not start with \> so it has to be \#a sequence line, so we
increment the string and \#add it to the created instance seq +=
line[:-1] aninstance = Fasta(name, seq) \#the loop before reads
everything but the penultimate \#sequence is added at the end, so we
need to add it \#after the loop ends items.append(aninstance) \#a list
with all read sequences is returned return items fastafile =
open(sys.argv[1], 'r').readlines() mysequences = read\_fasta(fastafile)
print mysequences for i in mysequences: print i.name[/sourcecode] At
first, it looks scary. But is not. There are many ways to create this
loop and to read the sequences, and many ways to make this loop shorter.
We will get there, eventually, but for starters this is OK. Basically,
in the above script we have a `Fasta` class, a `read_fasta` function and
a couple of lines to read a print the results. The `read_fasta` function
basically checks all items of a list and see which is the first
character of each item: a `>` sign indicates that the item should be
parsed to the temporary name string, another character redirects the
item to the sequence string. Instances are created on the fly and the
attributes assigned as what was file content is being scanned. In the
end, just to be sure of what we accomplished with the function we print
the list and loop through it and print the name of each sequence read.
Notice that the loop counter/index is the one that receives the class
attribute. The biggest advantage of this way of reading FASTA files is
that the class and the function are reusable. Basically we can create a
file (for instance called readfasta.py) and import into another script
and we have a FASTA reader ready to rock. We would need to tweak a
little bit in order to catch exceptions, but with consistent FASTA files
this would work fine.
