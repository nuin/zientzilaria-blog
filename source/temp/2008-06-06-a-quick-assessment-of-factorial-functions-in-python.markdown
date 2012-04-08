---
author: admin
date: '2008-06-06 11:52:35'
layout: post
slug: a-quick-assessment-of-factorial-functions-in-python
status: publish
title: A quick assessment of factorial functions in Python
wordpress_id: '113'
? ''
: - factorial
  - functions
  - lambda
  - operator.mul
  - Phase 2
  - python
  - timeit
---

A short pause on the motifs subject. As mentioned on comments there is a
lot of different ways of calculating
[factorials](http://en.wikipedia.org/wiki/Factorial "Factorial") in
Python (the same "problem" can be found in some other languages too).
[Cariaso](http://python.genedrift.org/2008/06/04/obtaining-overrepresented-motifs-in-dna-sequences-part-10/#comment-14054)
suggested to time the execution of different factorial functions,
including the ones found on [Python's
cookbook](http://aspn.activestate.com/ASPN/Cookbook/Python/Recipe/67668)
(which I should have included in the beginning of last post). Anyway all
functions from the webpage were included, as the one mentioned on a
comment and both functions seen here. Using timeit (thanks Mike!) the
execution time of all of them were measured by calculating the factorial
of 800 and 4000. First, the functions: [sourcecode language='python']def
fac\_01(n): result = 1 for i in xrange(2, n+1): result \*= i return
result def fac\_02(n): value = reduce(lambda i, j : i \* j, range(1, n +
1)) return value def fac\_03(n): import operator value =
reduce(operator.mul, xrange(2, n + 1)) return value def fac\_04(n): fac
= lambda n:n-1 + abs(n-1) and fac(n-1)\*long(n) or 1 return fac(n) def
fac\_05(n): fac = lambda n:[1,0][n\>0] or fac(n-1)\*n return fac(n) def
fac\_06(n): fac = lambda n:reduce(lambda a,b:a\*(b+1),range(n),1) return
fac(n) def fac\_07(n): fac=lambda n: [1, 0][n \> 0] or reduce(lambda x,
y: x\*y, xrange(1,n + 1)) return fac(n) def fac\_08(n): fac = lambda n:
n <= 0 or reduce(lambda a, b: a\*b, xrange(1,n + 1)) return fac(n) def
fac\_09(n): fac = lambda n: [[[j for j in (j \* i,)][0] for i in
range(2, n+1)][-1] for j in (1,)][0] return fac(n) def fac\_10(n): fac =
lambda n: [j for j in [1] for i in range(2, n+1) for j in [j \* i]] [-1]
return fac(n)[/sourcecode] `fac_01` was suggested by bearophile on a
comment (no psyco import here), `fac_02` was the first one we have seen
in the blog, `fac_03` was the one "selected as the fastest" (mentioned
on comments too) and functions 4 to 10 were gathered from the cookbook,
all of them using `lambda`. Now, to the results (no fancy graphs, yet),
average over 1000 repeats, time in seconds: *800!* fac\_01: **0.0010**
fac\_02: 0.0012 fac\_03: **0.0010** fac\_04: 0.0022 fac\_05: 0.0020
fac\_06: 0.0015 fac\_07: 0.0013 fac\_08: 0.0013 fac\_09: 0.0017 fac\_10:
0.0015 *4000!* fac\_01: **0.0226** fac\_02: 0.0242 fac\_03: **0.0230**
fac\_04: N/A fac\_05: N/A fac\_06: 0.0244 fac\_07: 0.0239 fac\_08:
0.0241 fac\_09: 0.0380 fac\_10: 0.0362 In both cases the "best"
functions were 1 and 3. For the smallest factorial (800!) 1 and 3 didn't
have a lot of advantage for 2, 6-10, while 4 and 5 were 2 times slower.
For the largest factorial (4000!) 1 was 4% better than 3, and the third
best (6) was also 4% slower than 3. Why do 4 and 5 have no computed
time? Because they are recursive and it blows the recursion limit in
Python. So I guess it is a safe bet to use either function 1 or 3, with
a slightly advantage for 3 in the case of large factorials. But at the
same time a believe for our case of overrepresented motifs, it would be
better to pre-calculate the factorials, store them and access the value
when needed. Andrew's idea of using binomials is also interesting, and I
am planning to test it here. He also gave a couple of other suggestions
that would need extra imports, scipy and gmpy.
[![Zemanta
Pixie](http://img.zemanta.com/reblog_a.png?x-id=72874bf9-9341-4e3e-9894-07c59d4cbd5a)](http://reblog.zemanta.com/zemified/72874bf9-9341-4e3e-9894-07c59d4cbd5a/ "Zemified by Zemanta")
