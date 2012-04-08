---
author: admin
date: '2007-11-01 16:08:24'
layout: post
slug: functional-programming-in-python-using-filter-take-one
status: publish
title: 'Functional programming in Python: using filter, take one'
wordpress_id: '70'
? ''
: - Phase 2
---

This time we check another functional programming function from Python:
`filter`. As the name implies, `filter` returns items from a sequence
(list, string, etc) that are true to a certain condition defined by the
function. The syntax is very similar to `map` [sourcecode
language='python']filter (function, sequence)[/sourcecode] and as `map`
it returns a list (except when the sequence is a string or tuple). In
the example here we will use `lambda` to define a one-line function.
Let's say we want to quickly find the sequences that contain a motif,
sequences that are stored in a FASTA file (again, this is a very simple
example, just a primer). Of course we can use another
[method](http://python.genedrift.org/2007/08/28/finding-motifs-iupac-and-regex-an-approach/),
but this time we want to use a functional programming approach. `filter`
suits us best here. Again we will reuse the newly created function that
returns only the sequences from a FASTA file and we end up with a script
that looks like this [sourcecode language='python']\#! /usr/bin/env
python import fasta import sys sequences =
fasta.read\_seqs(open(sys.argv[1], 'r').readlines()) motif = sys.argv[2]
print filter(lambda x:x.find(motif) \>= 0, sequences)[/sourcecode] We
skip the part we already seen and check the last line. Basically each
item from the list (sequences) is a string and we are applying the
`find` method in order to find a motif on a position larger or equal to
0. Notice again, the syntax similar to `map`. Of course this is not very
useful as it is, so next time we will change this script to make it more
meaningful.
