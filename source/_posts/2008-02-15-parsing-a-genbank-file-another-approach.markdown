---
author: Paulo Nuin
date: '2008-02-15 11:35:13'
layout: post
slug: parsing-a-genbank-file-another-approach
status: publish
title: Parsing a GenBank file, another approach
wordpress_id: '77'
? ''
: - GenBank
  - parsing
  - Phase 2
  - python
---

Last couple of entries we learnt a little bit about `sets` and that
newer Python versions make its use a lost faster than `dictionaries` to
uniquify `lists`. And soon we will see good examples of `sets` usage.
And now for some completely different ... we go back to parsing GenBank
files. We saw sometime ago how to extract some simple information
contained in this type of files. I am working on a project that requires
a lot of work in GenBank files, and instead of learning how to use an
available parser I decided to write a simple one on my own. The
requirements were simple: extract all protein sequences from a whole
genome GenBank file and also the DNA from the sequence available in it
(this time we will see how to get the proteins and next time the
latter). We all know that GenBank files have an annotation section, with
IDs, references, organism and some other information at the top. The DNA
sequence at the bottom, after ORIGIN, and the protein sequences are in
annotated regions of CDSs. An example is below:


`      gene            8330..9475                      /gene="COS1"                      /locus_tag="YNL336W"                      /db_xref="GeneID:855380"      CDS             8330..9475                      /gene="COS1"                      /locus_tag="YNL336W"                      /experiment="experimental evidence, no additional details                      recorded"                      /note="Protein of unknown function, member of the DUP380                      subfamily of conserved, often subtelomerically-encoded                      proteins"                      /codon_start=1                      /product="Cos1p"                      /protein_id="NP_014063.1"                      /db_xref="GI:6323993"                      /db_xref="SGD:S000005280"                      /db_xref="GeneID:855380"                      /translation="MKENELKNEKSVDVLSFKQLESQKIVLPQDLFRSSFTWFCYEIY                      KSLAFRIWMLLWLPLSVWWKLSNNCIYPLIVSLLVLFLGPIFVLVICGLSRKRSLSKQ                      LIQFCKEVTENTPSSDPHDWEVVAANLNSYLYENKAWNTKYFFFNAMVCQEAFRTTLL                      EPFSLKKDEAAKVKSFKDSVPYIEEALGVYFREVEKQWKLFNSEKSWSPVGLEDAKLP                      KEAYRFKLTWFLKRISNIFMLIPFLNFLCCIYVSRGMCLLLRTFYLGWILFMLVQGFQ                      NMRMIVLSVKMEHKMQFLSTIINEQESGANGWDEIAKKMNRYLFEKKVWKNEEFFFDG
IDCEWFFSHFFYRVLSAKKSMRALSLNVELWPYIKEAQLSCSEESLA"`



In a GenBank file each coding gene corresponds to at least one protein.
The first line, gene, contains the nucleotide region, as the CDS line.
The other lines, starting with a slash provide information about the
gene and the last piece of information is the DNA translation with the
whole protein sequence. In my case, the first objective was to obtain
the protein sequence, get the protein ID and the gi ID from each entry
in a genome file. An initial assessment, tell us that creating a class
for each protein in the file is a good start. 

{% codeblock lang:python %}class Protein: def __init__(self, gi, id, sequence): 
	self.gi = gi 
	self.id = id 
	self.sequence = sequence{% endcodeblock %} 

So we declare the class and have elements for the
IDs and the amino acid sequence. The next problem is how do get each
gene/CDS information, extract what we need and store in a list of class
instances? This is much like we do with our FASTA entries, reading line
by line and looking for FASTA sequence names, which start with `>`. For
GenBank files we will look for lines containing the word gene. Of course
this would mean that every gene that has this word in its name will be a
problem, so we match against `'  gene  '` (the word gene flanked by two
spaces). 

{% codeblock lang:python %}proteins = [] 
index = 0 
entry = '' 

for line in gbfile: 
	if line.find(' gene ') >= 0: 
		if index \>= 1:
		#parses the CDS and appends to a list
		proteins.append(parse_entry(entry)) 
		entry = '' 
		index += 1 
		entry += line
	elif line.find('ORIGIN') >= 0: 
		#found the DNA sequence, we can stop now 
		break 
	else: 
		entry += line{% endcodeblock %}

 In the above excerpt we read
the file line by line, having an index just to keep the code aware of
which entry we are at. Every time we find a line with `'  gene  '`, we
check for the index and if it is larger than one we parse the entry that
has been compiled already and start a new one. If we find 'ORIGIN' we
bail out, breaking the loop, and in every other case we add a line to
our current entry. When this is sent to the parsing function we clear
the string and start compiling the information again. Using a string for
an entry might be a second choice, as lists are easier to manipulate
after (and eventually we will transform our string in a list by
splitting it). Notice that we have a call to a function `parse_entry`,
let's see how this function is 

{% codeblock lang:python %}def parse_entry(gene_data): 
	prot_id = '' 
	sequence = '' 
	gi_id = ''
	gene_data = gene_data.split('\n') 
	for line in gene_data: 
	if line.find('/product') >=0: 
		prot_id = line[line.find('=') + 2:-1] 
	elif line.find('protein_id') >= 0: 
		prot_id += '\t' + line[line.find('=') + 2: -1] 
	elif line.find('GI:') >= 0: 
		gi_id = 'gi' + line[line.find('GI:')+3:-1]
	elif line.find('/translation') >= 0:
		sequence = line[line.find('=') + 2:] 
		temp = gene_data.index(line) 
		for i in range(temp+1, len(gene_data)): 
			sequence += gene_data[i].strip()

	return Protein(gi_id, prot_id, sequence){% endcodeblock %}

 As mentioned
above, we split the string in a list (we will check if there is any
improvement in speed if we use a list from the beginning) and then
analyse each one of the lines. In this case, we only need the protein,
the gene name and, evidently, the protein sequence. Dissecting the
excerpt above we have 

{% codeblock lang:python %}if line.find('/product') >=0: 
	prot_id = line[line.find('=') + 2:-1] 
elif line.find('protein_id') >= 0: 
	prot_id += '\t' + line[line.find('=') + 2: -1]{% endcodeblock %} 

This will get us the protein ID from
`/protein_id="NP_014063.1"` and also the gene name/info from
`/product="Cos1p"`, which them can be stored in the `prot_id` string
that will be passed to the class instance. The gi ID can be extracted in
similar fashion. In order to get the sequence we have to do a small
trick, that can be seen on the excerpt below

{% codeblock lang:python %}elif line.find('/translation') >= 0:
	sequence = line[line.find('=') + 2:] 
	temp = gene_data.index(line) 
	for i in range(temp+1, len(gene_data)): 
		sequence += gene_data[i].strip(){% endcodeblock %}

 We find the beginning of the
translation information by checking the line that contains
`/translation` and we extract the initial part of the sequence my
finding the equal sign and getting everything after it. Then the trick.
We know that the end of the translation information will be the last
line of the whole gene/CDS entry. So we check for the index of the first
sequence line and store it in a temp variable. Using this variable as
the first value of a range we are able to get every other line of the
sequence. That simple. To do the output, we can just iterate the list of
class objects and print all the information in FASTA format or any other
that we wish. Put everything together and we have a simple but effective
GenBank parser. Please notice that this script wouldn't work in every
possible scenario, but with minor tweaks it should be applicable in most
cases. Next time, we will see how we can get the DNA sequence in an
effective way. *An example of GenBank file can be found
[here](http://www.ncbi.nlm.nih.gov/entrez/viewer.fcgi?db=nuccore&id=117937805)*
