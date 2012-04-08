---
author: admin
date: '2008-06-03 13:59:28'
layout: post
slug: obtaining-overrepresented-motifs-in-dna-sequences-part-8
status: publish
title: Obtaining overrepresented motifs in DNA sequences, part 9
wordpress_id: '111'
? ''
: - Generator
  - motifs
  - Phase 2
---

Back on new functions for motif quorums. We jump function 7 in order to
explain "simpler" ones, 8 and 9. Both functions use `generators`. We've
already seen here `generators`, which are functions that use the `yield`
statement to generate iterators. The generator is very similar to a
function but instead of returning a value, it yields one and waits for
another call to resume. In function 8, a generator is used to return the
motif sequence that is used as a key in the defaultdict. Notice the
scope of the generator that is coded inside a function. [sourcecode
language='python']def get\_quorums\_08(seqs, mlen): """ add seq id\_no
to a set use enumerate to create seq\_no use an explicit generator to
create the motifs """ def motif\_gen(seq): for n in
range(len(seq)-mlen): yield seq[n:n+mlen] quorum = defaultdict(set) for
id\_no, seq in enumerate(seqs): for motif in motif\_gen(seq):
quorum[motif].add(id\_no) return quorum[/sourcecode] In function 9 a
very similar structure is used but in this cases instead of a "pure"
`generator` it uses `generator expressions` which a very similar to
[list
comprehensions](http://python.genedrift.org/2008/03/11/fasta-module-generating-reverse-complement-of-dna-sequences/)
but with parentheses instead of square brackets. `Generator expressions`
are generators that can be written in one line and have identical
behaviour as generators coded in the "regular" inception. In the
function below the `generator expressions` provide the iterator for the
loop with `motif` as index. Very simple and elegant. [sourcecode
language='python']def get\_quorums\_09(seqs, mlen): """ add seq id\_no
to a set use enumerate to create seq\_no use a generator expression to
create the motifs """ quorum = defaultdict(set) for id\_no, seq in
enumerate(seqs): for motif in (seq[n:n+mlen] for n in
range(len(seq)-mlen)): quorum[motif].add(id\_no) return
quorum[/sourcecode] In the next post we will go back to the statistical
module and soon we will see the remainder 5 functions sent by Mike.
[![Zemanta
Pixie](http://img.zemanta.com/pixie.png?x-id=f8754f61-28d8-4dc0-b4f1-6ef618fa780e)](http://www.zemanta.com/ "Zemified by Zemanta")
