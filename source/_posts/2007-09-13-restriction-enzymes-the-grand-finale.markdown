---
author: Paulo Nuin
date: '2007-09-13 16:17:28'
layout: post
slug: restriction-enzymes-the-grand-finale
status: publish
title: 'Restriction enzymes: the grand finale'
wordpress_id: '54'
? ''
: - Section 6
---

We get to the last piece of the puzzle. On the last four posts we have
seen each part of the restriction enzyme site searcher script, and now
we put everything together. If someone is also following the book, will
see that the Python code we are producing here is slightly different,
but in essence achieves the same result. 


Ok, we saw last time that the
function which searches for the enzyme sites returns a tuple with the
actual sites and positions. Why is it better to return sites and
positions? Because one enzyme can have multiple sites and you might want
to know where are they. Also, it helps us practice some Python skills.
We will start by the last piece, and part of it we already saw before.

{% codeblock lang:python %}'
if isname: 
	print 'Name found'
	sequences = fasta.read_fasta(open(sys.argv[2], 'r').readlines()) 
	for item in sequences:
	 	sites, positions = find_sites(enzyme, enzymeset, item.sequence) 
		print item.name[:20]+'...' 
		for i in zip(sites, positions): 
			print i[0], '->', i[1] 
else: 
	print 'Enzyme name not found, please try again'{% endcodeblock %}

This is the `if` that checks to see if
the input enzyme name was found in the list. Clearly we added a couple
of things. Already covered here, if `isname` is true we go and read the
sequence file, which can contain a single or multiple sequences. We
start a loop and call the `find_sites` and expect the return on a tuple
`sites, positions`. Next line, we print the sequence name for the
output. And then ... Yes, and then we have something new: `zip`. This is
a function that returns a list of tuples from each one of the arguments
passed to it. In our case we are passing two lists (sites and positions)
and we know that each site has one position, and we also know that
because of the way we build both lists the i-th element in sites will be
equivalent to the i-th element in positions. Using `zip` we create n
tuples where the i-th tuple is equivalent to the i-th element in sites
and the i-th element in positions. 

Confused? Let's see. Imagine that sites has is composed of 

{% codeblock lang:python %}['AAA', 'AAC', 'ACA', 'TAA']{% endcodeblock %}

and positions is composed of 

{% codeblock lang:python %}['300', '454', '23', '345']{% endcodeblock %} 

and we want
to ouput this `AAA -> 300 AAC -> 454 ACA -> 23 TAA -> 345` The first
idea that comes to mind is to do a loop, with a range as we already know
that both lists will have the same size. Something in the lines of


{% codeblock lang:python %}for i in range(len(positions)): 
	print sites[i], '->', positions[i]{% endcodeblock %} 

and it will work fine and it
is not that long (codewise). `zip` might not be an advantage here, but
it will be somewhere else, for sure. We print the results and we are
done. The full code will be posted in the repository soon. Next we will
move to the book's chapter 10 and we start a new section here, checking
for GenBank files.
