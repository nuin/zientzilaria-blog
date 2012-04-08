---
date: '2007-03-02 17:27:54'
layout: post
slug: geneious-a-reply-from-biomatters
status: publish
title: 'Geneious: a reply from Biomatters'
wordpress_id: '4'
categories:
- Bioinformatics - opinion
---

On the Geneious discussion forum, Tobias, has replied to my review(s) with very interesting points that I think need some further argumentation. I start dissecting his post:


> I remember your old post from a year ago and just read your new review, and I thought I'd address a few of the points you raised.


Although, I "raised more points" on my second review, which is based on a more mature version of the software, I had posted some interesting points on my initial assessment which haven't been touched by Tobias on his reply. Maybe because my first review was less critical, less "negative" than the second one. Regardless, I still think (and I will have this opinion until I see some software better than) that Geneious is a great piece of software and deserve a very high praise.


> Of course I am 100% biased because I work at Biomatters, but I would like to give my personal view on some points that you raised. You may of course take my affiliation bias into account when reading those


Bias acknowledged.


> 1. I agree that the free version gives you "limited resources" as you point out. But please do also consider that software is always limited, and in fact Geneious today gives you a lot more than the free version which you have positively reviewed a year ago. So the question here is whether you should compare today's free version with Geneious Pro, or with last year's free version and the other free software that is available. I lean towards the latter, and I think Geneious 2.5.3 scores very well in this comparison.


My first "positive" review praised the first version of Geneious. My second "negative" one "slammed" it, or maybe just gave a little bit of balance to the initial review. I agree that the number of free features in Geneious is good and software is always limiting. But with no bias, compare the pro and free versions.


> 2. The point of Geneious having "no groundbreaking or innovative feature that wasn't seen in other molecular biology/phylogenetics package" is probably more true than others you raise, however it is also true that Geneious does offer some unique and innovative functionality that I don't know from other bioinformatics software:
- collaboration (obviously there is a chicken and egg problem,
and it will only become really useful once many people start
using it). The new version of collaboration for Geneious 3.0 has
much improved collaboration features such as one on one chat
and will hopefully greatly accelerate this development.
- agents
Also, Geneious Pro offers many features otherwise found only in much more expensive software packages.


As I said, I could not test collaboration. I tried testing it with Daniel Batten, but we never found a right time to meet online. Regarding the interface, you can find similar or even better features in [BioEdit](http://www.mbio.ncsu.edu/BioEdit/bioedit.html), which is also free. But it has major disadvantages, as being Windows-only and being focused only on sequence alignment. Other software that can be comparable to Geneious is [bioOpen](http://www.aborygen.com/downloads/biOpen/), but falls in the same category as BioEdit: Mac-only and not even free. I don't know the price of bioOpen but its ordering form gives you the option to select which functionalities you want.


> 3. You ask what incentive someone has to write a plugin for Geneious. If I was a bioinformatics student today and wrote software e.g. for my MSc project, I don't see what reasons there are *not* to write it as a plugin for Geneious.


I was never a bioinformatics student, maybe because during my time there were not many bioinformatics courses available, even more where I did my graduate studies. So I cannot give you a personal view as a "bioinformatics student". But first, we have to separate bioinformatics students in two classes (too few maybe): the computer scientist that understands biology and the biologist that programs computers. You can even include here a third class which is the computer-savvy biologist: he/she cannot program but have a high knowledge of computers.

With our categories defined I ask you again: what are the benefits of writing a plug-in for Geneious for each one of these classes of users?


> This is much easier than writing the functionality from scratch, because I don't have to worry about the graphical user interface - which is one of the biggest workloads in writing software.


I agree that writing plugins using a **proprietary** API is much easier than doing for scratch. I also agree that the interface is one of the biggest workloads in writing software. Being a interface programmer like myself, I understand how underrated the interface development is. But how many bioinformatics applications have interfaces? How many are cross-platform? And if I only need some functionality that Geneious does not give me but it would take a couple of hours to write in Perl/Python/Ruby ([like this](http://www.biomatters.com/userforum/comments.php?DiscussionID=87))? If I am a bench biologist with zero knowledge of programming do I have to wait for someone write me a plug-in or wait for Biomatters to include in Geneious?


> Also, it makes my program a lot more usable for a lot more people. Peer respect and publicity are among the strongest incentives - when people write free software, as many other people as possible using it is their *main* goal.


Of course it makes a program more usable for a lot more people. People that are using Geneious, right? How do you measure peer respect? By doing a wonderful program from scratch or by adding to a **proprietary** software a plug-in? Or, wouldn't be better to create a open source project (or join one) that works in bioinformatics development?


> I spent a considerable amount of time during my studies writing software, and I wish Geneious had been around back then - it would have made my software much easier to write and use, and it would have become known to a lot more people<


I did my Masters writing software and my PhD working on phylogenetics. Would Geneious help me in the first case? No (maybe with ideas). Would it help me in the latter? Definitely, yes. Would I spend time during my PhD to write plug-ins to Geneious? No. See the difference?


> 4. You suggest that we concentrate on writing plugins and sell licenses for using those. Really this isn't very far from what we are already doing - the main difference between Geneious and Geneious Pro is that Geneious Pro has more features, and most of these are provided plugins. So really there are already *lots*of plugins - it's just that most of them already come shipped with Geneious, instead of you having to download them in a separate file from our website. In fact, if other people were to write free plugins which provide all of the Geneious Pro functionality for free, the incentive for Geneious Pro would basically disappear. This is the only concern I personally have about our Public API - and it's about the opposite from yours.


This is not the first time I suggested this. I had discussions with Daniel Batten about this subject, and even point him some licensing possibilities, such as [MatLab](http://www.mathworks.com/). I saw the list of add-ons when customizing Geneious. Regarding your concern, I don't think it will be fulfilled.


> 5. The import feature hasn't always worked correctly for you. We would like to keep Geneious as bug free as possible, so if you could please email any files upon which Geneious fails to e.g. tobias@biomatters.com, then that would be much appreciated and we will fix these problems as soon as possible.


I have sent samples, even add to other topics guidance to some biological file formats. I personally don't have any file that I am working at the moment, but as everyone that releases a new bioinformatics application, releases a new filetype at the same time, the amount of filters and errors will be huge.


> We are typically quite responsive, even though we live in a different time zone to most other people.


When I say that is a disadvantage to be in New Zealand, is that sometimes users (especially the ones that pay) tend to be quite demanding. As I am not a Geneious user _per se_, this does not affect me.


> 6. There are now 4 plugins available for download, and a fifth will possibly follow soon. Only three of the currently available ones work for Geneious 2.5.x, but this will probably be fixed at some point. As our API stabilises and more plugins become available, we hope to introduce a more comfortable way of installing them and keeping them up to date.


There were only two at the time of my review. It is good that it is increasing, 100% in a couple of days. And going back to the "peer respect", I downloaded [MrBayes](http://mrbayes.csit.fsu.edu/) plug-in and I couldn't find the names of the developers. Also could not find any reference to MrBayes authors, papers, etc.


> 7. Scripting language support is already being developed. Update: It probably won't make it into Geneious 3.0, but nevertheless Geneious will have scripting support at some point.


Great. That was another thing that Daniel and I discussed last year. I think this is nice for people trying to create molecular biology, phylogenetics, etc courses for a large audience or for some university program. I couldn't find the Educational plug-in in Geneious.

Still, in my opinion Geneious is a great software.
