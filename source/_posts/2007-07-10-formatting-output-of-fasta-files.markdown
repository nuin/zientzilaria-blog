---
author: admin
date: '2007-07-10 11:30:15'
layout: post
slug: formatting-output-of-fasta-files
status: publish
title: Formatting output of FASTA files
wordpress_id: '43'
? ''
: - Section 5
---

The Beginning Perl for Bioinformatics book shows a script to print
formatted sequence data, specifying that no more than 80 characters
(either nucleotides or amino acids) should be printed across a page.
Here, we will see a similar script in Python and will include it in our
`fasta.py` module in order to use it a default output, taking advantage
of its usability. Basically, our FASTA reader strips all the carriage
returns/new lines (if existent) from the input file, so the sequence
itself is stored continuously in a string. Of course we could do it
differently and store the sequence as is in the file, but then they
might differ on the number of characters per line and other features.
Our goal then is to *break* the sequence in chunks, making it look like
a justified paragraph. We use the code below to obtain this, back after
it. 

{% codeblock lang:python %}#!/usr/bin/env python 
import fasta
import sys 

sequences = fasta.read_fasta(open(sys.argv[1], 'r').readlines())
temp = [] 

for i in sequences: 
    print i.name 
    for j in range(0,len(i.sequence),80): 
        temp.append(i.sequence[j:j+80]) 
        print '\n'.join(temp) 
        temp = []{% endcodeblock %} 

The script, as always, is very
simple and does the job. A new feature of the range method is
introduced: the *step*. From previous posts we have seen that function
range generates a sequence of integers based either on one value
{% codeblock lang:python %}>>>range(5) 
>>>[0, 1, 2, 3, 4]{% endcodeblock %} 

or two values

{% codeblock lang:python %}>>>range(10,15) 
>>>[10, 11, 12, 13, 14]{% endcodeblock %} 

The *step* parameter makes the generated to jump a
certain number of values. 

{% codeblock lang:python %}>>>range(10, 20, 2) 
>>>[10, 12, 14, 16, 18]{% endcodeblock %} 

This is similar to the
`for` loop in C/C++ where the loop is define by three parameters on a
construction like this 

{% codeblock lang:c %}for (i = 0; i < 10; i++){% endcodeblock %} 

where the first parameter sets the initial value of
`i`, the second value sets the maximum value of `i` and the last one
sets the *step* that `i` will be incremented. In our small script above,
we read the sequence (this time putting everything in one line), get the
sequences and then iterate along the instances of our class, printing
first the name of the sequence. Then we iterate on the whole length of
each sequence, this time generating a range that starts on zero and goes
up to the final nucleotide/amino acid and has a *step* that defines the
number of characters we want to print in one line. To print the sequence
to the screen we had two options: directly print using 

{% codeblock lang:python %}print i.sequence[j:j+80]{% endcodeblock %} 

or use the
longer route shown in our script. Trying this script will output the
sequences from the original file with 80 characters along the line. Next
following the book we will write a script to translate DNA to protein
using our FASTA reading function and modify our FASTA module to include
the formatted output function.