---
author: Paulo Nuin
date: '2008-03-11 16:23:47'
layout: post
slug: fasta-module-transcribing-dna
status: publish
title: 'Fasta module: transcribing DNA'
wordpress_id: '89'
? ''
: - bioinformatics
  - dna
  - Phase 2
  - python
  - RNA transcribe
---

A long time ago when the blog was still based on the Perl book we have
seen [how to transcribe DNA to RNA](http://python.genedrift.org/2007/01/23/transcribing-the-other-way/).
This entry serves only to remember the method and add a function to the
`fasta` module in the repository. It is really simple to transcribe in
Python, by employing the `replace` method on strings. Our function looks
like 

{% codeblock lang:python %}def transcribe(seq): 
	RNA = seq.replace('T', 'U') 
	return RNA{% endcodeblock %} 

Some other functions will
be added to the module in the next couple of weeks. After that we will
divert the focus on optimizing our GenBank parsing script.
