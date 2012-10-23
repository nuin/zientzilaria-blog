---
author: admin
date: '2007-03-30 15:19:30'
layout: post
slug: ramdomization
status: publish
title: Ramdomization
wordpress_id: '31'
? ''
: - Section 4
---

We start section 4 with a very short introduction to randomization.
Chapter 7 of BPB discuss the use of randomization to obtain mutations in
DNA and protein sequences. The example given in the book is at the same
time simple and interesting, as it creates a paragraph from random
selections of nouns, adjectives, verbs and other grammar elements. Here
we are going to to create a very (stress on very) simple dice game,
where each time you run the script it will throw two dices for you and
two dices for the computer. It then prints the sum of the dices and
tells who won the match. Randomization is an important feature of
computer languages. There are different researchers involved in the
creation of the best approaches to generate random number in computers.
Random number are important in the simulation of different natural
processes, such as genetic mutation, gene drift, epidemiology, weather
forecast, etc. The better the generator, the better the simulation.
Python has a random module included, with a myriad of functions that can
perform different randomizations. In this post we will see the `integer`
randomization, and in later entries we will see some other powerful
functions. Our script is quite simple, and the only new aspect for us
here is the random module and the `randint` function. 


{% codeblock lang:python %}#!/usr/bin/env python 
import random 

dice1 = random.randint(1,6) 
dice2 = random.randint(1,6) 
computerdice1 = random.randint(1,6) 
computerdice2 = random.randint(1,6) 
mine = dice1 + dice2 

his = computerdice1 + computerdice2 

print 'mine = ' + str(mine) + ' vs. computer = ' + str(his) 

if mine > his: 
    print "I won"
elif mine < his: 
    print "Computer won" 
else: 
    print "Tie. Try again"
{% endcodeblock %}

`random.randint` is a function that generates an integer random number
between a range specified by the number between parentheses. In the
above case, we are using a dice of 6 values. So, for every call of
`random.randint(1,6)` a random number between 1 and 6 will be generated.
We store this number in a variable, sum the user's dices and the
computer's and check with a `if` clause to see the winner. A good
exercise would be to make this script interactive, allowing multiple
matches. Next we will see another random module function and then we
will generate mutations on DNA sequences.
