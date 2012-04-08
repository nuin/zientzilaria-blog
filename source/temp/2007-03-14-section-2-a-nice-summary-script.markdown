---
author: admin
date: '2007-03-14 15:32:24'
layout: post
slug: section-2-a-nice-summary-script
status: publish
title: 'Section 2: a nice summary script'
wordpress_id: '27'
? ''
: - Section 2
---

Closing section two, let's use everything we saw before and write a nice
script that will read a sequence file (DNA) and report us of any
"errors" and the number of different nucleotides. It is very simple, but
a good exercise. Depending on your needs you can easily modify it to
check for other characteristics of sequences, even change it to read
amino acids sequences. We start with the code, comments coming after it.
[sourcecode language='python']\#!/usr/bin/env python import sys import
re fileentered = True while fileentered == True: filename =
raw\_input('Please enter a file to check: ') if len(filename) \>= 1:
try: seqlist = open(filename, 'r').readlines() sequence =
''.join(seqlist) sequence = sequence.replace('\\n', '') totalA =
sequence.count('A') totalC = sequence.count('C') totalG =
sequence.count('G') totalT = sequence.count('T') otherletter =
re.compile('[BDEFHIJKLMNOPQRSUVXZ]') extra = re.findall(otherletter,
sequence) output = open(filename+'.count', 'w') output.write('Count
report for file ' + filename + '\\n') output.write('A = ' + str(totalA)
+ '\\n') output.write('C = ' + str(totalC) + '\\n') output.write('G = '
+ str(totalG) + '\\n') output.write('T = ' + str(totalT) + '\\n') if
len(extra) \> 0: output.write('Also were found ' + str(len(extra)) + '
errors\\n') for i in extra: output.write(i + ' ') else: output.write('No
error found') output.close() print 'Result file saved on ' + filename +
'.count' except: print 'File not found. Please try again.' else:
sys.exit()[/sourcecode] The main change here is that we use a `while`
loop to control de program flow. Notice that we import `sys` and `re`.
Basically we ask for an user input, the filename, and depending on the
input given we process the file or exit the program. The early exit is
done with the `sys.exit` method which is a shortcut to get out of the
script processing. Very handy. If the input is valid we `try` to open
it. If the operation is successful, great, we read the file, count the
nucleotides and use a quite scary regular expression to search all the
"errors" in our sequence. The regex is compiled with the pattern
`'[BDEFHIJKLMNOPQRSUVXZ]'` which means "match any character in this
range". Take a closer look at the pattern and you will see that is every
letter in the alphabet, except for ACGT. And when searching for these
"errors" instead of using `re.search` we use `re.findall`, which
conveniently returns a list with all the substrings found. That's even
more handy. On the final part of the script we take care of the output,
opening a file called `.count` where we print the counts and the errors,
if they actually exist. One thing I left from the previous post, is that
we need to close the file opened to write. In some cases if the file is
not properly closed, errors might occur. So always remember to close the
files used for writing/appending, using `.close()`.
