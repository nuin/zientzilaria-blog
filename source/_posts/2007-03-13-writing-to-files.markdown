---
author: admin
date: '2007-03-13 14:58:58'
layout: post
slug: writing-to-files
status: publish
title: Writing to files
wordpress_id: '25'
? ''
: - Section 2
---

We already know how to read from files, now we are going to see how to
write to them. We will start with a simple example, writing some content
to a "fresh" file that does not exist in the system. Sometime ago, we
have seen the `print` statement in Python, that prints to the system
standard output (usually the screen). This output can be redirected
using `>` to a stream/file. But if we are going to create really
professional applications (even to our own use), usually stream
redirection is not really the nicest approach. In some cases the best
alternative is to save a file. Also, some posts ago, we covered the
methodology to `open` a file. We are going to use here the same command,
`open` to (in our case) create the file. Remember that to read the file
we used 

{% codeblock lang:python %}file = open(dnafile, 'r'){% endcodeblock %} 

where the `'r'` is the mode we are using to open the
file. In that case we used the *read* mode, now we are going to use the
*write* mode. When we open a file with this command in *write* mode if
the file (with the name with pass) does not exist it is created. If it
does exist, all the contents of the current file will be erased, so be
careful when opening a file from your script. Check for the location,
file name, etc before opening the file. So, basically we have


{% codeblock lang:python %}file = open(output, 'w'){% endcodeblock %} 

and
the file is open and ready to receive data. Let's cheat and use the
previous script that counts nucleotides and modify it to save a
`count.txt` file wit the results: 

{% codeblock lang:python %}
#!/usr/bin/env python
 
#let's keep the file fixed for now
dnafile = "AY162388.seq"
#opening the file, reading the sequence and storing in a list
file = open(dnafile, 'r')
#initialize a string to receive the data
sequence = ''
for line in file:
    sequence += line.strip() #notice the strip, to remove n
#"exploding" the sequence in a list
seqlist = list(sequence)
#initializing integers to store the counts
totalA = 0
totalC = 0
totalG = 0
totalT = 0
#checking each item in the list and updating counts
for base in seqlist:
    if base == 'A':
        totalA += 1
    elif base == 'C':
        totalC += 1
    elif base == 'G':
        totalG += 1
    elif base == 'T':
        totalT += 1
#printing results
resultfile = open('counts.txt', 'w')
resultfile.write(str(totalA) + ' As found \n')
resultfile.write(str(totalC) + ' Cs found \n')
resultfile.write(str(totalG) + ' Gs found \n')
resultfile.write(str(totalT) + ' Ts found \n')
{% endcodeblock %}

The only difference is at the end of the script. Here instead of `print` we use
`write`. Notice that `write` is a method of the opened file.(in our case
called `resultfile`. This method only accepts strings, so we need to
convert everything to string before writing in the file. Notice also
that we need to add a carriage return/newline at the end of the string
to be written. Differently of `print`, `write` does not automatically
puts a new line at the end of the output.
