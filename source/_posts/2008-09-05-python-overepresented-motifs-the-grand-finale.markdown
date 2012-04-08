---
author: Paulo Nuin
date: '2008-09-05 21:27:56'
layout: post
slug: python-overepresented-motifs-the-grand-finale
status: publish
title: Python, overepresented motifs, the Grand Finale
wordpress_id: '163'
? ''
: - bioinformatics
  - determination
  - Motif
  - motifs
  - Phase 2
  - python
---

In this final part, let's do some very simple refactoring and modify the
output section to make the result a little bit better. There are not
many options about the functions to calculate the [binomial
expansion](http://en.wikipedia.org/wiki/Binomial_theorem "Binomial theorem").
But Andrew posted some opinions on how to slight change the quorum
function. 

{% codeblock lang:python %}def get_quorums(seqs, mlen):
""" add seq id_no to a set use explicit counter to create seq_no """
quorum = defaultdict(int) for seq in seqs: for n in range(len(seq) -
mlen): quorum[seq[n:n + mlen]] += 1 return quorum{% endcodeblock %} 

His modifications were small but improved the code a bit, as you remove one
variable/object from the function. At the same time there is need to
change a bit our output section of the code, as we don't use a
`defaultdict` initialized with a set, but with an integer. 

{% codeblock lang:python %}for i in foreground: term1 = choose(background[i],
foreground[i]) term2 = choose((N - background[i]), len(input_seqs)-1)
term3 = choose(N, len(input_seqs)) p = (float(term1) * float(term2)) /
term3 if 0 < p <= 0.0001: print i, foreground[i], background[i],
p{% endcodeblock %}


Notice that in the `term1` line we don't check for the
set length anymore and just use the integer stored in `foreground` and
`background`. Again a small change, that can make the code a little bit
more clear. But we need to modify this section so the output is a little
bit more clear, maybe ordered by motif sequence. But as we are reading
the sequences as they are our results are not ordered. It would be great
to have a final list starting with `AAAAAAAA` and ending with `TTTTTTTTT`.
There is an easy way to do that, and very inexpensive regarding code and
final performance. Basically we append each one of the motifs (and their
extra information) to a list and use the `sort` method for lists. So our
output section of the code will be 

{% codeblock lang:python %}res_motifs = [] for i in foreground: term1 =
choose(background[i], foreground[i]) term2 = choose((N - background[i]),
len(input_seqs)-1) term3 = choose(N, len(input_seqs)) p =
(float(term1) * float(term2)) / term3 if 0 < p <= 0.0001:
res_motifs.append(i + '\\t' + str(foreground[i]) + '\\t' +
str(background[i]) + '\\t' + str(p)) res_motifs.sort() for i in
res_motifs: print i{% endcodeblock %} 

Putting everything together our final
motif determination script is (batteries included): 

{% codeblock lang:python %}\#!/usr/bin/env python import fasta import sys from
collections import defaultdict def choose(n, k): if 0 <= k <= n: ntok =
1 ktok = 1 for t in xrange(1, min(k, n - k) + 1): ntok *= n ktok *= t
n -= 1 return ntok // ktok else: return 0 def get_quorums(seqs, mlen):
""" add seq id_no to a set use explicit counter to create seq_no """
quorum = defaultdict(int) for seq in seqs: for n in range(len(seq) -
mlen): quorum[seq[n:n + mlen]] += 1 return quorum input_seqs =
fasta.read_seqs(open(sys.argv[1]).readlines()) input_seqs2 =
fasta.read_seqs(open(sys.argv[2]).readlines()) foreground =
get_quorums(input_seqs, 10) background = get_quorums(input_seqs2,
10) N = len(input_seqs) + len(input_seqs2) res_motifs = [] for i in
foreground: term1 = choose(background[i], len(foreground[i]) term2 =
choose((N - background[i]), len(input_seqs)-1) term3 = choose(N,
len(input_seqs)) p = (float(term1) * float(term2)) / term3 if 0 < p <=
0.0001: res_motifs.append(i + '\\t' + str(foreground[i]) + '\\t' +
str(background[i]) + '\\t' + str(p)) res_motifs.sort() for i in
res_motifs: print i{% endcodeblock %} 

Next we will see some basic Python methods. And maybe start a new series and phase.