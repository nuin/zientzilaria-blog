---
author: admin
date: '2008-03-17 16:31:43'
layout: post
slug: python-sets-intersections-reduce-and-more
status: publish
title: Python sets, intersections, reduce and more
wordpress_id: '91'
? ''
: - asterisks
  - intersection
  - Phase 2
  - python
  - reduce
  - sets
---

Last time we saw how to use a set intersection to check for clusters of
DNA/protein sequences and their genome intersections. We going to use
the same example but this time we will see how we can change it and
create a function that would calculate an arbitrary number of
intersections at a time and also be able to check the intersection of
more than two sets. Our previous code to calculate intersections was


{% codeblock lang:python %}from sets import Set 
#for Python 2.3 and below 
genA, genB, genC = Set([]), Set([]), Set([]) 
#populate the sets ... 


print len(Set.intersection(genA, genB)) 
print len(Set.intersection(genA, genC)) 
print len(Set.intersection(genB, genC)){% endcodeblock %} 


and that's does not gives us the most important
piece of information: the intersection of A, B and C. Let's see how we
can do it. Python has a function that can help us this time: `reduce`.
This function allows to reduce a series of values to a single one, by
employing a function defined in its parameters. From the file tutorial


{% codeblock lang:python %}reduce(function, iterable[,initializer]){% endcodeblock %} 

Basically `reduce` will make the function
modify the values of a iterable (i.e. list). In our case `reduce` helps
us calculate the intersection of many sets at once (our sets are `genA`,
`genB` and `genC`) 

{% codeblock lang:python %}reduce(Set.intersection, [genA, genB, genC]){% endcodeblock %}

 where `reduce` is applying the `Set` method
intersection to a list of sets passed to the function. Python's `reduce`
might not be available in 3.0, but it is worth knowing. Now that we have
a Pythonic way of checking the intersections we need to put `reduce` in
a function, to make our code more elegant. 

{% codeblock lang:python %}def get_intersection(my_set1, my_set2, my_set3):
	return reduce(Set.intersection, [my_set1, my_set2, my_set3]){% endcodeblock %}

Done. In this function `reduce` will operate by
first checking the intersection between `my_set1` and `my_set2` and
storing it internally, then checking for the intersection between the
previous result and `my_set3`. But wait ... `get_intersection` receives
three arguments, so it will be able to return the intersection only when
three sets are sent, thus we would have to create another function that
can receive two items in order to calculate the intersection between two
items. And if we have more than three genomes to compare ... There is a
[trick](http://farmdev.com/thoughts/24/what-does-the-def-star-variable-or-def-asterisk-parameter-syntax-do-in-python-/).
If we define our function receiving only one argument and put a
star/asterisk on it, this means that an arbitrary number of arguments
will be provided to this function in a tuple (and a tuple is iterable,
so it can be used in a reduce). Changing our function accordingly, we
will have 

{% codeblock lang:python %}def get_intersection(*my_sets): 
	return reduce(Set.intersection, my_sets){% endcodeblock %} 

so we can send 2, 3, 4, 5 or *n* number of sets
to this function and it will return the intersection among all of them.
Our simple script would be (including the above function) 

{% codeblock lang:python %}from sets import Set 
#for Python 2.3 and below 
def get_intersection(*my_sets): 
	return reduce(Set.intersection, my_sets)

genA, genB, genC = Set([]), Set([]), Set([]) 

#populate the sets ...

print len(get_intersection(genA, genB)) 
print len(get_intersection(genA, genC)) 
print len(get_intersection(genB, genC)) 
print len(get_intersection(genA, genB, genC)){% endcodeblock %}
