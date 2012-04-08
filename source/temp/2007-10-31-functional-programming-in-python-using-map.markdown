---
author: admin
date: '2007-10-31 13:33:59'
layout: post
slug: functional-programming-in-python-using-map
status: publish
title: 'Functional programming in Python: using map'
wordpress_id: '69'
? ''
: - Phase 2
---

Functional programming in Python. First we need to define what is
functional programming. Quoting
[Wikipedia](http://en.wikipedia.org/wiki/Functional_programming): "is a
programming paradigm that treats computation as the evaluation of
mathematical functions and avoids state and mutable data. It emphasizes
the application of functions, in contrast with the imperative
programming style that emphasizes changes in state." Rather complex, eh?
Another explanation can be found
[here](http://www.cs.nott.ac.uk/~gmh/faq.html#general-topics):
"Functional programming is a style of programming that emphasizes the
evaluation of expressions, rather than execution of commands. The
expressions in these language are formed by using functions to combine
basic values. A functional language is a language that supports and
encourages programming in a functional style." Basically any functional
programming language tries to minimize the code, reducing it, avoiding
the use of variables and relying on the use of functions and
expressions. Python, clearly, is a not a functional programming language
*per se*, but it has some functions that allow a functional approach. We
will see a couple of them in this entry. If you are interested in
learning more about functional programming and Python, check Alan
Gauld's
[tutorial](http://www.freenetpages.co.uk/hp/alan.gauld/tutfctnl.htm).
There are many ways to use functional programming in bioinformatics. We
will start with a very simple example, but first we need to modify the
FASTA module we created before. Currently this module only has two
functions, one that reads sequences and their names and one tha formats
their output. We will add a function that reads only the sequences and
returns a list containing them. This function is very similar to the
`read_fasta` function [sourcecode language='python']def
read\_seqs(file): items = [] seq = '' index = 0 for line in file: if
line.startswith("\>"): if index \>= 1: items.append(seq) seq = '' index
+= 1 else: seq += line[:-1] items.append(seq) return items[/sourcecode]
and it uses an identical approach. Instead of creating an instance of
`Fasta` class we only create a simple list, and ignore the sequence
title. This will also be useful for a future code reuse, as sometimes we
are only interested in the sequence itself and not the name. Might save
us some typing and decrease code size depending on the situation. In
this entry we will see one Python's functional programming function:
`map`. But we will need to use another one too, which is called
`lambda`. `lambda` is the function that defines what is called an
anonymous function, or a nameless function that can fit in one line. We
have seen that functional programming is all about functions, so
`lambda` is the aid to implement the small and short functions we use in
this type of approach. One example of `lambda` use would be on the
calculation of number exponentials, which normally can be achieved like
this [sourcecode language='python']def exp(value): return
value\*\*2[/sourcecode] (exponentials in Python are defined by \*\*)
Using `lambda` we can rewrite the above function like [sourcecode
language='python']exp = lambda value:value\*\*2[/sourcecode] with the
following syntax:
` lambda [parameters] : [expression to be used on the parameters] ` In
both cases you can use the functions the same way, by calling `exp(10)`
for example. Ok, let's move to `map` then. `map` applies a function,
usually a `lambda`, to every item in a list of items. This list can be
of any sequence type, but `map` always returns a list. Using the above
exponential example, let's say we want to calculate the cube of a series
of values. Using `map` and `lambda` we would have something like this
[sourcecode language='python']print map(lambda value:value\*\*2,
[2,5,12,34,56]) [4, 25, 144, 1156, 3136][/sourcecode] And that's it.
Dissecting this line of code, we have a `lambda` function that due to
the use of the `map` function is applied on every item of the list that
follows. This list can be anything, previously set or not. So, applying
this to a bioinformatics example would be simple (this might not be the
most useful or real-world example ever, but it should give us a primer
to endeavour in more advanced stuff). Let's say we want to check
sequence size for all sequences in a FASTA file. Emphasizing code reuse,
we created a new function that returns a list of the actual sequences
only. Without functional programming a loop to read the sequence lengths
would be very simple [sourcecode language='python']for sequence in seq:
print len(sequence)[/sourcecode] With a functional programming approach,
we can do it in one line (not a large advantage here) [sourcecode
language='python']print map(lambda x:len(x), data)[/sourcecode] Yep, not
a lot of gain with this example, as mentioned. The full script would
look like [sourcecode language='python']\#! /usr/bin/env python import
fasta import sys data = fasta.read\_seqs(open(sys.argv[1],
'r').readlines()) print map(lambda seq:len(seq), data)[/sourcecode]
`data` is our list of sequences, and inside the `map` function we have a
`lambda` that checks for the size of each sequence in that list. Quite
simple.
