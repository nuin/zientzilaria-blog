---
author: Paulo Nuin
date: '2008-03-14 13:40:26'
layout: post
slug: genbank-parsing-both-scripts
status: publish
title: 'GenBank parsing: both scripts'
wordpress_id: '87'
? ''
: - bioinformatics
  - dna
  - GenBank
  - parsing
  - Phase 2
  - protein
  - python
---

Both scripts to parse GenBank scripts are below and included in the
repository. First the one that extracts amino acid sequences, and then
the latest to extract the DNA. 

{% codeblock lang:python %}
#! /usr/bin/env python
 
'''
input is a GenBank file. The script searches for gene annotations, extract all lines
from the file and then parses these lines in order to extract protein sequences
Ribosomal genes and other non-coding genes are not extracted - plan to do it later
output is a fasta formatted file
'''
 
import sys
import fasta
 
class Protein:
    '''
    class that stores protein information
    '''
    def __init__(self, gi, id, sequence):
        self.gi = gi
        self.id = id
        self.sequence = sequence
 
def parse_entry(gene_data):
    '''
    parses the entry received from the main function
    in order to extract information as protein id
    gi, etc
    '''
    prot_id = ''
    sequence = ''
    gi_id = ''
    gene_data = gene_data.splitlines()
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
                if gene_data[i].find('sig_peptide') >= 0:
                    break
                else:
                    sequence += gene_data[i].strip()
 
    return Protein(gi_id, prot_id, sequence)
 
#only input is a genbank file
gbfile = open(sys.argv[1])
 
proteins = []
index = 0
entry = ''
for line in gbfile:
    if line.find('  gene ') >= 0:
        if index >= 1:
            #parses the CDS and appends to a list
            proteins.append(parse_entry(entry))
            entry = ''
        index += 1
        entry += line
    elif line.find('ORIGIN') >= 0:
        #found the DNA sequence, we can stop now
        break
    else:
        entry += line
 
#parses the last entry after leaving the loop
proteins.append(parse_entry(entry))
 
#output
for i in proteins:
    if len(i.gi) > 2:
        print i.gi, i.id
        output = open(i.gi + '.fasta', 'w')
        output.write('>' + i.gi + '\t' + i.id + '\n')
        i.sequence = i.sequence.replace('\"', '')
        output.write(fasta.format_output(i.sequence, 80))
        print i.id


{% endcodeblock %} 

{% codeblock lang:python %}

#! /usr/bin/env python
 
'''
script that extracts sequences from a GenBank file. Script reads the gene CDS from the file and
builds a list of start and end positions, and if gene is complement outputs the 5'3' sequence and
its reverse complement
only input is a GenBank file
outputs a fasta file with the GI ID as its name.
'''
 
import sys
import fasta
 
class CDSinfo:
    '''
    CDSinf class to store all the information from CDS
    '''
    def __init__(self, gi_id, id, start, end, complement):
        self.gi_id = gi_id
        self.id = id
        self.start = start
        self.end = end
        self.complement = complement
 
def parse_entry(gene_data):
    '''
    each CDS entry is obtained in the main function and a string of lines with
    information is passed to parse_entry to be parsed and have information extracted
    '''
 
    gene_data = gene_data.splitlines() #changes a string to list, splitting at line ends
    start, end = 0, 0
    gi_id = ''
    id = ''
    complement = False
    for line in gene_data: #searches for regions annotated as CDS
        if line.find('  CDS  ') >=0:
            temp = line.split()
            #checks for complement sequence, if true remove extra characters
            if temp[1].find('complement') >= 0:
                complement = True
                temp[1] = temp[1].replace('complement(', '')
                temp[1] = temp[1].replace(')', '')
            temp2 = temp[1].split('..')
            start = temp2[0]
            end = temp2[1]
        #checks for GI IDs
        elif line.find('GI:') >= 0:
            gi_id = 'gi' + line[line.find('GI:')+3:-1]
        #get the gene name/function
        elif line.find('/product') >=0:
            id = line[line.find('=') + 2:-1]
        #and adds the protein id
        elif line.find('protein_id') >= 0:
            id += '\t' + line[line.find('=') + 2: -1]
 
    return CDSinfo(gi_id, id, start, end, complement)
 
#only input is the genbank file with annotation and sequence
gbfile = open(sys.argv[1])
 
index = 0
entry = ''
sequence = []
is_seq = False
 
genes = []
for line in gbfile:
    #reads the genbank file and whenever finds a gene annotation
    #concatenate the lines up to the next gene
    if line.find('  gene ') >= 0:
        #if an entry is complete, send it to parse
        if index >= 1:
            #appends to a list of CDSinfo objects
            genes.append(parse_entry(entry))
            entry = ''
        index += 1
        entry += line
    elif line.find('ORIGIN') >= 0:
        #found sequence start, set the flag on and parses the last entry
        is_seq = True
        genes.append(parse_entry(entry))
    elif is_seq == True:
        #if flag is true keep going, usually sequences are store at the end of the file
        line = line.split()
        sequence.append(line)
    else:
        #this is an entry so append line
        entry += line
 
str_seq = ''
#make the sequence a string
for i in sequence:
    str_seq += ''.join(i[1:]).upper()
 
for i in genes:
    if len(i.gi_id) > 2:
        print i.id, i.start, i.end
        output = open(i.gi_id + '.DNA.fasta', 'w')
        output.write('>' + i.gi_id + '\t' + i.id + '\n')
        # if this is a complement, print both 5'-3' and reverse complement sequences
        if i.complement == True:
            output.write(fasta.format_output(fasta.invert(str_seq[int(i.start)-1:int(i.end)]), 80) + '\n')
        else:
            if not i.start.find('join') >= 0:
                output.write(fasta.format_output(str_seq[int(i.start)-1:int(i.end)], 80))



{% endcodeblock %} 

Checking the DNA extract script carefully, we notice
that we have an extra function in the `fasta` module, `invert`.
**Update**: A small change to the script is that `split('\n')` can be
replaced by `splitlines()` which is a built-in method for strings. This
hasn't been added yet to the repository version of the file and an
explanation on its use will be added shortly.
