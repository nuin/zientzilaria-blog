---
date: '2007-09-16 14:16:50'
layout: post
slug: apart-from-python-and-perl-in-bioinformatics
status: publish
title: Apart from Python and Perl in Bioinformatics
wordpress_id: '38'
categories:
- Bioinformatics - opinion
- Science
---

Last post received a lot of comments, mainly because I did not mention other languages on it. The reason of the post was to show that Perl and Python are equivalent, just a matter of taste and personal preferences, and maybe of how comfortable one is with a programming language. 

Also a _mea culpa_ of missing Perl's interactive shell. That would give Perl a slight advantage over Python, but in the end it really doesn't matter.

**The case for Java**

A lot of people mentioned Java as a must for Bioinformatics, and I agree with them. But again it wasn't in the scope of what I intended to write. Even though I don't like Java (personal taste) I don't deny its importance in the field, its robustness, its easy cross-platform development and power. Several large scale Java bioinformatics applications are available, showing all its features and beauty. Two good examples are Geneious and CLC Workbench, that are the closest you can get to project and database management in molecular biology. 

I see Java dominating its niche in Bioinformatics, of the large scale, cross-platform GUI application development. At the same time Python and Perl "compete" for their niche of the small to medium applications to quickly deal with some data (sometimes large amounts), most of the time also cross-platform and sometimes only used _in house_. Ruby might be soon joining both for an extra competition. Just to be clear, I am not saying that either Perl or Python (you might include Ruby) are not engineered to large scale application development, or is not possible to use Java as an agile script language.

**Other languages**

I consider myself a generalist. I have tried many different languages and do not shy away of trying new ones now and then. In science the larger the diversity, the better, especially in bioinformatics. I would state the obvious by writing that each language is tailored to do different things, and it is also relevant in bioinformatics. 

But as in any software development environment, you have to attach yourself to some rules. If you are a tenured professor with your own research program you might be able to use a more obscure language and impose on your lab such language. 

On the other hand if you are a student or post-doc in a lab, you may not have that much liberty to use your language of choice. Sometimes, you will be working on someone else's code, maybe going to upgrade an already released application. And in some cases, your boss don't know that particular language and have no interest in learning it and have no interest in reviewing a code in a language she or he doesn't understand. It is an identical situation for a developer or consultant starting a gig in a softhouse. You can bring your knowledge, but maybe you **must** code in C# even though you might not like it.

It also depends on the final use of the program. If it is going to be used in house just to generate results for a publication, you might have more liberty on what your decisions. But if if the application will be widely released, via publication or announcement, you probably need to follow the same rules of development and deployment as any commercial package.

And what do I consider obscure in bioinformatics? Maybe F#, OCaml, Haskell just to limit to the ones mentioned in the comments. I have F# and Haskell installed, but never toyed with them to be able to give a verdict. Never tried OCaml, but heard good things about it. R is a great environment, even though you might not do actual code in it and just use the functions and libraries available. I am starting with Ruby and giving a shot at Rails and will see how it goes. 

There is space for most languages in Bioinformatics. It depends on your personal taste, the scope of your application and the environment where you working in. Just like any software development project.

