---
author: admin
date: '2007-04-02 12:57:24'
layout: post
slug: random-sequences-in-python
status: publish
title: Random sequences in Python
wordpress_id: '32'
? ''
: - Section 4
---

There is a reason to say that Python has batteries included. On the last
post we have seen a small example of randomization in Python, generating
random integer values for a (extremely) simple dice game. We move to
another example, still simple which will allow us to generate random DNA
sequences. The script is 

{% codeblock lang:python %}#!/usr/bin/env python 
import random 
import sys 
length = int(sys.argv[1])
dnaseq = list('ACGTACGTACGTACGTACGTACGTACGTACGTACGTACGTACGTACGTACGTACGT') 
result = '' 
for i in range(length): 
    result += random.choice(dnaseq) 

print result{% endcodeblock %} 

Not fancy at all, just plain simple (yet again). We
import a couple of modules, `sys` and `random`, and ask for the sequence
length as a script parameter. `dnaseq` is a list containing a tandem
repeat of ACGT, and from there we will extract our random nucleotides.
In fact `dnaseq` could have been 'ACGT' only. The fact that we create a
string and convert it to a list, is just for convenience of writing
`'ACGT...'` easier than `['A', 'C' ...]`. We then declare an empty
string that will be used to store the random sequence. And inside the
loop, the command that does all the magic: `random.choice()`. This
command will return a random element from the list passed as subject.
Using it inside a loop we will get a random nucleotide on each iteration
and add it to our string. This is a very simple command, but at the same
time extremely powerful and easy to implement. A good exercise from this
would be to modify the `dnaseq` string and see if there is any change in
the final random sequence.
