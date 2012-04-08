---
author: admin
date: '2007-01-15 13:47:54'
layout: post
slug: importing-and-regular-expressions
status: publish
title: Importing and regular expressions
wordpress_id: '8'
? ''
: - import
  - python
  - regular expressions
  - Section 1
---

Tisdall's book on Perl introduces next the ability to transcripts DNA
sequences into RNA. In order to do that we need to check a different
aspect of programming: regular expressions (or regex). Regular
expressions is a pattern/string expression that works
matching/describing/filtering other strings. Let's say you want to
examine or extract all vowels contained in one phrase, one page, one
word. Another example would be to remove all html tags from a downloaded
webpage. As HTML tags are encapsulated between `<` and `>` signs we can
create a regex that will search for any characters in between the signs
and remove (parse) them from our page. We will deal very briefly with
regex, and if you are interested in learning more about it you can
search for countless references on the internet (such as [this
one](http://www.regular-expressions.info/)). In order to use regular
expression in Python we need to check another concept present in the
language: importing modules. Python core functionality provides most of
the usual operations and also comes with a built-in library of functions
that "access to operations that are not part of the core of the language
but are nevertheless built in". One of this operations is the ability to
interpret regular expression that in Python is located in the `re`
module. Apart from the language core, built in modules, Python can be
further extended by using third-party modules imported into the
language. Anyone can create a module and distribute to every Python user
and programmer. So, in order to have regex capabilities we literally
have to `import` the regex module. We do that by entering the line:
[sourcecode language='python']import re[/sourcecode] Python's code style
guide suggests that `import` statements should be on separate lines
[sourcecode language='python']import sys import re ...[/sourcecode] and
to be put on the top of the file (usually below the line that tells your
OS to use Python's interpreter on the script). So the first two lines of
our new script would be [sourcecode language='python']\#! /usr/bin/env
python import re[/sourcecode] Now that we have the ability to use regex,
we need to create one expression that will transcribe our DNA sequences
into RNA.
