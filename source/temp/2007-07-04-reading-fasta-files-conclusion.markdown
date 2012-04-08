---
author: admin
date: '2007-07-04 15:36:15'
layout: post
slug: reading-fasta-files-conclusion
status: publish
title: 'Reading FASTA files: conclusion'
wordpress_id: '42'
? ''
: - Section 5
---

In the previous entry we have seen how to read a FASTA file and display
a simple output. The ability of reading such files in Bioinformatics is
extremely relevant, so from now on most of our scripts that deal with
sequences will use this feature. In the repository there is a link to
the `fasta.py` which contains the code below [sourcecode
language='python']class Fasta: def \_\_init\_\_(self, name, sequence):
self.name = name self.sequence = sequence def read\_fasta(file): items =
[] index = 0 for line in file: if line.startswith("\>"): if index \>= 1:
items.append(aninstance) index+=1 name = line[:-1] seq = '' aninstance =
Fasta(name, seq) else: seq += line[:-1] aninstance = Fasta(name, seq)
items.append(aninstance) return items[/sourcecode] We are going to reuse
this code several times, and now we only need to import by using
[sourcecode language='python']import fasta[/sourcecode] and we are done.
This will make everything easier. Please, be aware in the following
posts the use of this simple module and download it from the repository
if needed.
