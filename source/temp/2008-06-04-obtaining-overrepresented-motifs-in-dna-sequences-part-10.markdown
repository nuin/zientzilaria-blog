---
author: admin
date: '2008-06-04 11:33:51'
layout: post
slug: obtaining-overrepresented-motifs-in-dna-sequences-part-10
status: publish
title: Obtaining overrepresented motifs in DNA sequences, part 10
wordpress_id: '112'
? ''
: - bioinformatics
  - motifs
  - motifs
  - overrepresented
  - Phase 2
  - python
  - statistics
---

Let's get back to the statistical module, that will calculate an
Hypergeometric Distribution (HD) *p* value so we can define the
overrepresented motifs. Last time we saw it, we just had defined the
[factorial
function](http://en.wikipedia.org/wiki/Factorial "Factorial"), which is
immensely helpful in this case due to the number of factorial
calculations needed in the HD. The factorial function was the one below
[sourcecode language='python'] def fac(n): value = reduce(lambda i, j :
i \* j, range(1, n + 1)) return value [/sourcecode] but as mentioned in
the comments by
[Dave](http://python.genedrift.org/2008/05/21/obtaining-overrepresented-motifs-in-dna-sequences-part-iv/#comment-13532)
and by Mike via email the method used is not the best method to
calculate factorial in
[Python](http://python.org/ "Python (programming language)"). The best
approach in this case is to use `operator.mul`. All functions in the
operator modules are in implemented in pure C and they mimic the same
operators in Python. So in this module we can find `mul` for
multiplication, `sub` for subtraction, `add` for additions, etc. The
`operator.mul` needs two arguments to multiply, and in our case we still
need to use `reduce` to sum all the results from a series of
multiplications. As parameters we should use a `range`, that can start
with 2, that should go up to the number we want the factorial plus one.
Finally our function would be [sourcecode language='python'] import
operator def fac(n): value = reduce(operator.mul, xrange(2, n+1)) return
value [/sourcecode] The time gain, quickly measured in a non-scientific
fashion in my system, is around 5 to 15%, depending on the factorial
being calculated. It may seem a small gain, but when you need to
calculate almost a million factorials for all possible motifs the amount
of time saved is crucial. Next time we will be back with more
statistics, expanding the module.
[![Zemanta
Pixie](http://img.zemanta.com/pixie.png?x-id=11aa0b44-3e0b-4f49-9921-54123607acf0)](http://www.zemanta.com/ "Zemified by Zemanta")
