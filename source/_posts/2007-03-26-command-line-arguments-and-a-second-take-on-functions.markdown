---
author: admin
date: '2007-03-26 13:18:48'
layout: post
slug: command-line-arguments-and-a-second-take-on-functions
status: publish
title: Command line arguments and a second take on functions
wordpress_id: '29'
? ''
: - Section 3
---

We have seen, briefly, how to define and use a function in Python. Now
we are going to jump forward a bit and create a new function and at the
same time take a look on command line parameters that can be passed to
the script. If you have used command line applications before, you might
have encountered programs that asks for a file name, a calculation
parameter, etc to be passed in the command line. Python scripts are no
different, they accept such parameters. For this we have the `sys`
module that has system specific parameters and functions. We have used
before the `sys.exit`, imported as an extra module function. 

Every operating system (even Windows) has arguments in its command line, and
programming languages usually call such arguments `argv` (in the C/C++
you have argv in the parameters of the main function). Lists in Python
start at 0 (zero), and for the argument list the first item is the
script/program name. Basically if we have this



{% codeblock lang:bash%}$> python myscript.py DNA.txt{% endcodeblock %}


`myscript.py` is the argument 0 in the
list and `DNA.txt` is the argument 1. So whenever we create a script that
receives arguments in the command line, we have to start (in most cases,
be aware) from 1. 


In Python using system arguments in the CLI will look
like 


{% codeblock lang:python %}import sys
filename = sys.argv[1]
valueone = sys.argv[2] ...{% endcodeblock %} 

We will a variation of our
previous script that counts the bases, now with command line arguments
and a function (with no "error" checking at first) 


{% codeblock lang:python %}
#!/usr/bin/env python import sys 

def count_nucleotide_types(seq): 
    result = []
    totalA = seq.count('A')
    totalC = seq.count('C')
    totalG = seq.count('G')
    totalT = seq.count('T')
    result.append(totalA)
    result.append(totalC)
    result.append(totalG)
    result.append(totalT) 
    return result 

sequencefile = open(sys.argv[1],'r').readlines() 
sequence = ''.join(sequencefile)
sequence = sequence.replace('\n', '')
values = count_nucleotide_types(sequence)

print "Found " + str(result[0] + "As" 
print "Found " + str(result[0] + "Cs"
print "Found " + str(result[0] + "Gs" 
print "Found " + str(result[0] + "Ts"{% endcodeblock %} 

Few new things here. We created a function `count_nucleotide_types` that should receive a string
containing the sequence. The "real" first line of the program flow is
the one that gets the name of the file from the command line argument,
open and read it. We then convert the list to a string, modify it a but
and throw it to the function. Get the result back, and done. With
functions we actually don't save coding time/length (at least here), we
make out code more organized, easier to read and somewhat easier to
someone else read and understand it. It is not a good coding practice to
have long programs/scripts with no functions, no subdivision, no
structure. Functions are sometimes good program nuggets that can be
reused in the same application or even ported/copied to other
applications and reused indefinitely. Soon we will see a function and
class that reads a FASTA file in Python that can be used anywhere in any
program that needs such feature. Try the code and come back later for more.
