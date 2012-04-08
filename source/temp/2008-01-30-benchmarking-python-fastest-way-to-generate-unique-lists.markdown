---
author: admin
date: '2008-01-30 13:13:29'
layout: post
slug: benchmarking-python-fastest-way-to-generate-unique-lists
status: publish
title: 'Benchmarking Python: fastest way to generate unique lists'
wordpress_id: '76'
? ''
: - benchmark
  - lists
  - Phase 2
  - python
  - sets
  - Uncategorized
  - unique
---

Just for fun, let's see if there is any advantage (apart from generating
a smaller code) in using either of the approaches to create an unique
list. A list of 741 gene IDs and another one with 1322 (that contained
all the 741 IDs from the first) were used. Instead of hard coding the
lists in the script, normal I/O was used and the files were read
automatically. Using a for loop the scripts were run 10 times and the
final time averaged. Here are the results Using dictionaries 0.08540
Using sets 0.15890 Almost twice as fast for the dictionaries. Why? One
thing, and one thing only: Python version. My system's box default
Python is 2.3.4, which has one of the first implementations of `set`. I
have a "personal" Python version 2.5 so the test was redone with the
newer Python Using dictionaries 0.04520 Using sets 0.03770 Ok. That
shows a little bit of advantage for `sets` what is expected. But it
shows us that different versions of Python have a huge difference
between them. This is a rather crude and simple test, with a small list
of entries, but there is a huge gain from version 2.3 to versio 2.5,
either in `dicts` or `sets`. For a more comprehensive test and more
functions with a similar objective check this
[page](http://www.peterbe.com/plog/uniqifiers-benchmark).
