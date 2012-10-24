---
author: Paulo Nuin
date: '2008-08-12 20:50:17'
layout: post
slug: obtaining-overrepresented-motifs-in-dna-sequences-part-11
status: publish
title: Obtaining overrepresented motifs in DNA sequences, part 11
wordpress_id: '133'
? ''
: - bioinformatics
  - hypergeometric distribution
  - motifs
  - Phase 2
  - python
---

After a long hiatus we are (almost) back on track in order to get our
scripts to determine overrepresented motifs in DNA sequences. Last time
we checked we defined the "best" [factorial function](http://en.wikipedia.org/wiki/Factorial "Factorial") in Python


{% codeblock lang:python %}
def fac_01(n):
    result = 1
    for i in xrange(2, n+1):
        result *= i
    return result

{% endcodeblock %}

 and Andrew Dalke
sent a couple of links pointing out to a binomial calculation function,
one of them is below 

{% codeblock lang:python %}\# This file contains the Python code from Program 14.10 of
# "Data Structures and Algorithms with Object-Oriented Design Patterns in Python" 
# by Bruno R. Preiss. 
## Copyright (c) 2003 by Bruno R. Preiss, P.Eng. All rights reserved. 
## http://www.brpreiss.com/books/opus7/programs/pgm14_10.txt # 

def binom(n, m): 
	b = [0] * (n + 1) 
	b[0] = 1 
	for i in xrange(1, n + 1): 
		b[i] = 1 
		j = i - 1
		while j > 0: 
			b[j] += b[j - 1] 
			j -= 1 
	
	return b[m]
{% endcodeblock %} 

There is a similar implementation in the Python Cookbook
online and it is clearly more convenient using this function than
actually coding to calculate an identical value using factorials. But
anyway, let's see how a function that calculates one binomial
coefficient from the Hypergeometric Distribution (HD) by using the
factorial function. Later we benchmark both methods. Each [binomial coefficient](http://en.wikipedia.org/wiki/Binomial_coefficient "Binomial coefficient")
can be expanded as
![image](http://codecogs.izyba.com/png.latex?%5C200dpi%20%5Cbegin%7Bpmatrix%7Dn%5C%5Cr%5Cend%7Bpmatrix%7D%20=%20%5Cfrac%7Bn!%7D%7Br!(nr)!%7D)
and the HD has three of them. From the Wikipedia "In probability theory
and statistics, the [hypergeometric distribution](http://en.wikipedia.org/wiki/Hypergeometric_distribution "Hypergeometric distribution")
is a discrete probability distribution that describes the number of
successes in a sequence of n draws from a finite population without
replacement." In the next post we will define each term of the HD for
the motifs case. In each [binomial expansion](http://en.wikipedia.org/wiki/Binomial_theorem "Binomial theorem")
we would have to calculate three factorial values, nine in total. With
the binomial function, only three values need to be calculated. So,
using the factorial function we would need to code something like this
in order to calculate one of the binomials 

{% codeblock lang:python %} 
#let's say the motif quorum in the foreground is 7
#and the total number of sequences is 3000 
#we won't touch the other required values 
fore = 7 total = 3000 
hd = fac_01(3000) / (fac_01(7) * fac_01(2993) 
print hd{% endcodeblock %}

Next, we will benchmark and see if there is an advantage to either method.
