---
author: admin
date: '2007-09-13 12:08:42'
layout: post
slug: restriction-enzymes-third-take
status: publish
title: Restriction enzymes, third take
wordpress_id: '53'
? ''
: - Section 6
---

We come to the penultimate part of our restriction enzyme site finder.
Just a couple of pieces lacking in the puzzle and we are there. First,
the most important: the function that searches for the sites, using
regex patterns. We called it `find_sites` [sourcecode
language='python']def find\_sites(input, set, sequence): iupacdict =
{'A':'[A]', 'C':'[C]', 'G':'[G]', 'T':'[T]', 'M':'[AC]', 'R':'[AG]',
'W':'[AT]', 'S':'[CG]', 'Y':'[CT]', 'K':'[GT]', 'V':'[ACG]',
'H':'[ACT]', 'D':'[AGT]', 'B':'[CGT]', 'X':'[ACGT]', 'N':'[ACGT]'} site
= set[input] pattern = '' positions = [] for i in site: pattern +=
iupacdict[i] searchpattern = re.compile(pattern) sites =
searchpattern.findall(sequence) temppos =
searchpattern.finditer(sequence) for i in temppos: begin, end = i.span()
positions.append(begin) return sites, positions[/sourcecode] We use the
IUPAC dictionary created previously to translate the nucleotides entries
in the restriction enzyme file. The function also receives three values:
the input name of the selected enzyme, the dictionary with all the
enzymes and sites and the sequence where to search. We could easily
remove one of those, but let's leave it there. First we get the site
from the dictionary and initialize an empty string to receive the patter
and a empty list to receive the positions. We will see why we don't need
an empty list to store the found sites. We then iterate over the site
and create a pattern using the values for each letter of the site
(dictionary key). Created the patter, we compile the regex and with
`findall` we find every entry of the site in the sequence. As we already
have seen, using the regex `findall` will generate a list with all the
entries for that particular regex in the string we are searching. This
is pretty handy because some enzymes have degenerated restriction sites.
That's why we don't need a pre-initialized empty list for the sites.
Then we use the `finditer` to find the the exact position of each one of
the sites. Each iterator is a tuple with a start and end positions. In
our case we only need the start position, so in a small loop we iterate
over the temporary variable and just append to the positions empty list
the start value. We have two integers, `begin` and `end` that receive
the values from `i.span`, but we only use `begin`. The function then
returns two lists as a tuple: one for the sites and one for the
positions. If our programming is correct, both lists should have the
same size and are ready to generate the output.
