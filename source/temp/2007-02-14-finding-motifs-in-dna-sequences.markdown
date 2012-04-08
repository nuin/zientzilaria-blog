---
author: admin
date: '2007-02-14 14:26:26'
layout: post
slug: finding-motifs-in-dna-sequences
status: publish
title: Finding motifs in DNA sequences
wordpress_id: '16'
? ''
: - Section 2
---

As you might have noticed, BPB generally uses protein sequences. I am a
"DNA guy", and basically in our simple examples either type of sequence
(except the example on transcribing) could have been used. I will stick
with this molecule for a while, or until I can. We are going to use our
good old AY162388.seq file, still assigning the file name inside the
script there will be a twist in the end. Also, remember the Regular
Expression module? We are going to use it too. I am going to do just as
the book: I will paste the code below with comments in the middle and
explain it afterwards. [sourcecode language='python']\#!/usr/bin/env
python \#finding motifs in DNA sequences \# we use the RegEx module
import re \#still keep the file fixed dnafile = "AY162388.seq" \#opening
the file, reading the sequence and storing in a list seqlist =
open(dnafile, 'r').readlines() \#let's join the the lines in a temporary
string temp = ''.join(seqlist) \#assigning our sequence, with no
carriage returns to our \#final variable/object sequence =
temp.replace('\\n', '') \#we start to deal with user input \#first we
use a boolean variable to check for valid input inputfromuser = True
\#while loop: while there is an motif larger than 0 \#the loop continues
while inputfromuser: \#raw\_input received the user input as string
inmotif = raw\_input('Enter motif to search: ') \#now we check for the
size of the input if len(inmotif) \>= 1: \#we compile a regex with the
input given motif = re.compile('%s' % inmotif) \#looking to see if the
entered motif is in the sequence if re.search(motif, sequence): print
'Yep, I found it' else: print 'Sorry, try another one' else: print
'Done, thanks for using motif\_search' inputfromuser =
False[/sourcecode] Now let's dissect the code, in a biological way. We
already seen everything up to the part the list's lines are joined.
First new lines for us is this [sourcecode language='python']sequence =
temp.replace('\\n', '')[/sourcecode] Most of the methods in Python have
very intuitive names (ok, most languages do), so it is easy to deduce
that `replace` actually replaces something. And why do we need to use
this method? First, we joined the lines in one temporary string (yep,
strings are immutable), but the lines come with everything, including
carriage returns that we need to get rid of. So our "final" string
`sequence` receives the value in `temp` and we apply the method
`replace` to modify it. `replace` has two arguments, the first is the
string we want to change from, while the second is the string we want to
replace with (in fact `replace` accepts three arguments, the last being
the number of times we want to do the change). In our case, we are
telling the interpreter to get every substring `'\n'` and put an empty
one in their places. The next line is a simple value assignment:
[sourcecode language='python']inputfromuser = True[/sourcecode] and the
variable will manage the `while` that checks input from the user.
Basically we will run the loop until a certain type of input is given,
that will make the variable value become `False`. That's why we have the
line [sourcecode language='python']while inputfromuser[/sourcecode] with
no check. Yep, notice that we don't need to check for the variable's
value, Python assumes that it is True. To understand better, imagine
that `inputfromuser` is a flag that appears when True and disappears
when False. Python can only "see" it when it appears, and when it does
disappear it needs to check for it. We will elaborate more later.
Another different line awaits us [sourcecode language='python']inmotif =
raw\_input('Enter motif to search: ')[/sourcecode] `raw_input` is a
function that takes a line input by the user and returns a string. In
our case, we assign the value returned by the function to a new string
called `inmotif`. Also, `raw_input` has one *prompt* argument which is
written to the screen with no trailing line, waiting for the user to
input something. This takes us to the `while` loop [sourcecode
language='python']if len(inmotif) \>= 1: \#we compile a regex with the
input given motif = re.compile(r'%s' % inmotif) \#looking to see if the
entered motif is in the sequence if re.search(motif, sequence): print
'Yep, I found it' else: print 'Sorry, try another one' else: print
'Done, thanks for using motif\_search' inputfromuser =
False[/sourcecode] After getting the input from the user, we need to
check the size of such input: if it is greater or equal to one, we will
search it in our sequence, otherwise we will finish the loop. So if we
get a valid input (valid in the sense of size, for now) we will compile
the regex and search for it. There is a difference in regex compilation.
In the DNA transcribing we assigned a string to the regex directly, now
we have a string coming from a variable/object [sourcecode
language='python']motif = re.compile(r'%s' % inmotif)[/sourcecode]
Notice the difference in the argument that is passed to the `compile`
function. In this case the regex to be compiled is coming from the
string entered by the user, and we have to pass it by using Python's
string formatting operator, noted as a `%`. This formatting operator
uses two parameters: a string with formatting characters and the data to
be formatted, separated by the percent sign. In our case the formatting
character will receive a string, hence the `%s` (s for string), and the
data to be formatted that is the input. Previously, we used the regex
function to replace characters/substrings in a sequence. This time, we
are interested to know if the motif entered by the user is in our
sequence. So we use the search method instead [sourcecode
language='python']if re.search(motif, sequence):[/sourcecode] Notice
that we do the search in at the same time we are testing for its result.
The same case as the checking we do at the while loop. If there is a
positive result from the regex search a True flag will be raised and the
interpreter will execute the code of the initial branch, not testing for
the `elif` and `else` [sourcecode language='python']print 'Yep, I found
it' else: print 'Sorry, try another one'[/sourcecode] This condition is
nested inside another condition, the one that tests for the size of the
input entered. So, if our search returns a regex object, we print
`Yep, I found it`, otherwise the user will receive
`Sorry, try another one`. Now back to our upper `if`, if the user input
length is equal to zero (just pressing the Enter key) the interpreter
will process the line [sourcecode language='python']print 'Done, thanks
for using motif\_search'[/sourcecode] and then [sourcecode
language='python']inputfromuser = False[/sourcecode] that will tell the
while loop that there is no True variable anymore, ending the loop and
consequently our script. Let's review the script and its flow:
[sourcecode language='python']1) assign a filename to be opened 2) read
the file 3) join the lines 4) remove carriage returns 5) ask for user
input, while is valid 6) if input length is greater or equal to 1,
process it 6a) compile regex with input 6b) search for it 6b1) if it is
found print yes 6b2) if it is not found print no 7) if input length is
equal to zero, end while loop, end string[/sourcecode] I know it is a
lot of information, take your time. The code can be downloaded from the
[repository](http://python.genedrift.org/repository/). Next I will
change a bit this script using other methods to find the motifs, and
making the promised twist in the method that reads the file.
