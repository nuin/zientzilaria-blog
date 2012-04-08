---
author: Paulo Nuin
date: '2007-10-26 12:15:47'
layout: post
slug: generating-multiple-sets-of-random-dna-sequences-with-one-script-and-a-bash-one
status: publish
title: Generating multiple sets of random DNA sequences with one script (and a bash
  example) [updated]
wordpress_id: '65'
? ''
: - off topic
  - Section 4
---

A commenter, Dilmurat, gave me an idea about the [script](http://python.genedrift.org/2007/04/04/a-script-to-simulate-dna-sequence-sets/)
that generates random DNA sequence sets. Apparently it wasn't clear that
the script was intended to generate only one sequence set, and not
multiple sets. Dilmurat also offered his solution: 

{% codeblock lang:python %}#!/usr/bin/env python 
import random 
import sys 
def simulate_sequence(length): 
	dna = ['A', 'C', 'G', 'T'] 
	sequence = '' 
	for i in range(length): 
		sequence += random.choice(dna) 
return sequence

setsize = int(sys.argv[1]) 
minlength = int(sys.argv[2]) 
maxlength = int(sys.argv[3]) 
rlength = [] 
sequenceset = [] 

for i in range(setsize):
	rlength.append(random.randint(minlength, maxlength)) 
for length in rlength: 
	sequenceset.append(simulate_sequence(length)) 
		
for sequence in sequenceset: 
	print sequence{% endcodeblock %} 

I don't know if the lack of
formatting in the comments might have generated a different result to
me, but let's see how we can generate multiple sets of random DNA
sequence. Getting back to section 4, we can start with the original
script that creates only one set 

{% codeblock lang:python %}#!/usr/bin/env python 
import random 
import sys 

def simulate_sequence(length): 
	dna = ['A', 'C', 'G', 'T'] 
	sequence = '' 
	for i in range(length): 
		sequence += random.choice(dna) 
	return sequence

setsize = int(sys.argv[1]) 
minlength = int(sys.argv[2]) 
maxlength = int(sys.argv[3]) 
sequenceset = [] 

for i in range(setsize): 
	rlength = random.randint(minlength, maxlength)
	sequenceset.append(simulate_sequence(rlength)) 
	
for sequence in sequenceset: 
	print sequence{% endcodeblock %} 

There is a very easy way of
changing this code to make it output a definite number of sets. WE add a
new input parameter and also a loop to it, and that should take care of
everything. 

{% codeblock lang:python %}#!/usr/bin/env python 
import random 
import sys 

def simulate_sequence(length): 
	dna = ['A', 'C', 'G', 'T'] 
	sequence = '' 
	for i in range(length): 
		sequence += random.choice(dna) 
	return sequence 
	
setsize = int(sys.argv[1]) 
minlength = int(sys.argv[2]) 
maxlength = int(sys.argv[3]) 
nsets = int(sys.argv[4])
for i in range(nsets): 
	sequenceset = [] 
	for i in range(setsize): 
	rlength = random.randint(minlength, maxlength)
	sequenceset.append(simulate_sequence(rlength)) 
	
	for sequence in sequenceset: 
		print sequence print{% endcodeblock %} 

A test with 10 as the
number of sequences, 20 as minimum and 30 as maximum length and 2 sets
output something like this 


`GAGGACGACGTGTCGGATTAGAT GCAGATAAACGGGTAAGATGA
ATTAGGAAGGGTCTAAGAGATCCCGGTAA ATCAGCCTCCGCACGCCTCGTGTA
AGTTTAGCTAGCCGTAGTACTTTC TTTGAAGCTCGGGGCTAAACTCCGACCAC
GACAGGGTAAGGTGACCTTCTCAG TGGTTGACTCTGTTCTCTGGT
CGCAATACGTCGTGGTGCCGCTCCACT TCCTGCAGGGAGGCAGCAGC
TTCGGAGGTATTGAGTACTGTTGCATCG CCCTTATAATACCTAGTGTAACATTC
TAGTCATGTCATATAACCTGTGTCG AGCGCGAACCCTCCAGTTTTTTT
AGGGCGTGTAAGCGACGTTGAACAAG CCATGCGTCTTTTTGGCGATCCGT
ACTCAGATCGGCTAGTATCCTTCGCACG CTATCGTCGTTCCCAGCAACGGCAGCAGA
CGTGCGATGGGGCGAGATTTTT ACGCTTTGGCTAGTGGGGAGTTTCGCCACT`


what is basically
what we need. Quick 'n' easy. Of course a [top notch bioinformatician](eridanus.net/blog/) that uses Linux 100% of the time
would be able to create a simple bash script and use the initial script
to generate multiple random sets. bash is not a primary scope of the
blog, but let's see how to do that. Saying the our initial script was
saved as `randomset.py` we would have a very short script in bash to
generate multiple sets. We want to generate 10 sets of sequences of
length between 20 and 30 nucleotides, and each set would need to have 10
different sequences (remember that our initial script only accepts 3
parameters). 

**Off topic**

`for ((i=0;i<10;i++)) 
  do     
  min=20     
  max=30     
  nseqs=10
  python randomset.py $nseqs $min $max     
echo  done`


That should do the trick. You can even type it from the command line.
The `for` syntax in bash is very similar to C/C++ but it does not accept
spaces, as all the variable assignments. When you assigning a variable
value in bash you omit the dollar sign and when you are reading the
variable value you access it with the dollar sign, like in the line that
runs the script. A `for` loop in bash starts with a `do` command and
ends in a `done` command, not brackets or parenthesis involved. The
`echo` at the end helps adding a separating blank line after each random
set. **off topic** 

Of course we could use "makenucseq from the EMBOSS
package", we can even use [Dawg](http://http://scit.us/projects/dawg)
from my friend Reed Cartwright, which I believe has a shorter learning
curve (and faster compilation) than EMBOSS, but that will be away from
the scope of this blog, which is to show how to use **Python** in
**simple** bioinformatics scripts. I allowed myself to post off topic
subjects (including this last paragraph) because a (very) small
percentage of the commenter(s) seems to misunderstand the real focus of
this tutorial. We don't need fancy words or complex topics to show how
simple things can achieve good results in almost no time. My focus is
not give the reader the fish and chips ready to eat. My focus is to show
how to fish and peel, cut and fry the potato in order to cook the dish.
This way, next time he or she might be cooking better things to eat.
