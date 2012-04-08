---
author: admin
date: '2007-01-23 13:52:30'
layout: post
slug: transcribing-the-other-way
status: publish
title: 'Transcribing: the "other" way'
wordpress_id: '10'
? ''
: - bioinformatics
  - python
  - Section 1
  - transcribe DNA
---

We have seen how to transcribe DNA using regular expression, even though
the regex we used cannot be considered a real one. Now we are going to
simplify our small script even more and take advantage of some string
capabilities of Python. Instead of using two lines, we are going to use
only one. And also we won't need to import anything. Let's start again
with the same DNA sequence [sourcecode language='python']myDNA =
'ACGTTGCAACGTTGCAACGTTGCA'[/sourcecode] This time we are going to use
`replace`. This is one of the Python's methods to manipulate strings.
Basically, we are asking the interpreter to replace a certain string by
another. The method returns a new copy of your string: [sourcecode
language='python']myRNA = myDNA.replace('T', 'U')[/sourcecode] This
tells Python: `myRNA` will receive a copy of `myDNA` where all Ts were
changed by Us. the "dot" after `myDNA` means that the method `replace`
will get that variable as input on that variable. So our code from above
would like this [sourcecode language='python']\#! /usr/bin/env python
myDNA = 'ACGTTGCAACGTTGCAACGTTGCA' myRNA = myDNA.replace('T', 'U') print
myRNA[/sourcecode] Simple and efficient. Next we will use the same
approach on generating the reverse complement of a DNA sequence, with no
regex pattern.
