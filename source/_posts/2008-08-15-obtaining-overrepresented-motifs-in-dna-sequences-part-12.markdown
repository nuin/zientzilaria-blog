---
author: Paulo Nuin
date: '2008-08-15 17:15:21'
layout: post
slug: obtaining-overrepresented-motifs-in-dna-sequences-part-12
status: publish
title: Obtaining overrepresented motifs in DNA sequences, part 12.5
wordpress_id: '137'
? ''
: - binomial
  - bioinformatics
  - factorial
  - motifs
  - Phase 2
  - python
---

So let's modify a little bit the [factorial function](http://en.wikipedia.org/wiki/Factorial "Factorial") and then
benchmark both by using `timeit`. Ideally our factorial function would
need to calculate a value similar to the [binomial expansion](http://en.wikipedia.org/wiki/Binomial_theorem "Binomial theorem"),
as we have three factorials to calculate in for each binomial in the
Hypergeometric Distribution. So we can add two extra factorial
calculations to our function and perform the multiplication and division
to return the equivalent to the binomial calculation. So the function
would be 


{% codeblock lang:python %}def fac(n, m):
	value1 = 1 
	for i in xrange(2, n + 1): 
		value1 *= i 
		value2 = 1 
	
	for i in xrange(2, m + 1):
		value2 *= i 
		value3 = 1 
		
	for i in xrange(2, (n - m) + 1): 
		value3 *= i
	
	return value1 / (value2 * value3){% endcodeblock %}


 `m` and `n` are both values of the binomial and `n - m` is the subtraction of one by the
other that forms the last factorial to be calculated. This way it makes
easier to time the performance of both functions. In the end the
complete script would look like 


{% codeblock lang:python %}\#!/usr/bin/env python 
import timeit 

def fac(n, m):
	result1 = 1
	for i in xrange(2, n + 1): 
	
	result1 *= i result2 = 1 for i
in xrange(2, m + 1): result2 *= i result3 = 1 for i in xrange(2, (n -
m) + 1): result3 *= i return result1 / (result2 * result3) def
binom(n, m): b = [0] * (n + 1) b[0] = 1 for i in xrange(1, n + 1): b[i]
= 1 j = i - 1 while j \> 0: b[j] += b[j - 1] j -= 1 return b[m] def
choose(n, k): if 0 <= k <= n: ntok = 1 ktok = 1 for t in xrange(1,
min(k, n - k) + 1): ntok *= n ktok *= t n -= 1 \#print ntok // ktok
return ntok // ktok else: return 0 if \_\_name\_\_ == "\_\_main\_\_":
stmt = "fac(3000, 7)" t = timeit.Timer(stmt = stmt, setup='from
\_\_main\_\_ import fac') stmt2 = "binom(3000, 7)" t2 =
timeit.Timer(stmt = stmt2, setup = 'from \_\_main\_\_ import binom')
stmt3 = "choose(3000, 7)" t3 = timeit.Timer(stmt = stmt3, setup = 'from
\_\_main\_\_ import choose') print 'fac: %.9f' % (t.timeit(100)/100)
print 'binom: %.2f' % (t2.timeit(10)/10) print 'choose %.9f' %
(t3.timeit(100)/100){% endcodeblock %} 

The final result of the average for
ten repetitions is as follow fac = 0.10 s binom = 43.24 s choose =
0.000005 s ~~Clearly, the factorial function gets a huge advantage over
the binomial one. So we will modify it a little bit and use it for our
HD script.~~ Clearly the `choose` function is the fastest one, so we
will incorporate it on out HD script.
