---
author: admin
date: '2008-05-09 21:46:50'
layout: post
slug: obtaining-overrepresented-motifs-in-dna-sequences-part-i
status: publish
title: Obtaining overrepresented motifs in DNA sequences, part 1
wordpress_id: '103'
? ''
: - bioinformatics
  - dna
  - motifs
  - motifs
  - Phase 2
  - python
  - Recursion
---

Changing gears now, leaving behind Pfam alignments. I decided to start a
new series of posts based on the conversion of some small C++ programs I
developed in the past. These small programs (I call them modules because
they were part of a larger application) were used to count motifs, short
nucleotide *words* up to 10-12 base pairs, and then calculate
statistical overrepresentation of these words by comparing a foreground
set of DNA sequences against a background set. We will start comparing
the different approaches of the C++ and the
[Python](http://python.org/ "Python (programming language)") codes and
point out advantages and disadvantages of doing it in one language or
the other. First thing we need to do is to count the motifs in all
sequences from our foreground and background sets. For the project I was
working on, the ideal word length was 10 nucleotides. Basically our C++
approach to increase speed was to transform the character DNA sequences
into numbers and then, while sliding a window with the desired word
length,
[hash](http://en.wikipedia.org/wiki/Hash_function "Hash function") the
base-four numbers into base 10 and increment a vector position,
previously initialized with 0. For four nucleotides and a word size of
10 there are 1,048,576 permutations possible, from AAAAAAAAAA to
TTTTTTTTTT. Initially the C++ program would do [sourcecode
language='c']for(j = 0; j < seqsize; j++) { seqfile.get(base); if(base
!= '\\n') { switch(base) { case 'A': bseq.push\_back(0); break; case
'C': bseq.push\_back(1); break; case 'G': bseq.push\_back(2); break;
case 'T': bseq.push\_back(3); break; } } }[/sourcecode] reading all
sequences and pushing an figure for each nucleotide in a vector, and
then sliding a window on this vector and hashing the base-four number
[sourcecode language='c']int hashSeq(vector subseq) { int w, i,
hashvalue = 0, power; w = subseq.size() - 1; for(i = 0; i <
subseq.size(); i++) { power = 0; hashvalue += subseq[i] \*
pow((double)4,(double)w); w--; } return hashvalue; } if(binseq[i].size()
\> motifwidth) { for(j = 0; j < binseq[i].size()-motifwidth+1; j++) {
sub.assign(binseq[i].begin() + j, binseq[i].begin() + j+motifwidth);
hashed = hashSeq(sub); nmercount[hashed]++; sub.clear(); }
}[/sourcecode] The whole C++ code has about 400 lines, including all the
possible output formatting and printing. Timing with `time` the C++
executable takes a little bit less than 2 seconds to read, count and
output different files. For Python, we will use a different approach and
gain a lot in code simplicity. As we want to count the number of times
size-10 words appear in all sequences, we first need to generate all
possible permutations (with replacement) of four nucleotides. This can
be easily accomplished by using generator functions. Regular functions
run until completion and the return a value. For instance, a function
that calculates the factorial of 10 will return the last value only,
after multiplying 10.9.8.7.6.5.4.3.2. A generator function runs until a
value is available to return, `yielding` it and then suspending its
operation until called again. The yielding part was emphasized because
`yield` is the command used by Python to return the value and suspend
the function until further notice. In the [factorial
function](http://en.wikipedia.org/wiki/Factorial "Factorial"), a
generator would return the intermediary factorial values up to 10. To
generate all 1 million plus permutations of 4 nucleotides we need a
function similar to the one below (modified from
[here](http://aspn.activestate.com/ASPN/Cookbook/Python/Recipe/190465))
[sourcecode language='python']def permutations(items, n): if n == 0:
yield '' else: for i in range(len(items)): for base in
permutations(items, n - 1): yield str(items[i]) + str(base)[/sourcecode]
Basically, what this generator function does is to combine all four
nucleotides in words of size 10. This is a [recursive
function](http://en.wikipedia.org/wiki/Recursion_(computer_science) "Recursion (computer science)"),
where the result of the function is dependent on the n-1 value
calculated by the function until n equals 0. The first `for` loop over
the items that we want to permute (the nucleotides) and the second `for`
recursively calls `permutations starting with the initial n` passed (10)
until we reach 0. Debugging this function we will see that `i` is
constant for each iteration of the second loop and only `n` changes from
10 to 0, while one by one nucleotides are joined to form a motif. It
starts with AAAAAAAAAA, then AAAAAAAAAC, then AAAAAAAAAG, until it gets
to a poly-T. Our final code would look like the one below [sourcecode
language='python']import fasta import sys def permutations(items, n): if
n == 0: yield '' else: for i in range(len(items)): for base in
permutations(items, n - 1): yield str(items[i]) + str(base) seqs =
fasta.get\_seqs(open(sys.argv[1]).readlines()) length = sys.argv[2]
nucleotides = ['A', 'C', 'G', 'T'] merged\_seqs = '' for i in seqs:
merged\_seqs += i.sequence for i in permutations(nucleotides,
int(length)): print i + '\\t' + merged\_seqs.count(i)[/sourcecode] where
we read the input sequence(s), merge them in one long string and as we
generate all possible combinations we count the number of times they
appear. This code running on the same input file used on the C++
executable is 60 times slower, taking in average one full minute to
count motifs in 8 500 bp DNA sequences. The slowest section is the
count, as the generation of all possible combinations is
straightforward. We lose some speed, but gain a lot on code simplicity
and clarity. Next we will modify this code to output different counts
needed for the statistical analysis.
[![image](http://img.zemanta.com/pixie.png?x-id=9e5576a3-3aac-421a-8959-197194f2d876)](http://www.zemanta.com/ "Zemified by Zemanta")
