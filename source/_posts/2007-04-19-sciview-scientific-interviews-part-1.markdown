---
date: '2007-04-19 15:26:33'
layout: post
slug: sciview-scientific-interviews-part-1
status: publish
title: 'SciView: scientific interviews, part 1'
wordpress_id: '18'
categories:
- Science
- SciView
---

Trying to generate content that would appeal to a wider range of scientists, I decided to do some email interviews with prominent scientists, in order to get their opinions on different aspects of science and research. The first interview was done with [Joe Felsenstein](http://evolution.genetics.washington.edu/phylip/felsenstein.html) , from the University of Washington. I would like to thank him for taking the time to answer my (sometimes) dull questions.
  
  
  

----------------------------------------------------------------------------------

_How do you see the "publish or perish" in science, with the increasing number of retracted papers, fake results, rushed publications and sometimes publication of extremely similar results in different papers and journals?_

JF: As you imply, "publish or perish" is a Bad Thing, which leads to all these negative results.  We should all be given a lifetime stipend with freely available grant funds, in hopes that before retirement we will produce at least one passable paper.    ;-) 

_Phylip is a great piece of software, in most cases better than PAUP and other similar applications. Can this be linked to the fact that it is open source and freely available? Have this helped to keep the software updated and portable to any system?_

JF: You will find that opinions vary greatly as to which is better, PHYLIP or PAUP*.  More people find PAUP* better than find PHYLIP better.  So your premise may be wrong, which leaves us without a need to find the reason. The availability of the source code allows people to suggest changes that increase robustness and portability.  But another reason is simply that I tend to write (and urge my programmers to write) in a "paranoid" style of C which deliberately avoids local features of one operating system or features of C that are sometimes not implemented correctly.  One correction: PHYLIP is ***not*** Open Source.  It is copyrighted to the University of Washington, and resale of it is potentially subject to a license fee.

Actually PHYLIP is not the result of a large community of users.  Mostly it's me and my student programmers, with some important pieces added by others. So it is not an example of the strength of the Open Source or GNU approach.


_Recently, I have focused on improving my interface design skills, trying to make the bioinformatics software-user interaction more friendly. Do you think that due to the fact that Phylip does not have a graphical interface was an obstacle to make it more widespread?_

JF: People often ask me why it doesn't have a GUI.  They also frequently request the opposite: a command-line interface with all options invoked from the command line. The problem is not having some GUI, it is having a good, intuitive GUI. That is a matter of design (Intelligent Design, I guess).  I once assigned a very good programmer to make a demonstration GUI for one of my programs, mimicking the menu that we already had (and actually then doing nothing, just showing what it would look like).  The result was so totally boring that it alerted me that the issue was not a GUI but what kind of GUI.

_How do you see that some bioinformatics companies create proprietary packages that are mere wrappers of open source academic software? And what about academic software that is sold? Most of them are funded by public agencies and tax money._

JF: In the USA in the 1970s the standard assumption was that publicly funded research should not be exploited commercially without a royalty coming back to the funding agency and the researcher.  Under the Reagan administration in the 1980s the view changed to being that the duty of the government was to subsidize the private sector by having their results used without compensation. The very same administrators who, in the 1970s, checked to see that you had not secretly privatized the products of research were now assigned to make sure that these results did get used privately (without compensation).  So it is hard to say what the legal status of research products such as software is. (There is an older tradition that books written by faculty members at universities can result in royalties to the author, without the university getting any payment).

One problem with Open Source (and with GNU licenses) is that they permit and encourage commercial exploitation without compensating anyone.  They love this but I would rather see some of the money made getting back to the original software authors.  That is one reason we aren't licensed under Open Source or under any of the GNU licenses.  I also have questions about whether these licenses permit the original author to say yea or nay to a proposed added feature -- I would prefer to maintain that degree of control.

_Your seminal work in 1981, introduced the maximum likelihood method for the calculation of phylogenetic trees. I do believe that a scientist's work has to be evaluated in its entirety, but that Journal of Molecular Evolution publication has influenced thousands of researchers for almost 26 years. Would you consider it your most important publication?_

