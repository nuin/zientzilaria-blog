---
author: admin
date: '2007-08-28 17:21:33'
layout: post
slug: finding-motifs-iupac-and-regex-an-approach
status: publish
title: 'Finding motifs: IUPAC and RegEx, an approach'
wordpress_id: '48'
? ''
: - Section 6
---

After a long delay, we are back. Before entering in the next topic,
Restriction Enzymes, let's take a look how to create a regex pattern
from user input and the dictionary of IUPAC code for nucleotides. We
will use the same dictionary from the previous entry [sourcecode
language='python']iupacdict = {'M':'[AC]', 'R':'[AG]', 'W':'[AT]',
'S':'[CG]', 'Y':'[CT]', 'K':'[GT]', 'V':'[ACG]', 'H':'[ACT]',
'D':'[AGT]', 'B':'[CGT]', 'X':'[ACGT]', 'N':'[ACGT]'}[/sourcecode] and
the same consensus sequence of the GATA3 binding site NNGATARNG This
consensus sequence will be provided as a script parameter, along with
the filename [sourcecode language='python']import sys import re
sequencefile = open(sys.argv[1], 'r').readlines() motif =
sys.argv[2][/sourcecode] First line reads the sequence file from the
user input and second line stores the input motif in a string. Now we
have to get the motif string and check for each letter (IUPAC code) and
get the correspondent set of nucleotides. For this we will use a loop
and a the method `get` method of Python dictionaries. This method, as
its name implies, gets the `value of the key` in parentheses. Like this
[sourcecode language='python']for n in motif:
iupacdict.get(n)[/sourcecode] If we combine both excerpts above and run
using as input the GATA3 model the result would like [sourcecode
language='python'][ACGT] [ACGT] [AG] [ACGT][/sourcecode] which is five
nucleotides short of the motif length. How to correct it? Pretty simple
we just add to the dictionary the "regular" nucleotide codes [sourcecode
language='python']iupacdict = {'A':'A', 'C':'C', 'G':'G', 'T':'T',
'M':'[AC]', 'R':'[AG]', 'W':'[AT]', 'S':'[CG]', 'Y':'[CT]', 'K':'[GT]',
'V':'[ACG]', 'H':'[ACT]', 'D':'[AGT]', 'B':'[CGT]', 'X':'[ACGT]',
'N':'[ACGT]'}[/sourcecode] This would solve our "problem" without adding
a line of code to the final script. Fastforwarding to creating the regex
[sourcecode language='python']mregex = '' for n in motif: mregex +=
iupacdict.get(n) print mregex \#just to check tosearch =
re.compile(str(mregex)) for i in tosearch.findall(sequencefile): print
i[/sourcecode] Simple and quick. The final output is not really
elaborated, but we can improve it. Next time.
