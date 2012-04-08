---
author: Paulo Nuin
date: '2007-10-03 16:25:16'
layout: post
slug: genbank-parsing-some-features-and-a-change-for-the-future
status: publish
title: 'GenBank: parsing some features (and a change for the future)'
wordpress_id: '58'
? ''
: - Section 7
---

This is the last entry based on the book. In my opinion, further topics
in the book are a little bit redundant and can be accomplished quite
easily if you have followed the tutorial here. 

If a good number of
people have interest in checking the remainder of the book, just let me
know and I will get back and follow the book. At the same time I am
accepting suggestions on topics to be covered (send me an email or leave
a comment). I already have some in mind and I am preparing a couple for
the next phase of the website. So, here is the last entry. Last time we
saw how to extract the sequence from a GenBank file. 

This time we are
going to parse some other information from these files. Basically we
will use the same idea of our last post to extract the Organism name,
the Locus and the Accession number of the item. From our last entry we
have to remember this 


{% codeblock lang:python %}sequence = ''
issequence = False
for line in gbfile: 
	if issequence == True and not line.find('/') == 0: 
		sequence += line.lstrip('0123456789 ').replace(' ', '')
	elif line.find('ORIGIN') >= 0: 
		issequence = True{% endcodeblock %} 
		
and modify it to our needs. Looks simple, and it is. Let's see 

{% codeblock lang:python %}import sys gbfile = open(sys.argv[1], 'r').readlines()
locus = '' 
organism = ''
 accession = '' 

for line in gbfile: 
	if line.find('LOCUS') >= 0: 
		locus = line 
	elif line.find('ACCESSION') >= 0: 
		accession = line 
	elif line.find('ORGANISM') >= 0: 
		organism = line
print locus.strip() 
print organism.strip() 
print accession.strip(){% endcodeblock %} 


Just add a flag for each entry you want
to parse and that's it. For longer entries, such as the sequence, we
have to use the same approach used before, with a boolean flag and
concatenating the lines until another flag is found. 


------------- 

Well, that's it. After 46 entries we start a new phase.
