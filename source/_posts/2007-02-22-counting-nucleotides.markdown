---
author: admin
date: '2007-02-22 14:48:35'
layout: post
slug: counting-nucleotides
status: publish
title: Counting nucleotides
wordpress_id: '19'
? ''
: - Section 2
---

We are going to jump the regular expression explanation that you can
find in the book, and we will go directly to the section that introduces
string/list/array manipulation and adapt it to Python. We are going to
see two different methods: a "long" and a "short" one. In many places
and computer languages you will see that there are different ways of
doing the same thing, with advantages and disadvantages. It is up to you
to define which methods are better or worse, as this is a very personal
matter. Some people prefer the longer way because it might be clearer
and easier to understand, or it might be necessary to use it due to code
maintainability. Other people would rather use the shorter path because
they want to generate code faster. It does not matter the path you
select, as long as you get your task done. That's the key: focus on the
end product not on how exactly got there. If you used 10 lines of code
more, or 10 less, that's irrelevant as long as you did what you wanted.
Live and learn and someday you will use the even shorter way. So we
start with the long way. We want to count the individual number of
nucleotides in a sequence, determining they relative frequency. Remember
that we read the lines of a sequence file into a list, using
`readlines`. But on the long method we will read the file and store the
data into a string like 

{% codeblock lang:python %}file = open(filename, 'r')
sequence = ''
for line in file:
    sequence += line{% endcodeblock %} 

This way it will be easier to "explode" the sequence
in separated items. After the "explosion" we can check each item in the
list and get our result. The code is below, I will be back after it.

{% codeblock lang:python %}#!/usr/bin/env python
#let's keep the file fixed for now
dnafile = "AY162388.seq"
#opening the file, reading the sequence and storing in a list
file = open(dnafile, 'r')
#initialize a string to receive the data
sequence = ''
for line in file:
    sequence += line.strip() #notice the strip, to remove \n
#"exploding" the sequence in a list
seqlist = list(sequence)
#initializing integers to store the counts
totalA = 0
totalC = 0
totalG = 0
totalT = 0
#checking each item in the list and updating counts
for base in seqlist:
    if base == 'A':
        totalA += 1
    elif base == 'C':
        totalC += 1
    elif base == 'G':
        totalG += 1
    elif base == 'T':
        totalT += 1
#printing results
print str(totalA) + ' As found'
print str(totalC) + ' Cs found'
print str(totalG) + ' Gs found'
print str(totalT) + ' Ts found'
{% endcodeblock %} 

Most of the above code was already covered before.
Let's look at the different stuff, like the "explosion line" 

{% codeblock lang:python %}seqlist = list(sequence){% endcodeblock %} 

Here we basically transform our string `sequence` into a list, by putting the
object type we want before the object we want converted, like we do here

{% codeblock lang:python %}print str(totalA) + ' As found'{% endcodeblock %}

This construction `type_to_convert(to_be_converted)`
tells Python to get whatever is inside the parentheses and transform
into whatever is outside. Converting the string to a list will get


{% codeblock lang:python %}GTGACTTTGTTCAACGGCCGCGGTATCCTAACCGT
GCGAAGGTAGCGTAATCACTTGTTCTTTAAATAAGGACTAGTATG
AATGGCATCACGAGGGCTTTACTGTCTCCTTTTTCTAATCAGTGAA ...{% endcodeblock %} 

and transform it into 

{% codeblock lang:python %}['G', 'T', 'G', 'A',
'C', 'T', 'T', 'T', 'G', 'T', 'T', 'C', 'A', 'A', 'C', 'G', 'G', 'C',
'C', 'G', 'C', 'G', 'G', 'T', 'A', 'T', 'C', 'C', 'T', 'A', 'A', 'C',
'C', 'G', 'T', 'G', 'C', 'G', 'A', 'A', 'G', 'G', 'T', 'A', 'G', 'C',
'G', 'T', 'A', 'A', 'T', 'C', 'A', 'C', 'T', 'T', 'G', 'T', 'T', 'C',
'T', 'T', 'T', 'A', 'A', 'A', 'T', 'A', 'A', 'G', 'G', 'A', 'C', 'T',
'A', 'G', 'T', 'A', 'T', 'G', 'A', 'A', 'T', 'G', 'G', 'C', 'A',
'T',...]{% endcodeblock %} 

After "exploding", we use a `for` loop to iterate
over every item in the list and use conditional statements to do the
counts. Regarding the counts, we use this operator 

{% codeblock lang:python %}totalT += 1{% endcodeblock %} 

that, in C/C++, tells the
interpreter to get the value of `totalT` and add 1 to it.
