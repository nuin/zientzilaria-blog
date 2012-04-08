---
author: admin
date: '2008-01-29 22:34:21'
layout: post
slug: uniquifying-lists-with-sets-and-dictionaries
status: publish
title: Uniquifying lists with sets and dictionaries
wordpress_id: '75'
? ''
: - Phase 2
---

We are going to use our previous example to compare the use of `sets`
and `dictionaries` to create unique lists. We've already seen that when
`sets` are used it is very simple to transform a `list` with repeated
items in a unique `list`. The only hassle is to create the `set` and
then transform it back into a `list`. Like last time (with one small
addition) [sourcecode language='python']from sets import Set cluster1 =
open(sys.argv[1]).readlines() cluster2 = open(sys.argv[2]).readlines()
allgenes = cluster1 + cluster2 uniqueset = Set(allgenes) finalist =
list(uniqueset)[/sourcecode] We can accomplish identical result by using
a `dictionary`. We create a small function to make our code clearer and
pass a list to it and we return the `dictionary` keys. Rmember that
Python `dictionaries` have values and keys and the latter cannot be
repeated, so it is basically a list of unique entries. Our function
would look like [sourcecode language='python']def
make\_unique\_list(mylist): dict = {} for word in mylist: dict[word] = 1
return dict.keys()[/sourcecode] In this function we declare the object
and in the loop, iterating over every list's item we assign a value
(arbitrary) to the dictionary key. As pointed above, no repeated keys
are allowed, so everytime a already checked item is seen by the
assignment it is not included in the dictionary. Finally we return only
the dictionary keys which is our final unique list. Our small script
would be: [sourcecode language='python']cluster1 =
open(sys.argv[1]).readlines() cluster2 = open(sys.argv[2]).readlines()
allgenes = cluster1 + cluster2 allgenes =
make\_unique\_list(allgenes)[/sourcecode] Both methods are very
effective and usually fast. I will post some comparisons and benchmarks,
just for fun. Nathan posted in the comments another approach using
dictionaries. It is below with syntax highlighting [sourcecode
language='python']dict.fromkeys(mylist).keys()[/sourcecode] Basically in
one line you pass a list of elements to dictionary and return all the
keys that are in the dic. Very Pythonic.
