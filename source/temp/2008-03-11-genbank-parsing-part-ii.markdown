---
author: admin
date: '2008-03-11 08:49:47'
layout: post
slug: genbank-parsing-part-ii
status: publish
title: 'GenBank parsing: part II'
wordpress_id: '86'
? ''
: - bioinformatics
  - dna
  - GenBank
  - parsing
  - Phase 2
  - python
---

Last thing we saw in the previous entry was the function to parse a
GenBank file in order to get the DNA sequences of an annotated gene.
This time we will dissect the function. [sourcecode
language='python']def parse\_entry(gene\_data): \#changes a string to
list, splitting at line ends gene\_data = gene\_data.split('\\n') start,
end = 0, 0 gi\_id = '' id = '' complement = False for line in
gene\_data: if line.find(' CDS ') \>=0: temp = line.split() if
temp[1].find('complement') \>= 0: complement = True temp[1] =
temp[1].replace('complement(', '') temp[1] = temp[1].replace(')', '')
temp2 = temp[1].split('..') start = temp2[0] end = temp2[1] elif
line.find('GI:') \>= 0: gi\_id = 'gi' + line[line.find('GI:')+3:-1] elif
line.find('/product') \>=0: id = line[line.find('=') + 2:-1] elif
line.find('protein\_id') \>= 0: id += '\\t' + line[line.find('=') + 2:
-1] return CDSinfo(gi\_id, id, start, end, complement)[/sourcecode]
First things first. As in the CDS/protein parsing example, the function
receives a string and it is easier for us to operate with lists, so we
split the string at the carriage returns. This time we also need to
check for the start and end positions of the gene in the long string
that is the DNA sequence of a GenBank file, so we just declare a couple
of integers `start` and `end`. We also have a couple of strings to
receive the gi ID and the gene product (`id`). And finally a boolean,
that will tell us if the sequence in question is on the DNA complement
strand, meaning it is a reverse complement of the DNA that is stored in
the file. So we start our loop checking for the elements of each line.
If we find a `'  CDS  '` we know that we can extract the start and end
positions of the gene [sourcecode language='python']if line.find(' CDS
') \>=0: temp = line.split() if temp[1].find('complement') \>= 0:
complement = True temp[1] = temp[1].replace('complement(', '') temp[1] =
temp[1].replace(')', '') temp2 = temp[1].split('..') start = temp2[0]
end = temp2[1][/sourcecode] We use temporary list and split the line at
the spaces and then move to get the information from it. If the line is
a reverse complement we remove the word from the entry and the
parentheses. Whenever the gene annotation relates to the complement
strand the entry is as such `complement(10728..11330)`. We then use
another temp object and split the second element in the split line and
separate it at the double dots. From this latter split, we end up with
two elements, the first is the start position and the second the end
position of the gene. To extract the other information everything works
as the previous script, basically checking for the presence of certain
words in the each line. In the end we return an instance of the class
`CDSinfo` which will be used to extract the DNA sequence.
