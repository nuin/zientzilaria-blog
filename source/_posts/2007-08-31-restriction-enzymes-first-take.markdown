---
author: Paulo Nuin
date: '2007-08-31 16:08:12'
layout: post
slug: restriction-enzymes-first-take
status: publish
title: 'Restriction enzymes: first take'
wordpress_id: '49'
? ''
: - Section 6
---

We now jump with both feet on the main topic of the book's chapter,
which is generating restriction maps of DNA sequences. First step is to
obtain restriction enzyme information, read it and format in a way that
our main script will understand. We will use the same dataset as the
book, the [Rebase](http://rebase.neb.com/rebase/rebase.html) database at
New England Biolabs. In the book, Tisdall suggests the download of a
*bionet* format, which can be downloaded
[here](ftp://ftp.neb.com/pub/rebase/) (scroll down to bionet.709). 

This file looks like this:


	AaaI (XmaIII)                     C^GGCCG  
	AacI (BamHI)                      GGATCC  
	AaeI (BamHI)                      GGATCC  
	AagI (ClaI)                       AT^CGAT  
	AanI (PsiI)                       TTA^TAA  
	AaqI (ApaLI)                      GTGCAC



where the first column contains the enzyme names and the second column
has the actual cleavage sites. 

It won't be difficult to parse this file
and create a dictionary with the names and sites, but it would be easier
if the file the data was tab-separated, but it is nothing we will have
problem dealing with. The file also has some header lines which we will
have to avoid. Next entry will deal with user cases and some other
aspects of coding, as we head to our most complex script until now. Noe
we will only create a function that reads the file and generates the
dictionary, what sounds very simple. There are two ways (maybe even
more) to discard the header lines: programatically or actively deleting
such lines. We won't delete the lines this time, so we have to follow
the other path. 

The easiest way to eliminate header lines from our
parsing function would be to count the lines and start the parsing
procedure after that certain number but that would mean a high
confidence of the format being constant in every release. So, first we
get rid of the header lines 


{% codeblock lang:python %}
def read_enzymes(file):
    resenz = {}
    start = False
    for line in file:
        if line.find('Rich Roberts') >= 0:
            start = True
            line = file.next()
        if start == True and len(line) > 10:
		{% endcodeblock %}


 where we already
declared the dictionary that will receive the name and sites. We have a
flag boolean that tells the script where the actual enzyme list starts
(`start`), declared as false and then modified to true when the line
containing `Rich Roberts` is found. The line `line = file.next()` tells
the script that the current line is equal to the next line of the file.
We do this to avoid starting the parsing of the file at the line we
found `Rich Roberts`. the `if` statement checks for the line size in
order to split and parse only the actual lines and discard empty ones.
Now, in order to get the sites and enzyme names we will use split,
differently than we used before. This time we won't pass any arguments
to split as a separator. This will trigger another type of splitting
procedure, where some characters will be stripped from the string
(spaces, tabs, newlines, returns, and form feeds) and the resulting words
will be then separated by arbitrary length strings of white spaces.
Basically, this split will return a list with the words in that particular
line. Inspecting the file carefully, we notice that some enzyme names
have an extra id between parentheses. We will not consider this extra
id. After splitting we will get the first and last elements of the list
and put them in our dictionary. 

{% codeblock lang:python %}buffer = line.split() 
resenz[buffer[0]] = buffer[-1].replace('\^',''){% endcodeblock %}

Done. We have the dictionary ready. And using Python's
included batteries we use the last line in the function to remove the
circumflex characters. Putting everything together we have 

{% codeblock lang:python %}
def read_enzymes(file):
    resenz = {}
    start = False
    for line in file:
        if line.find('Rich Roberts') >= 0:
            start = True
            line = file.next()
        if start == True and len(line) > 10:
            buffer = line.split()
            resenz[buffer[0]] = buffer[-1].replace('^', '')
			{% endcodeblock %}
