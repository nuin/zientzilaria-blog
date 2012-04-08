---
author: admin
date: '2007-07-16 11:59:56'
layout: post
slug: finding-motifs-iupac-and-regex-an-overview
status: publish
title: 'Finding motifs: IUPAC and RegEx, an overview'
wordpress_id: '45'
? ''
: - Section 6
---

End of Section 5, moving to Section 6. For anyone also following the
book there will be a jump at the end of chapter 8, so we are not
touching the final script that deals with different reading frames here.
We are going straight, or almost, to another take of Regular
Expressions. We are going to check some aspects of restriction enzymes,
but first we are going to touch base with motif finding in DNA
sequences. We already saw how to use the `re` module and to do some
simple regular expression searches. Basically our motif search was very
simple, with run-time user input using [sourcecode
language='python']motif = re.compile('%s' % inmotif)[/sourcecode] where
`inmotif` was the short string sequence entered. Enhancing this a little
bit we will first create a more advanced regex search using mismatches
in the sequences and after we will see (as in the book) how to translate
IUPAC code to regex. The IUPAC table is A - Adenine C - Cytosine G -
Guanine T - Thymine U - Uracil M - A or C R - A or G W - A or T S - C or
G Y - C or T K - G or T V - A or C or G H - A or C or T D - A or G or T
B - C or G or T X - A or C or G or T N - A or C or G or T You are going
to use basic Python to do this. There are mode advanced ways to reach
the same goals, but as we haven't seen a lot of dictionaries it would be
great to check them again. The first idea for the table above is to use
a dictionary for the codes that represent two or more nucleotides, as
dictionary keys would be ideal to include in regex elements. Our basic
dictionary would look like this [sourcecode language='python']iupacdict
= {'M':'[AC]', 'R':'[AG]', 'W':'[AT]', 'S':'[CG]', 'Y':'[CT]',
'K':'[GT]', 'V':'[ACG]', 'H':'[ACT]', 'D':'[AGT]', 'B':'[CGT]',
'X':'[ACGT]', 'N':'[ACGT]'}[/sourcecode] We include the square brackets
around each key because these brackets inside a regex indicate a match
in one of the characters. This dictionary would be really advantageous
for restriction enzymes too. Now in order to find a motif we need to
create a regular expression from the consensus sequence of the motif
model, that can be for instance a transcription factor binding site.
Let's say we have a GATA3 model of binding site which has a model
NNGATARNG what would give us a regular expression [sourcecode
language='python']motif =
re.compile('[ACGT][ACGT]GATA[AG][ACGT]G')[/sourcecode] that can be
extracted directly from the `iupacdict`. Next time, we will check how to
create these regex on the fly, from input and the dictionary.
