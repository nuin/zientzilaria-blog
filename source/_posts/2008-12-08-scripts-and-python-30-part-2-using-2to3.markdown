---
author: admin
date: '2008-12-08 14:55:56'
layout: post
slug: scripts-and-python-30-part-2-using-2to3
status: publish
title: Scripts and Python 3.0, part 2, using 2to3
wordpress_id: '209'
? ''
: - Python 3.0
---

And we're back to check our initial scripts to run on Python 3.0. Along
with this latest release, a nice tool to parse your scripts is also
installed. It's called
[2to3](http://docs.python.org/dev/3.0/library/2to3.html) and it's
available in the `Tools/scripts` of your Python 3.o installation
directory. Basic usage is very similar to any python script: [sourcecode
language='bash']2to3 end. This will tell Python what we want the end of
the line, in our case an empty string. So the line would be [sourcecode
language='python']print(line, end = '')[/sourcecode] That's it. So
code\_03 and code\_04 will be [sourcecode language='python']\#code\_03
import re \#setting the DNA string myDNA = 'ACGTTGCAACGTTGCAACGTTGCA'
\#assigning a new regex and compiling it \#to find all Ts regexp =
re.compile('T') \#create a new string tha will receive \#the regex
result with Us replacing Ts myRNA = regexp.sub('U', myDNA) print(myRNA)
\#end 03 \#code 04 \#assigning a filename to a variable dnafile =
"AY162388.seq" \#opening the file file = open(dnafile, 'r') \#printing
each line of the file for line in file: print(line, end="")[/sourcecode]
Now, code\_05, has 45 lines including comments, so it should be a good
idea to test 2to3 on it, especially after a long time since we created
the script. There might be some other changes that we might miss (I
already . Let's run 2to3 on our original script and check the output:
`RefactoringTool: Skipping implicit fixer: buffer RefactoringTool: Skipping implicit fixer: idioms RefactoringTool: Skipping implicit fixer: set_literal RefactoringTool: Skipping implicit fixer: ws_comma --- code_05.py (original) +++ code_05.py (refactored) @@ -30,16 +30,16 @@  #the loop continues  while inputfromuser:      #raw_input received the user input as string -    inmotif = raw_input('Enter motif to search: ') +    inmotif = input('Enter motif to search: ')      #now we check for the size of the input      if len(inmotif) >= 1:          #we compile a regex with the input given          motif = re.compile('%s' % inmotif)          #looking to see if the entered motif is in the sequence          if re.search(motif, sequence): -            print 'Yep, I found it' +            print('Yep, I found it')          else: -            print 'Sorry, try another one' +            print('Sorry, try another one')      else: -        print 'Done, thanks for using motif_search' +        print('Done, thanks for using motif_search')          inputfromuser = False RefactoringTool: Files that need to be modified: RefactoringTool: code_05.py`
So a lot of lines, seems that we need to do a lot of changes. But in
fact there are not many changes. All lines starting with a - need to be
removed and replaced by the lines starting with a +, and the + lines are
adjacent to the ones we need to change. Again, the most common changes
here are the print statements, but there is also another change to be
done [sourcecode language='python']inmotif = raw\_input('Enter motif to
search: ') inmotif = input('Enter motif to search: ')[/sourcecode] So,
there is no `raw_input` in Python 3.0, it was abolished for a more
evolved `input` function that now always expect a string, that can be
evaluated later if needed (and desired), just like the old `raw_input`.
Now there is no confusion anymore on which one to use. Digging a little
bit into 2to3 we see that it can write the code for use by using the
`-w` parameter when running the script. Be careful as it rewrites the
same file, however saving a backup copy. In the end we get this code
from 2to3 (code\_05.py) [sourcecode language='python']\#!/usr/bin/env
python ''' simple script to find motifs on DNA sequences using regex the
script is interactive ''' \# we use the RegEx module import re import
string \#still keep the file fixed dnafile = "AY162388.seq" \#opening
the file, reading the sequence and storing in a list seqlist =
open(dnafile, 'r').readlines() \#let's join the the lines in a temporary
string temp = ''.join(seqlist) \#assigning our sequence, with no
carriage returns to our \#final variable/object sequence =
temp.replace('\\n', '') \#we start to deal with user input \#first we
use a boolean variable to check for valid input inputfromuser = True
\#while loop: while there is an motif larger than 0 \#the loop continues
while inputfromuser: \#raw\_input received the user input as string
inmotif = input('Enter motif to search: ') \#now we check for the size
of the input if len(inmotif) \>= 1: \#we compile a regex with the input
given motif = re.compile('%s' % inmotif) \#looking to see if the entered
motif is in the sequence if re.search(motif, sequence): print('Yep, I
found it') else: print('Sorry, try another one') else: print('Done,
thanks for using motif\_search') inputfromuser = False[/sourcecode] 2to3
seems to be pretty good in detecting changes, pointing them to you and
even writing the newer script for you. Until now I haven't tested on big
scripts (more than 100 lines long), but I plan to do it soon. For small
scripts we saw that it works quite well. A good test for 2to3 would be
when we get to the motifs scripts that are a little bit more complex,
even though they are quite short. Stay tuned and check new code on the
repository.
