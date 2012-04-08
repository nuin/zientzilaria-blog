---
author: admin
date: '2007-09-07 16:48:50'
layout: post
slug: restrinction-enzymes-second-take
status: publish
title: 'Restriction enzymes: second take'
wordpress_id: '51'
? ''
: - Section 6
---

We already have a function that reads the enzymes from a dataset in a
flat file (with one change: return) 


{% codeblock lang:python %}def read_enzymes(file): 
	resenz = {} 
	start = False 
	for line in file: 
		if line.find('Rich Roberts') >= 0: 
			start = True 
			line = file.next() 
			if start == True and len(line) > 10:
				buffer = line.split() 
				resenz[buffer[0]] = buffer[-1].replace('\^', '')
				
	return resenz{% endcodeblock %} 
	
We now need a function to write a function
that searches for the sites and a main function that accepts the
parameters, coordinate the search and return the results. Looks like we
are more than halfway there. Parameters input was shown before, starting
on section 3. We import the `sys` module and use the array inside
`sys.argv` to send the parameters to the script. A basic skeleton of our
main function would look like this 

{% codeblock lang:python %}import sys 
import re 
import fasta 
#reading the ezyme dataset in one line and storing enzyme information in enzymeset 
enzymeset = read_enzymes(open('bionet.709', 'r')) 
#storing enzyme name on a string
enzyme = sys.argv[1] 
#reading a FASTA file and storing the sequences
sequence = fasta.get\_seqs(open(sys.argv[2],'r').readlines()){% endcodeblock %} 

That's a start. Now we have to write a
function that will check for the enzyme name entered by the user in
order to check for the existence of such enzyme. Something like this
would work 

{% codeblock lang:python %}def check_enzyme(input, set):
	if set.has_key(input):
		return True 
	else: 
		return False{% endcodeblock %} 

This
basically tests of the dictionary contains the name entered. If yes then
we return True, otherwise False is returned. This changes our main
script body {% codeblock lang:python %}import sys 
import re 
import fasta 
#reading the ezyme dataset in one line and storing enzyme information in enzymeset 
enzymeset = read\_enzymes(open('bionet.709','r')) 
#storing enzyme name on a string 
enzyme = sys.argv[1] 
#check if the name entered is valid 
isname = check_enzyme(enzyme, enzymeset) 
#if it is valid, continue, otherwise abort 
if isname:
	#reading a FASTA file and storing the sequences 
	sequence = fasta.get_seqs(open(sys.argv[2], 'r').readlines())
else: 
	print 'Name invalid. Please try again.'{% endcodeblock %}

So, we have a good idea on what to do now. We just need a function that creates a
regular expression and searches it on the sequence. Next time ...
