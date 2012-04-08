---
author: admin
date: '2008-03-06 17:17:03'
layout: post
slug: parsing-genbank-getting-dna-from-genome-entries-part-i
status: publish
title: 'Parsing GenBank: getting DNA from genome entries, part I'
wordpress_id: '85'
? ''
: - Phase 2
---

Before we see how to improve the speed in our Python code (would it be
possible?), let's go back to our GenBank parsing algorithm. Last time we
saw how to extract the proteins from the CDS entries along the file.
This time we will see how to get the DNA from the file. Usually DNA
sequence is stored at the bottom of the GenBank file, in a long sequence
(if the file is a genome, for instance). Basically, what we need to do
is to get the start and end position of each gene (or any annotated
piece) and cut the long sequence at the bottom. This will require a
couple of changes in our previous script, basically to get the DNA and
to cut it. Previously, we had this to read the file [sourcecode
language='python']proteins = [] index = 0 entry = '' for line in gbfile:
if line.find(' gene ') \>= 0: if index \>= 1: \#parses the CDS and
appends to a list proteins.append(parse\_entry(entry)) entry = '' index
+= 1 entry += line elif line.find('ORIGIN') \>= 0: \#found the DNA
sequence, we can stop now break else: entry += line[/sourcecode] Notice
that we stop when we reach the bottom DNA sequence. We need to go
further, but there is another issue: DNA sequence stored in a GenBank
file are stored in blocks of nucleotides and the initial position in
each line is also there. So we need to join these blocks and remove the
number from the beginning of the line. In the end we would have this
[sourcecode language='python']is\_seq = False genes = [] for line in
gbfile: if line.find(' gene ') \>= 0: if index \>= 1:
genes.append(parse\_entry(entry)) entry = '' index += 1 entry += line
elif line.find('ORIGIN') \>= 0: is\_seq = True
genes.append(parse\_entry(entry)) elif is\_seq == True: line =
line.split() sequence.append(line) else: entry += line str\_seq = '' for
i in sequence: str\_seq += ''.join(i[1:]).upper()[/sourcecode] We added
a couple of things. Mainly a flag boolean variable (`is_seq`) that tells
the program that we have reached "DNA level" and a routine to join the
blocks from the second one to the end. `sequence` is list at first,
appending blocks of actual DNA sequence and numbers obtained from the
`split` method. We use a "blank" `split`, what means it will break the
string in the spaces. Our `join` method above joining list elements from
the element 1 and forward. Element 0 in this case would be the numbers
indicating sequence position. The function to parse the entries and the
class to store the information also need to be changed. Previously, our
class was simpler, with less objects. This time we need to extract more
information. [sourcecode language='python']class CDSinfo: def
\_\_init\_\_(self, gi\_id, id, start, end, complement): self.gi\_id =
gi\_id self.id = id self.start = start self.end = end self.complement =
complement[/sourcecode] We removed the sequence object, but added a
start, end and a complement, for the cases where the gene is on the
reverse complement. The function to extract the info looks like
[sourcecode language='python']def parse\_entry(gene\_data): \#changes a
string to list, splitting at line ends gene\_data =
gene\_data.split('\\n') start, end = 0, 0 gi\_id = '' id = '' complement
= False for line in gene\_data: if line.find(' CDS ') \>=0: temp =
line.split() if temp[1].find('complement') \>= 0: complement = True
temp[1] = temp[1].replace('complement(', '') temp[1] =
temp[1].replace(')', '') temp2 = temp[1].split('..') start = temp2[0]
end = temp2[1] elif line.find('GI:') \>= 0: gi\_id = 'gi' +
line[line.find('GI:')+3:-1] elif line.find('/product') \>=0: id =
line[line.find('=') + 2:-1] elif line.find('protein\_id') \>= 0: id +=
'\\t' + line[line.find('=') + 2: -1] return CDSinfo(gi\_id, id, start,
end, complement)[/sourcecode] We will discuss the parsing function in
the next entry and wrap up both codes, and add them to the repository.
