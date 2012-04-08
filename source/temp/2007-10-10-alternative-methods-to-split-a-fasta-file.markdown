---
author: admin
date: '2007-10-10 13:53:28'
layout: post
slug: alternative-methods-to-split-a-fasta-file
status: publish
title: Alternative methods to split a FASTA file - updated (again)
wordpress_id: '63'
? ''
: - fasta
  - Phase 2
  - split
---

As Daniel didn't enlightened us on how to use csplit, I am posting
several ways on how to split a multiple sequence FASTA file. This post
gets out of our focus (if you haven't noticed, our focus here is
**Python**, and maybe suffers from the NIH effect. Not invented here. We
will be back with our normal programming after this. We start with our
"widely" available option **csplit**:
`csplit -kf seq file '%^>%' '/^>/' '{*}'` where `k` tells the program to
keep files in case of an error, `f` sets a prefix for the output files
(otherwise xx00 is used) and two regex patterns are used: between %s is
the one to skip and between /s is the one to copy up to but not
including the line. In {} is the number of times we want to have the
previous patterns repeated, a \* meaning as many time as possible. Easy,
eh? Now, we can check how perl fares. I am not a perl monger so I
googled it and I found an one-liner. Quoting the original
[site](http://www.softpanorama.org/Scripting/Perlorama/perl_in_command_line.shtml):
Split a multi-sequence FastA file into individual files named after
their description lines.
`perl -ne 'BEGIN{$/=">"}if(/^\s*(\S+)/){open(F,">$1")||warn"$1 write failed:$!\n";chomp;print F ">", $_}'`
and I am not daring to explain this one. But cariaso did and also sent a
better version of it \# This magic variable makes perl read lines \#
that end with \> \# instead of a newline n $/="\>"; while (<\>) { \#
foreach line in the input files if (/\^\>(w+)/) { \# grab the first word
of text open(F,"\>$1") || \# open a file named that word warn "$1 write
failed:$!n"; chomp; \# strip off the \> at the end print F "\>", $\_; \#
print \>text to the file } } You can also do in Python, without any OO
programming in 5 lines: [sourcecode language='python']file =
open('myfile').readlines() str = ''.join(file) temp = str.split('\>')
for i in temp: print '\>' + i[/sourcecode] that can be run with no
difficulties from the interactive console. And which cariaso also
corrected and improved [sourcecode language='python']fileobj =
open("myfile.fasta") ignore = fileobj.read(1) text = fileobj.read()
records = text.split("\>") for i in records: print '\>' + i[/sourcecode]
along the offer of a nicer approach [sourcecode language='python']def
eachfasta(fileobj): sofar = fileobj.readline() for line in fileobj: if
'\>' == line (bracket zero close bracket): yield sofar sofar = line
else: sofar += line yield sofar fileobj = open("myfile.fasta") for i in
eachfasta(fileobj): print i[/sourcecode] Also Joe wanted to dip in and
sent his approach: [sourcecode language='python']\# f6smod.py 10-26-07
jto \# purpose: modify program by Michael Cariaso, given in Paolo Nuin's
blog: \# http://python.genedrift.org import sys fileobj =
open('fasta.seq') ignore = fileobj.read(1) \# The above line removes the
first char from the file object. \# It can also be used to check that
the first char is a '\>' if ignore != '\>': print "The first character
in the supposed FASTA file is: " + ignore print "not '\>', so sys.exit()
is being invoked." sys.exit() text = fileobj.read() records =
text.split('\>') \# Here, rather than use the for loop to just print out
the sequences, it \# is used to store them in a list. After that they
can be printed out, or \# stored in separate files, or or further split
into header line and sequence \# (using the carriage return at the end
of the header file). seqlist = [] listcount = 0 \# store each
header/sequence in a list for i in records: i = '\>' + i
seqlist.append(i) listcount += 1 \# print the list for seq in seqlist:
print seq \# Split into header line and sequence, and make the sequence
a single string. for seq in seqlist: splitCR = seq.split('\\n') print
"header: " + splitCR[0] sequence = ''.join(splitCR[1:]) print "sequence:
" print sequence[/sourcecode] OK, so ~~three~~ ~~five~~ six more options
available. I am pretty sure sed and awk would be able to do it glued by
a bash script, but I am far of being an expert in sed or awk. If you
know how to do it, leave a comment.
