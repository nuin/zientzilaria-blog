---
author: admin
date: '2007-02-20 14:30:10'
layout: post
slug: finding-motifs-in-dna-sequences-twist
status: publish
title: 'Finding motifs in DNA sequences: twist'
wordpress_id: '17'
? ''
: - Section 2
---

As promised, let's change a bit our previous code, and make it more
effective. If you are reading this tutorial in one-entry mode, let's
check the code 


{% codeblock lang:python %}
#!/usr/bin/env python
import re
dnafile = "AY162388.seq"
seqlist = open(dnafile, 'r').readlines()
temp = ''.join(seqlist)
sequence = temp.replace('\n', '')
inputfromuser = True
while inputfromuser:
    inmotif = raw_input('Enter motif to search: ')
    if len(inmotif) >= 1:
        motif = re.compile('%s' % inmotif)
        if re.search(motif, sequence):
            print 'Yep, I found it'
        else:
            print 'Sorry, try another one'
    else:
        print 'Done, thanks for using motif_search'
        inputfromuser = False
{% endcodeblock %}

In order to
make it more effective, let's allow the input of any file, maybe asking
for the file as soon as the script is started. To accomplish that we
need to "protect" the script and make it error proof (almost at least).
Yes, you thought it right: we need to check if the input file exists
before opening it. We can use `try ... except` statements to do that.
Pretty handy. This is called an exception handler, so basically we try
the validity of some command/method and depending on the result we
continue our program flow or we catch the exception and do something
else. Under `try` we put the expression to evaluate, and under `excepts`
what to do in case of failure. Like this 


{% codeblock lang:python %}
try:
    opening a file 
except: 
    as the file does not exist, print something{% endcodeblock %} 

So, let's put in our code above. We
remove this 

{% codeblock lang:python %}dnafile = "AY162388.seq"
seqlist = open(dnafile, 'r').readlines(){% endcodeblock %}

and include these lines 

{% codeblock lang:python %}fileinput = True
fileinput = True
while fileinput == True:
    filename = raw_input('Enter file name:')
    if len(filename) > 0:
        try:
            dnafile = open(filename, 'r')
            fileinput = False
        except:
            print 'File does not exist, please try again'
    else:
        sys.exit()
{% endcodeblock %}

I know, a lot of new code. But if you take a closer look, there is only three
lines we have never seen: `try except` and the last line with
`sys.exit()`. Here, the script tries to open the file provided as input,
if it does find the file normal operation resumes, if does not, the
script asks for another input. As in the other while loop, we control it
with a boolean variable, and in the case of empty input we end the loop
and the script, using a system command `exit`, in the last line of the
new code. Our script is better now, not bulletproof, but a little bit
more efficient. There still a "flaw", that you can only check one file
for each run of the script. At least we not stuck to our usual DNA
sequence.