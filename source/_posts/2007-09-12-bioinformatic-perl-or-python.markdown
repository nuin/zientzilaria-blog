---
date: '2007-09-12 21:16:02'
layout: post
slug: bioinformatic-perl-or-python
status: publish
title: '"bioinformatic perl or python"'
wordpress_id: '36'
categories:
- google searches
---

I decided to create a new series of posts (a category to be more precise) that deals with some searches that reach the blog. I use a pretty nice logging [application](http://haveamint.com) so it is easy to randomly select a Google search term to discuss about it.

About an hour ago someone in the interwebs searched for "bioinformatic perl or python" and my other [blog](http://python.genedrift.org) is the third returned by Google. How can answer this question without praising too much Python or not despising too much perl? 

My language of choice was always C/C++ even though it can explode in your face if not handled with care. I also tried Java (did not like it), Visual Basic, Pascal, Delphi and of course Perl, before arriving in Python. The are many differences between Python and Perl, and there aren't many differences between Python and Perl. Specially for bioinformatics development. 

Keep the score and please remind this comparison is for a bioinformatician perspective, or even a curious biologist that wants to learn programming.

In Python, OO (object orientation) is natural, while in Perl is an added layer. Is this important for a bioinformatician? It is relative, depends how much you know programming and what you want to do. OO is really nice even for some simple things, and if it is natural or hacked on the language, does not matter. 
Tie: Python 1, Perl  1

Python syntax is easy to understand, Perl's not so much. Python is naturally indented, Perl no. Cleaner syntax, easier to learn, more difficult to make simple mistakes (not 100% true, but let's assume so).
Advantage Python: Python 2, Perl 1

Perl has natural support for regular expressions, which are very handy in a lot of biological tasks. Python has the re module but the regex is not natural. And you bet you are going to use a lot of regex in bioinformatics.
Advantage Perl: Python 2, Perl 2

Speed: very similar. In most cases speed is not a problem in bioinformatics applications. Both are interpreted languages, not compiled to bytecode, so if you want speed go check C/C++.
Tie: Python 3, Perl 3

Python has an interpreter that can be used interactively. That's very handy when you are not sure if some technique will work and want to test before wasting hours implementing and failing. If you are learning to program or at least learning Python, that's very useful. Perl does not have it.
Advantage Python: Python 4, Perl 3

Support: Perl has CPAN, Python has Cheese Shop. But Perl has much more third-party modules than Python. On the other hand, Python community is growing. Basically anything you want to do in Perl, might have been already implemented, so there is no reinventing-the-wheel-ism. 
Advantage Perl: Python 4, Perl 4

Functional programming: according to Wikipedia, FP is a programming paradigm that treats computation as the evaluation of mathematical functions. Like OO, is something that you want to address at a higher level of programming knowledge. Perl has it, but Python's is better. period.
Advantage Python: Python 5, Perl 4

Portability: it is a tie. Both run everywhere and anywhere. 
Tie: Python 6, Perl 5

GUIs: Python has more possibilities in the GUI department, while Perl is a little behind. If you are a beginner, you probably won't be making any graphical interfaces, and for most of the stuff in Biology (if you are computer savvy) interfaces are not important. In the end, you type faster than you click.
Tie: Python 7, Perl 6

And finally, support of the biological community: Perl, hands down. BioPerl is stronger than BioPython, and more complete, so most of the stuff you want are already there. BioPython is growing (not really that much), but it will take some time to reach the BioPerl level. Perl will also let you talk with more people at conferences, so it is an ice breaker.
Advantage Perl: Python 7, Perl 7

Conclusion:

It is just a matter of taste. Both languages are well balanced and powerful. Depending on your needs one will be more suited than the other, but in the end both can give you the desired result. Python has a slight advantage of being easier to learn, with a more English-like syntax, while Perl has the slight advantage of a slightly bigger community. You will be happy with both, and in the end it would be fun to know both. There are many ways of doing things, either in Perl or Python.

And remember, this is a perspective of a biologist/bioinformatician.


