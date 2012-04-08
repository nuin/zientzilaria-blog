---
author: admin
date: '2008-01-28 16:55:35'
layout: post
slug: python-sets
status: publish
title: Python sets
wordpress_id: '74'
? ''
: - lists
  - Phase 2
  - python
  - sets
  - unique
---

After a long hiatus we are back with more Python tips, tricks, codes and
snippets. This time we will check how `set` works in Python. `set` is
another object type available in Python (version 2.3 and up) that brings
a lot of features to the language. From the Python Library Reference: "A
set object is an unordered collection of immutable values. Common uses
include membership testing, removing duplicates from a sequence, and
computing mathematical operations such as intersection, union,
difference, and symmetric difference." Yep, all these are possible with
`set`, and let me stress that it is not duplicated. So, a `set` is
basically a collection of item, but its unordered and not indexed,
because it does not record element position or indertion order. Methods
available for a `set` include `union()`, `intersection()`,
`difference()` that we will check next time. First let's see some basic
set functionality. Differently from other commonly available Python
object types, we need to import a library in order to use `set`
[sourcecode language='python']from sets import Set[/sourcecode] should
work. A first use for `set` would be to uniquify a list. Let's say that
you have the gene IDs of two different clusters and you want to merge
these lists and keep only the unique ones, eliminating possible
duplicates IDs. We could do that with a `dictionary` and a simple
function (we will also check this later on) but a `set` makes our life
easier. [sourcecode language='python']from sets import Set cluster1 =
open(sys.argv[1]).readlines() cluster2 = open(sys.argv[2]).readlines()
allgenes = cluster1 + cluster2 uniqueset = Set(allgenes)[/sourcecode]
and that's all. Of course we won't have a flexibility of a `list`, but
we can easily convert the `set` to a list and manipulate as before. Next
time we will see what else we can do with `sets` and gene lists.
