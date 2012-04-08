---
author: admin
date: '2007-02-12 14:18:03'
layout: post
slug: manipulating-python-lists-ii
status: publish
title: '"Manipulating" Python lists II'
wordpress_id: '14'
? ''
: - Section 1
---

As mentioned we will see in this entry some other features of Python
lists. We will start with a similar example to the one in the book and
then use our DNA file. So let's assume we have this simple list
[sourcecode language='python']nucleotides = [ 'A', 'C', 'G',
'T'][/sourcecode] If we print it directly we would get something like
this [sourcecode language='python']['A', 'C', 'G', 'T'][/sourcecode]
which is fine for now, as we are not worried (yet) with the output (what
we will do further below). Let's remove the last nucleotide. To
accomplish that, we use `pop` with no specific index [sourcecode
language='python']nucleotides.pop()[/sourcecode] which gives me this
when printed [sourcecode language='python']['A', 'C', 'G'][/sourcecode]
Remember that lists are mutable, so the removed item is lost. We can
also remove any other in the list, let's say 'C'. First, we reassign the
original list items and then remove the second item [sourcecode
language='python']nucleotides = [ 'A', 'C', 'G'. 'T']
nucleotides.pop(1)[/sourcecode] The list when printed will return this
[sourcecode language='python']['A', 'G', 'T'][/sourcecode] `pop` accepts
any valid index of the list. Any index larger that the length of the
list will return an error. For future reference, remember that when any
item is removed (and inserted) the indexes change and the length also.
It may seems obvious but mistakes are common. Shifting from our
'destructive' mode, we cal also add elements to the list. Adding to the
end of the list is trivial, by using `append` [sourcecode
language='python']nucleotides = [ 'A', 'C', 'G'. 'T']
nucleotides.append('A')[/sourcecode] that returns [sourcecode
language='python']nucleotides = [ 'A', 'C', 'G'. 'T', 'A'][/sourcecode]
Adding to any position is also very straightforward with `insert`, like
this [sourcecode language='python']nucleotides = [ 'A', 'C', 'G'. 'T']
nucleotides.insert(0, 'A')[/sourcecode] where `insert` takes two
arguments: first is the index of the element before which to insert and
second the element to be inserted. So our line above will insert an 'A'
just before the 'A' at position zero. We can try this [sourcecode
language='python']nucleotides = [ 'A', 'C', 'G'. 'T']
nucleotides.insert(0, 'A1') nucleotides.insert(2, 'C1')
nucleotides.insert(4, 'G1') nucleotides.insert(6, 'T1')[/sourcecode]
that will result in [sourcecode language='python']['A1', 'A', 'C1', 'C',
'T1', 'T', 'G1', 'G'][/sourcecode] Notice that we add every new item at
an even position, due to the fact that for every insertion the list's
length and indexes change. And for last, we will take care of the
output. Of course if are creating a script that requires a nicer output,
printing a list is not the best way. We could create a loop and merge
all entries in the list, but that would be a couple of lines and we
ought to have an easier way (otherwise we could be using C++ instead).
There is a way, by using the method `join`. This method will join all
the elements in a list into a single string, with a selected delimiter.
[sourcecode language='python']nucleotides = [ 'A', 'C', 'G'. 'T']
"".join(nucleotides)[/sourcecode] will generate this output [sourcecode
language='python']ACGT[/sourcecode] `join` is a method that applies to
strings. The first "item" is a string, that could be anything (in our
case is an empty one). The code line tells Python to get the empty
string an join it to the list of strings that we call nucleotides. With
this we finish the first section of the site and we are moving to
chapter 5 in the book.
