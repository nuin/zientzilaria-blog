---
date: '2007-08-11 09:53:56'
layout: post
slug: sciview-part-5-interview-with-alexei-drummond
status: publish
title: 'SciView part 5: interview with Alexei Drummond'
wordpress_id: '24'
categories:
- Science
- SciView
---

We are back with more interviews. This time it is Dr Alexei Drummond's take on Science and everything that surrounds it. Apart from his academic work, Alexei is Chief Scientist of [Biomatters](http://www.biomatters.com) the developers of [Geneious](http://blindscientist.genedrift.org/2007/03/02/geneious-one-year-or-almost-later/) (and [here](http://blindscientist.genedrift.org/2007/02/26/hello-world/)). Enjoy.

---------------------------------------------------------------------------------------

_You are Biomatters' Chief-Scientist, one of the founders of the company and the mastermind behind Geneious. What was your motivation to start the company and develop the program? How to balance these activities with your regular job as a university professor?_

I would say that my main motivations for wanting to build Geneious were frustration and hope. I was frustrated at the number of molecular biologists who didn't seem to have the software tools they needed to do their job. I was hopeful I could provide the framework for those tools, if only I had a few great programmers. 

Since I was one of the only people in the department who could program, I was often asked to write scripts, or teach people how to program enough so they could do it themselves. When biologists start asking about where they can learn to program a computer, just so they can do their job you know something is wrong! Most of the things they wanted to do were reasonably straightforward. It seemed to me that these kind of basic productivity problems had been solved in other workplaces like the office -- so why had they not been solved in the research laboratory? I initially wanted to build the system as an academic research project -- but then realized that would fail at a number of levels. Firstly, software development isn't science -- but science now crucially relies on software development and support. Secondly, most academic programmers are not interested in (or good at) designing user interfaces, and certainly developing software is not a scientific outcome that gets recognized like publishing papers does. Thirdly, academics are quite bad at supporting software and documenting it. So it seemed to me, that for a lot of reasons, a professional software company was the best avenue to realize a software system that would dramatically improve the productivity of molecular biologists by putting bioinformatics at their fingertips. Really I just wanted to make science go faster -- and with less hassle.

_ Geneious is a Java application? Why Java? Any special feature in the language or previous experience? Is there anything that you wish Java was capable of so you can include in Geneious?_

Java is a general-purpose programming language -- so you can do in Java pretty much anything you can do in software. The main reason for choosing Java is that it is very easy to write sophisticated user interfaces that run on Windows, Linux and Mac OS X. This is really important in the field of molecular biology where about 20% of the users have Mac OS X. Earlier versions of Java didn't integrate with some aspects of different operating systems as well as they could, but with Java 5 most of this integration is quite good. Also, more and more academic developers are using Java (because it is easy, cross-platform and OO) so that also works in our favor. Every language has its pros and cons, but  for our purposes Java was one of the best choices.

_You are the first scientist outside North America that is interviewed here. You have worked for some years in Oxford, UK. What are the main differences of working in New Zealand in comparison to Europe? How your return to New Zealand has influenced your decision to start the company?_

New Zealand is a very small country with just 4 million people. But we are a proud nation. But we have a long history of world firsts, like being the first country to give woman the right to vote (1893). A New Zealander was the first to "split the atom" (Ernest Rutherford), and a New Zealander was the first to the top of Mt Everest (Sir Edmund Hillary). We are also one of the first countries to declare ourselves a Nuclear-Free Zone (1985). So I would say that New Zealand is a place the is not afraid to try to lead the way, despite our small size. Our Prime Minister, Helen Clark, recently declared our Government's aspiration to make New Zealand a carbon-neutral country. It is these kinds of radical ideas that we strive to make reality. So it is quite natural to try to build a unique software package in New Zealand -- although we are still far from where we are aiming to be.

_In your opinion what are the main differences of developing applications in academia and in the private sector?
_

Academics develop software for the love of it -- and their first aim is to make the software work for themselves, and secondarily to work for their colleagues, as long as that doesn't take too much effort. There are a few academics that try very hard to produce easy-to-use well-supported software, but they tend not to have the resources to do what the private sector can - for example PAUP* still doesn't have a manual after many many years. The challenge for the private sector developing *scientific* software, is how to keep abreast of the science, which is changing so rapidly. At Biomatters we really try to have the idea that we are part of the scientific community. We have invited a number of scientist to work with us on various projects and we find that in this way we learn a lot more about what is needed, and how best we can fit into the academic ecology. Our goal is a happy marriage where academic programmers can get on with developing great new algorithms, and Geneious can provide the interoperability, the user interface and the support.

_What would you teach to an "academic developer"? What developers in academia lack when compared to developers working in companies?_

I don't think it is a question of what academic developers lack in terms of skills -- I think it is more a question of motivation. Aside from Geneious I produce academic software (like BEAST). What motivates me to answer 100 technical email queries every month about the BEAST software? My main passion is science, not supporting software. So by creating a successful software package, I have created a heavy burden of support. I would rather that somebody else supported all the simple questions about user interface, file conversion, installation, et cetera... So in some sense, what I am hoping to "teach" academic developers is that maybe there is another way to do things. It we had one framework that made interoperability and user interface more seamless and standard, each academic could focus on the science, the new algorithms and the part of their job that they find really exciting -- the discovery.

_Another question that is already favourite of this interview series is about computer graphic interfaces. Geneious has a very nice GUI, but in my opinion still lacks some simple features. Can you tell us how the program's GUI was first designed and what kind of user input is considered in the development? Which is more important: "what the user want" or "what we want"?_

Most users didn't say they wanted the mouse, or the iPod before the visionary told them they wanted it. So I do think there is room for a lot of innovation in software development. But of course, there are definitely things that users know that they need right now. Balancing these two things is the real trick. Biomatters is very serious about listening to our users and we have an active forum and a small group of power users that have been quite helpful in the past. Of course there is always more to do. We also think that we have introduced a few nice new ideas in our software and there are more on the way. Specifically we are interested in developing the concept of "live" research publications, where arrival of relevant new data automatically updates the published research in that area. As you can imagine, this is a long term goal. But I think you need these visions to aim for, if you are going to make real progress.

_For the young bioinformatician: should s/he focus on publications, skills, languages? Or a balance of all? What is your advice?_

A young bioinformatician should focus on the science. What are the outstanding questions that your skills enable you to take a step towards answering? Once you focus on the science the publications, skills and languages will come.

I used to program ten different languages very well. But 95% of my programming these days is done in Java (because I am usually building on stuff I have done previously). PERL is still quite important in bioinformatics -- but I think that is because there is still a lot of need to write one-off scripts. Will we get to a point where there is more sophistication? I think that bioinformatics has to become a field where people without programming skills can contribute substantially. I would argue that all of the programmers in bioinformatics should be working very hard to program themselves out of their jobs (and into more satisfying jobs). Lets build software systems that take this field to the next level. That is what we am trying to do (slowly but surely) with Geneious. We want to create a system that ultimately makes the programmers redundant -- at least for the menial tasks -- so that any molecular biologist can construct complicated queries and analyses in an intuitive graphical manner. Then the programmers can focus on the hard questions like new algorithms and methods of analysis.

_What in your opinion is your most important software?_

I don't really compare my software projects, because they are so different. I guess this is for other people to decide. But judging from you line of questioning, Geneious is currently winning ;-)

------------------------------------

I would like to thank Alexei for answering my questions.