JF:  The maximum likelihood method for phylogenies was introduced by Edwards and Cavalli-Sforza in 1964, and for molecular sequences it was first done by the great statistician Jerzy Neyman in 1971.  My 1981 paper did cite Neyman (it didn't credit Edwards and Cavalli-Sforza but at least I have cited their pioneering work on this many times before and since).  What I did that was new was to make it practical to do multi-species cases by introducing the pruning algorithm.  I also promoted and explained ML for years.  In the 1980s I gave many talks at universities.  I usually had to explain what likelihood was because the statistics courses that biologists took didn't bother to teach them this.  I also wrote a number of review articles and made programs available to do ML. Of my papers, the 1981 ML paper is the third most cited so far (after the 1985 bootstrap paper, a paper in 1989 in Cladistics describing PHYLIP, and just ahead of my 1985 paper on phylogenetic comparative methods).  Basically they are all part of the process of promoting a statistical modelling approach to phylogenies, so it is hard to label one as more important.  Possibly my most important paper in the long run will be my 1978 paper on a model of macroevolution, which has had no citations in the past 22 years.

_Sometime ago I attended a Hennig Society meeting, mainly because it was organized by the same institute where I was doing my PhD and because I was curious to meet the researchers behind some of the papers I was reading at the time. Later when I was doing part of my work at the National Museum of Natural History, I attended a lecture by James Farris and what happened in that presentation made me coin (for my own usage) the term "cult" for cladists and cladistics. What is your take on the usual "cult"-followers narrow-minded scientific views, where no method is better than them and sometimes even alignment software is demonized._

JF: Now you have some sense of what the atmosphere was like in morphological systematics in the early 1980s.  At that time most young systematists had joined the Hennig Society in a fit of enthusiasm for phylogenetic systematics, and work coming from any other intellectual source stood a good chance of being rejected out of hand as "not being science". My own guess is that this level of excessive zeal was a reaction to the inertia in systematics, as all the main professorships and curatorships then were in the hands of followers of Mayr and Simpson, the "evolutionary systematists", who would not make their methods explicit.  The way to intimidate them was to up the temperature of the debate. This attracted people with certain kinds of personalities.

You aren't the first person to analogize the behavior of this group to an evangelical religion. The Hennig Society types have always wanted to be seen as having a key to understanding everything phylogenetic, a key that everyone else lacked. In the longer run, their behavior alienated their own base, and there were internal conflicts. Most young systematists deserted the Hennig Society and started coming to the Evolution Meetings, where the discussion is fairly normal in tone, personal attacks are discouraged, and there is a lot of good-natured discussion among people with different views.

(I don't think the issue is whether or not one uses cladistic approaches to classification, as most of the reasonable young systematists at the Evolution meetings take that position).

What interests me is that the hard core of the Hennig Society has not mellowed or compromised. I was expecting that they would, but they have not only remained as ferocious, but continued to hold views very distinct from everyone else's. They have circled the wagons and are still holding out, though they must be getting a bit lonely by now.

_Lately two big projects related to phylogenetics are getting some steam: the Tree of Life and the DNA barcoding. I am more aware of the latter, due to the fact that I attended a presentation about it and through a friend that woks on the project. I think that the goals of the
DNA barcoding are great for the field, wet-lab and theoretical scientists. What is your opinion about this type of project that tries to address all subjects in a big umbrella? Wouldn't the support of a larger number of small projects be better?_

JF: I don't really object to big projects as long as they don't suck up the money for everything else.  I was on the Genbank Advisory Committee some years ago, and I think the DNA and protein databases and Pubmed are examples of important and necessary large-scale projects.  So although I worry about money for small projects being soaked up by the big ones, I don't object to the latter in principle.  In Canada they used to have a system of giving out small amounts of money to everybody.  They are moving away from that now, but I don't think it should disappear entirely.

_You have in Phylip's grant webpage a "no thanks" section listing everyone that refused supporting the program along the years. In my opinion this is a bold statement and not very common in the scientific environment (at least not online). What would be your advice for the young scientist that is searching for financial support for his/her research? Should s/he be vocal when a strong application is rejected?_

JF: Generally, no.  I could do this because I felt confident enough in my reputation.  It was fun.  These granting agencies can say all sorts of fatuous things in their evaluations and they are never called on this. A web page is editor-free publication so I had fun with that. I had a hope that it might cause grant reviewers to think twice about getting themselves on that list by coming up with arbitrary and ill-thought-out objections. (Based on our lab's experience since then, alas, this isn't working). But for a vulnerable young researcher I would say no, don't succumb to that temptation.  You may get a reputation as a sorehead.  I know a few young scientists who are quite combative about any negative evaluation, and they do get a reputation as someone you don't want to deal with. However in these days of increasing difficulty in finding funds, it is tough for newcomers as the agencies are looking for any reason to say no.
