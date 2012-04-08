---
author: admin
date: '2008-05-21 13:50:00'
layout: post
slug: obtaining-overrepresented-motifs-in-dna-sequences-part-iv
status: publish
title: Obtaining overrepresented motifs in DNA sequences, part 5
wordpress_id: '107'
? ''
: - bioinformatics
  - hypergeometric distribution
  - motifs
  - motifs
  - Phase 2
  - python
---

Now that we have the script to generate the word quorums working (and
working fast!) we need then to calculate the a *p* value for each motif
based on the fore and background quorums. A *p* value cut-off will
determine the statistically significant words, or overrepresented. These
overrepresented words then can be analysed in more details (that we
won't see here) and for instance determine new or already known
transcription factor binding sites. A well established statistical
method to determine such overrepresented words is the [Hypergeometric
Distribution](http://www.mnlottery.com/hypergeo.html) (HD for short). HD
measures "success" and "failures" for values that do not fit in the
[binomial
distribution](http://en.wikipedia.org/wiki/Binomial_distribution "Binomial distribution"),
and depend on the measurements without replacement. Basically, HD's
equation has a a series of binomial coefficients/combinations ![HD
equation](http://www.genedrift.org/hd.gif) where *N* is the population
size, *m* is foreground cluster size, *k* is the motif quorum in the
background gene set and *x* is the word quorum in the foreground set.
Note that the above equation is for the cumulative HD, where a sum of
probabilities is calculated. All the combinations in the above equation
have to be expanded to factorials that depending on the value to be
calculated are very computer intensive and sometimes don't fit in the
memory (either a float or integer). But
[Python](http://python.org/ "Python (programming language)") is able to
handle very large numbers and the calculation of large factorials is
relatively fast. In C++, I had to use a couple of tricks to achieve a
good speed in the factorial determination, and specially in the HD
calculation that requires multiple factorials and multiplication,
division and subtraction of large numbers. I didn't want to use any
mathematical trick such as [Stirling's
approximation](http://en.wikipedia.org/wiki/Stirling's_approximation "Stirling's approximation").
13! in C++ already blows the size of long, so I had to use the [MAPM, A
Portable Arbitrary Precision Math Library in
C](http://www.tc.umn.edu/~ringx004/mapm-main.html). This library is
quite fast to calculate the factorial values but when one needs to
calculate more than 200,000 factorials the speed is unbearable. So, I
decided to pre-calculate a series of factorial values, keeping 10
decimal places as precision and saving in another column their
exponential. Then using this table as an input I was able to multiply,
divide and subtract the factorials and by employing the first law of
exponents do the same operations with their exponential. This speeds up
the process tremendously. In Python, we don't need any extra third-party
library, we just use Python itself, without importing an extra module. A
factorial function in Python can be written in one line, but for clarity
is better to define it separately. We can try throwing any number at it
and see the result. [sourcecode language='python'] def fac(n): value =
reduce(lambda i, j : i \* j, range(1, n + 1)) return value [/sourcecode]
We already saw `reduce` and `lambda` and using these two methods make
the factorial function clear and simple. And why are we not using a
recursive function? Because Python has a limit recursion depth (1000).
Next time we will implement the code that calculates the HD *p* values.
[![image](http://img.zemanta.com/pixie.png?x-id=60da2ecf-5651-4268-95c2-8f4bcac0b4be)](http://www.zemanta.com/ "Zemified by Zemanta")
