---
date: '2008-04-23 19:45:15'
layout: post
slug: how-to-improve-scientific-software
status: publish
title: How to improve scientific software?
wordpress_id: '138'
categories:
- Bioinformatics - opinion
tags:
- BMC Bioinformatics
- Computer software
- how-to
- improve
- Java
- Languages
- Open source
- Programming
- scientific software
- Source code
---

Do you know the answer to the above question? No? Me neither, but I can offer some suggestions. On a daily basis, a bioinformatician is exposed to hundreds of applications, computer languages, websites, you name it. Some of them are commercial, some of them free and open source. Some of the academia-developed software are open-source, some of them are not. 

A good portion of the academia-developed software are published in scientific journals, as an 2-page application note in [Bioinformatics ](http://bioinformatics.oxfordjournals.org/), or on a longer paper on [BMC Bioinformatics](http://www.biomedcentral.com/bmcbioinformatics/), just to name two of the journals of the field. 

I cannot complain of non-published applications. Usually they are free, open, and were developed during someone's spare time. I have the option of not using them, or modify them or helping the developer to improve it. I cannot complain of lack of documentation, bugs, minor errors or even the lack of an interface.

On the other hand, I can complain about published applications. Usually they are also free, but not always open and they were developed with a publication in mind, or at least as a mean towards a publication. It should have proper documentation, be slightly portable (yes, that's important, so if you are developing your next groundbreaking phylogenetic tool in [OCaml](http://caml.inria.fr/), distribute the executable, don't ask me to "compile" or install OCaml) and be easy or moderately easy to use. I give a break for the lack of interface.

And, why should I expect such things from a published application? Because, apart from the developers, at least one editor and two reviewers have (supposedly) tested (or glanced over) the application. Usually, scientific journals ask the authors to provide a copy of the package that is being submitted to publication. Basically one should include everything that is going to be installed, compiled, etc. So, a simple manual or readme, installation instructions, source code, executable(s), you name it, should be in the package.

I can say, from personal experience, that the majority of the published applications will have most of the items required for a user-friendly experience. But many fail in at least one of these aspects:



	
  * poor (or nonexistent) documentation

	
  * errors and bugs, too evident to be missed by the reviewers/editor

	
  * far from being user-friendly, even the command-line ones

	
  * non-portable (even between [Linux](http://en.wikipedia.org/wiki/Linux) distros)



This makes me ask myself: Are the editors/reviewers testing, checking, using these applications at all, before accepting the manuscript? I guess not, or it seems that they are not. Some errors you see in some applications are easy fix, and wouldn't harm the program's merit, but in the end would greatly improve user satisfaction and require less email exchanges with developers/scientists regarding bugs and errors. After all, you already published it, nobody told you that you have to support it, right?

This brings us to the original question: how to improve scientific software? Simple ... no, not really. 

Far from having the ideal solution, I will add my two cents:

1- Journals can to create a more rigorous publication process for applications, what would include more testing from the editor/reviewers. That would make the review process slower, will make editors and reviewers to spend time, that they already have in short supply, on a job that they are not  compensated for. Everybody will be unhappy and the process fails. So, if journals are willing to publish application only manuscripts, why not have an in house testing facility, at least to check for basic things that the authors claim their software should do? Too expensive for the journals? Maybe, maybe not.

2- Publication of applications _per se_ should be abolished. If you want to release an application and publish it, be sure you prove the merits of it with a publication that includes the software, its application and results that are scientifically relevant. This way we also abolish the publication-of-the-main-project, along with the paper on the application-that-was-used-to-generate-the-results and the paper about the program-that-was-used-to-display-the-results-generated-by-the-other-application. This way we would also foster collaboration between pure bioinformatics/application development groups with wet-lab groups.

3- Create a centralized scientific software repository, something like Sourceforge, and let people contribute, collaborate, code and develop and when the application is mature enough, publish it and give credit to everyone that had some input. Depending on the quality and amount of time dedicated to a project, the person would be a co-author or cited in the acknowledgments. This would also increase collaboration, people interested can learn and teach, exchange ideas and develop good application development standards, different computer languages, etc. Maybe you might not even need to publish the software in a journal, the user input and evaluations would be enough to solidify a good developer/scientist CV.

All options above are not mutually exclusive, they can be implemented at the same time, or they can't be implemented at all. Would Open Science benefit from this? I bet so.

[![](http://img.zemanta.com/pixie.png?x-id=c24ea5f5-9528-4569-ac1c-ce2cea8e07c7)](http://www.zemanta.com/)
