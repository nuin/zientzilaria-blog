---
author: admin
date: '2007-02-22 14:51:58'
layout: post
slug: counting-nucleotides-part-ii
status: publish
title: 'Counting nucleotides: part II'
wordpress_id: '20'
? ''
: - Section 2
---

Let's check the "short" way, that is basically a method that avoid the
"explosion" of the string. Instead of transforming the sequence from the
file from a string to a list, we go and use the string directly,
applying one of the methods available to manipulate strings. This time
we read the file at once and convert the list to a string using `join`.
To count we simply use the method `count` on our string. Pretty nice.

{% codeblock lang:python %}#!/usr/bin/env python 
#still keep the file fixed 
dnafile = "AY162388.seq" 
#opening the file, reading the sequence and storing in a list
seqlist = open(dnafile, 'r').readlines()
#let's join the the lines in a temporary string 
temp = ''.join(seqlist)
#counting 
totalA = temp.count('A')
totalC = temp.count('C')
totalG = temp.count('G')
totalT = temp.count('T') 
#printing results 
print str(totalA) + ' As found' 
print str(totalC) + ' Cs found' 
print str(totalG) + ' Gs found'
print str(totalT) + ' Ts found'{% endcodeblock %}


That's the short way: using `count`. This is a method that when applied
on a string counts the number of times the substring appears in our
string. We can even set a start and ending point to count. Notice one
difference in this script to the previous examples: after we join the
items of the list into a string we do not remove the carriage returns.
Because in this case we don't need it, as it will be an extra character
there that won't make any harm.
