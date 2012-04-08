---
date: '2007-11-19 13:29:47'
layout: post
slug: sciview-part-6-interview-with-dr-roderic-page
status: publish
title: 'SciView, part 6: interview with Dr Roderic Page'
wordpress_id: '70'
categories:
- Science
- SciView
---

This edition of SciView features Dr Roderic Page from the University of Glasgow. Among other things, Dr Page was the editor of the Current Protocols in Bioinformatics, is the Editor in Chief of Systematic Biology, is an avid [blogger](http://taxonomy.zoology.gla.ac.uk/rod/rod.html) and is the developer of TreeView, a phylogenetic tree visualization software. I had the opportunity to ask him about his bioinformatics work and his views on science. I would like to thank Dr Page. 
---------------------------------------------------------------------

_In your blog ([iPhylo](http://iphylo.blogspot.com/)) an usual topic is the management and flow of information in Biology/Phylogenetics. In your opinion what are the main  hurdles of this subject in science? With the ever increasing amount of  generated information, databases, scientific publications, do you think that we will reach a stage where it won't be possible to stay afloat in a sea of data?_

RP- Well I think we are well past the floating stage! What I think would be cool would be a service like Google News that automatically aggregates  
stories (for "stories" read "papers and data)" and summarises the Zeitgeist. This wouldn't be overly hard to do. [uBio](http://www.ubio.org/index.php?pagename=ubioRSS) has a service that classifies RSS feeds from journals by taxon. Imagine taking that, together with newly added GenBank sequences, and clustering the feeds by various topics. Then display that using a treemap (analogous to  Marcos Weskamp's [newsmap](http://marumushi.com/apps/newsmap/)). You could get an "at a glance" view of what is going on.

This is a bit of a half-baked idea, but it relies on things that are becoming more and more available: stable identifiers, and services that  
provide data (and/or links between data). I think these are the two key things that will help us manage the flood of data. Without identifiers we will struggle to realise when we are talking about the same thing (witness the frustration with [redundant links in Connotea](http://www.nodalpoint.org/2006/12/15/buggotea_redundant_links_in_connotea), even though much of Connotea's core functionality relies on stable identifiers), and services give us means to extract and manipulate data. We are slowly moving away from relying sole on web links, or thinking that merely "putting something on the web" is good enough.

Lastly, I've often argued that in some fields, such as phylogenetics, the days of the journal are numbered. I think what we really need is a database that can generate "reports" that function as a journal article (i.e., the contributor gets a citable paper), but where the submission process is primarily one of submitting data and protocols. Many papers in phylogenetics are of the sort "I think group x is way kewl, I grabbed gene y, used program z, and here is my tree". Why not submit these straight to a database, instead of what we have now, which is the original data (e.g., alignments) and trees are usually lost? Databases such as TreeBASE that largely collect data after publication are sparsely populated, hence much valuable data and results are locked up in PDFs on journal web sites. Every month a weighty copy of Molecular Phylogenetics and Evolution lands on my desk, and the wasted data and trees makes me want to cry.

_This is an identical question I asked Joe Felsenstein (with a twist): Lately two big projects related to phylogenetics are getting some steam: the Tree of Life and the DNA barcoding. I am more aware of the latter, due to the fact that I attended a presentation about it and through a friend that woks on the project. I think that the goals of the DNA barcoding are great for the field, wet-lab and theoretical scientists. What is your opinion about this type of project that tries to address all subjects in a big umbrella? Wouldn't the support of a larger number of small projects be better? How would this type of projects can contribute to the information management and flow?_

RP - Barcoding is the simplest of the two "big projects" -- it's a simple idea (and one that has been employed by microbiologists for decades), applied to things that we can see with the naked eye. As with all of these things, there's been much hype, controversy, and heated debate. My own sense is that much of this is dying down, and certainly most articles in journals like Systematic Biology are investigating the performance of barcoding methods, rather than engaging in philosophical or political debate. I think barcoding will generate a lot of data, much of which will be useful, probably in ways we don't expect. We will have standardised genetic samples taken at a known place at a known time from organisms whose identity is either known or can be inferred. I'm struggling to see why this isn't a good thing.

My sense is that large projects don't always scale well. You don't get 10x more out of a project simply because it has 10x as much money. You get administrative layers, and a lot of politics. If the big project is really lots of little ones, then it may well succeed. Barcoding is really lots of little projects -- everybody grabs their favourite beastie and sequences it. There aren't any great technological or intellectual challenges. I think the real problem is when the project has big goals, articulates a grand vision, then struggles to deliver. I suspect [CIPRES](http://www.phylo.org) is an example of a large project that hasn't delivered quite as much as it promised. My biggest fear is that the [Encyclopedia of Life](http://eol.org) may end up in this category.

_You have three different blogs, iPhylo, iSpecies and bioGUID, but none of them are, what I can call, Open Science. Would you consider endeavouring in this new trend and opening up your scientific activities?_

RP - You missed one blog -- [http://semant.blogspot.com](http://semant.blogspot.com). I guess it depends what you mean by "Open Science." These blogs are pretty open about the success and failure of various projects, and I don't shy away from thinking out aloud. In some cases suggestions I've made in the blogs have been taken up and explored further by others. The Pygmybrowse widget to display large trees in a small space is a recent example.

For some time I've done things like post final reports on research grants online, as well as manuscripts that didn't make it into print (these are now available in Nature Precedings).

Not all the code I write is available. Some projects, like the [Taxonomic Search Engine](http://taxonomicsearch.sourceforge.net/) and [MyPHPBib](http://myphpbib.sourceforge.net/) are hosted on SourceForge, and [TreeView X](http://darwin.zoology.gla.ac.uk/~rpage/treeviewx/) is also open source (code available from my site, and as part of the Debian repository). Other stuff is sometimes so experimental and fluid that it would be more trouble than it is worth to package it nicely. Some legacy code uses libraries that are not Open Source and hence can't be distributed. That said, I'm looking at hosting current projects (such as [http://bioguid.info](http://bioguid.info)) on Google Code. Since 2005 anything which I've published as first author has been Open Access, and any software or data described in those papers is Open Source.

_Sometime ago, in the Nature Network's Bioinformatics group someone was asking about good protocols in the field. Can you tell us about the Current Protocols in Bioinformatics, which is was edited by you? How content is added to it and how frequent are the updates?_

RP - I'm no longer involved with [Current Protocols](http://www.currentprotocols.com/WileyCDA/CPTitle/isbn-0471250937.html). It was a great project to be involved with as it opened my eyes to the breadth of the field, and I got free trips to the US to meet with the other editors (I'm easily bought). Eventually I just had too many other commitments (it overlapped with being editor of [Systematic Biology](http://systbiol.org)), so I left the board.

Content is commissioned by the editorial board, who each handle 2-3 topic areas. Updates come out every three months. If you have the print version (currently two massive ring binders), then you have the fun task of inserting new sections and removing old content.

_What do you think is the importance of protocols in Bioinformatics? Isn't bioinformatics a field more dynamic than cytogenetics and molecular biology for instance?_

RP - This is an interesting point. I think there are some protocols which are  widely used and are reasonably stable over time (BLAST searching, for example), and others which either are short lived (the software keeps changing, or the question being addressed by the protocol looses its relevance). In some ways Current Protocols is an old fashioned way of providing information on how to do things. A wiki may be more appropriate, certainly it could be more dynamic, and ideally free. However, one could ask whether a wiki would have acquired the same degree of authority as the Current Protocols, which could assemble a board of people with broad expertise and experience, pay contributors for their work, provide copy editing and other editorial assistance, plus give a commitment to maintain and update the publication.


_Another question that is already favourite of this interview series is about computer graphic interfaces. TreeView(X) is a very important application in Phylogenetics and it is basically interface only, as the main focus is to display phylogenetic trees. Usually, a good percentage of messages sent to Paup's discussion list are somewhat related to TreeView. What in your opinion is the importance of a graphical interface for a biologist?_

RP - Well, unless you only use Lynx as your web browser, and vi to edit text, then I think the importance of the graphical interface is pretty much self evident! I think graphical user interfaces are desirable in two sets of circumstances: (1) the software is infrequently used, or (2) the user is not a "power user". When I was at Oxford a colleague told me that he liked graphical interfaces because, after weeks in the field, the last thing he needed was to have to learn (or relearn) some garbled syntax in order to analyse his hard-won data. I've also seen the difference a graphical interface can make when teaching students -- you want to keep the mechanics of using the software out of the way and let them focus on what they are actually doing (and why they are doing it).

Of course, graphical interfaces can get in the way as soon as you want to do something not originally thought of by the person who wrote the program. This is one reason why David Swofford's PAUP* is a model of flexible software. There is an elegant GUI (sadly fully available on Mac Classic only, although the Windows version has some of the essential features such as the spinning cursor and the PAUP Monaco font, both things I ported across a decade ago), and the command-line interface for batch processing.

_Continuing on TreeView(X), your latest version is pure wxWidgets. Why did you choose this framework to develop TreeViewX? Why not QT or Java or another GUI framework? How TreeViewX is different to the initial version of TreeView?_

The short answer is that I have a lot of code written in C++, and I haven't the time nor inclination to learn Java. When Java come along in the early '90's it's big selling point was cross-platform portability. Well, it didn't support the Mac terribly well, and I had my own C++ class libraries that worked natively on Windows and Macs, so there was no incentive to use it. Until fairly recently most Java applications I've seen are sluggish and/or poorly designed. When the time came to look at supporting Linux (around 2000), Qt wasn't an option because it wasn't free on Windows, and didn't support the Mac. So, wxWidgets was the logical choice, although it took a while for the Mac version to be usable.

TreeView X differs from TreeView in being Open Source, and available for Windows, Mac OS X, Linux, and other forms of Unix. It lacks some of the nicer features of the original TreeView (which only runs on Windows and Macs), mainly because I haven't had time to add them, and my own work has focussed more on web application development. Like many people who program, the software I write addresses problems I'm interested in at the time, so if my interests change, the software may languish.

_In your opinion what is your greatest contribution to science. A software, a publication..._

RP - I don't think there's any easy way to answer that. Let me respond by breaking it down into three categories. What contribution was the most fun, what was the most satisfying, and what do I think people will associate with me?

The most fun I've had is blogging, or to be more precise, trying to make connections between different areas such as bioinformatics, biodiversity informatics, systematics, digital libraries, and the Semantic Web. My hope is that readers of blogs like iPhylo will get something out of it, but ultimately I don't particularly care because, hell, I'm having a ball.

In terms of satisfaction, I enjoyed working on mincut supertrees. This was a change of topic (aggregating small phylogenies into one large "supertree"), required programming algorithms (rather than, say, graphical interfaces), and was my first introduction to the world of publishing in the computer science literature (the joys of LaTeX, and the requirement of having your paper accepted for publication BEFORE you could give a talk). It was also one of the best refereeing experiences I've had, because one diligent referee read my source code and pointed out that what I said I was doing in the manuscript and what my code actually did were not quite the same thing (I guess you'd call this an example of "Open Science").

But, if your question is what will people associate with me, then I think that is the work on "historical associations", namely genes and species, hosts and parasites, and areas and phylogenies. Making the case that these are all equivalent questions, and could be approached using the same algorithm, is probably the thing I could point to as being the thing that I have have done that was "significant".

-------------------------------------------------------------

I would like to thank Dr Page for taking the time to answer my questions.
