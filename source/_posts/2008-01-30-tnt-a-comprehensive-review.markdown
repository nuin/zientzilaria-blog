---
date: '2008-01-30 14:41:52'
layout: post
slug: tnt-a-comprehensive-review
status: publish
title: 'TNT: a(n) (almost) comprehensive review'
wordpress_id: '86'
categories:
- Bioinformatics - opinion
- Science
tags:
- maximum likelihood
- parsimony
- review
- TNT
---

As promised I'm writing about the free version of TNT. So far I was able to test the Linux version which does not have a graphical interface. I am planning to download a Windows version and test it, but not until next week. So far here are my impressions.

When you start TNT you are greeted by its own prompt, in identical fashion to PAUP and MrBayes. As a regular user (or most of the regular users) I fired up TNT without reading the manual, so my first attempt was to write help at the prompt and the prompt answered by changing itself from ">tnt*" to ">help". One point against TNT, as either PAUP of MrBayes at least display a list of possible commands. Feeling helpless I decided to access the manual. 

**The Manual**

Oh, my eyes!!! Whoever chose the background colour for the html manual might have an agreement with some optometrist. I cannot read a paragraph without averting my eyes for a "refresh" (if you are interested search for bgcolor=aqua). Anyway, the introductory part of the manual tells you to do exactly what I did, by entering "help" at the prompt. Second thing it tells you is that if you don't have a Windows version it is not possible to convert your files (i.e. fasta, phylip, nexus) to TNT's own format. Usual, it follows the rule, _one application_ - _one format_, they just forgot to include _one converter_. Just adding insult to injure they suggest that you use a text editor, anyone, and check their example files. Yeah, right. Basically TNT read Hennig86 matrices. Just get them from your 5 1/4" floppies.



> update: there is a way to display the commands at the prompt. "help" alone does not work, it has to be followed by a ";", but the manual says "help "





> update II: according to the manual TNT is able to read NEXUS files and can even include TNT commands in a block. Good.





**Using TNT**

Apparently TNT has a good selection of commands, from what can be seen from its help. It covers most of the things you want to study by using parsimony. It is mentioned in the manual that TNT does not do maximum likelihood (don't say!) or bayesian analysis (geez!), but they will incorporate some ML algorithms, even though rudimentary (I bet!).

So, from my shell I started TNT and as I would do in the PAUP CLI version just put the filename as a parameter

./tnt primate-mtDNA.nex (if you really noticed I was using one of PAUP's example files)

No dice. So I dig deeper in the manual and find a section dedicated to us poor Linux and OS X users



> Linux and Mac OS X versions of TNT have a couple differences with the standard versions.  First, those versions can take a comma ( , ) instead of a semicolon ( ; ).  This is because the shells there use semicolons to separate commands, and giving arguments to TNT from the command line becomes difficult. Second difference is that those versions can run in the background.  If you want to start TNT in the background, use bground as first argument, then give the normal arguments you would give the program (do not activate reports and do not change the silent status, but you can set report+ to report every certain number of trees, replications, or seconds, so that you can monitor progress by inspecting the output file; make sure you do have output files, otherwise the program would run and exit without doing anything!), and end with the usual '&'.  TNT will not write to the console, or expect console input (at least if no errors occur). It will write its results to a file and exit smoothly (exit code is 0; if the program runs out of commands while in the background it exits with code 1). Should some error occur during the search, the program writes a message to the ouptut file, and exits with code 255.  Try

     ./tnt bground p zilla.tnt, echo=, log peep, rep+1, mu10=ho3, le, ne, quit, &

and do "tail –f peep" to monitor search progress.



Very simple and straightforward. But at least I got a clue on how to open a file or use it as a parameter. So I repeat my first command line with the parameter p and then the filename

./tnt p primate-mtDNA.nex

Success ... no not so fast. An error is reported:

PISH (Phylogenetic Inference SHell)

Reading from primate-mtDNA.nex
Reading file primate-mtDNA.nex as NEXUS





> Data from:
        Hayasaka, K., T. Gojobori, and S. Horai. 1988. Molecular phylogeny
                and evolution of primate mitochondrial DNA. Mol. Biol. Evol.
                5:626-644.

  ... Skipping taxa block ...
  ... Skipping characters block ...
Error reading NEXUS file: expected cost
Error reading primate-mtDNA.nex
g = coding;    usertype 2_1 = 4  [weights transversions 2 times transitions



OK, fine. But what's PISH? No clue. I edited the file and removed the assumptions block, as TNT seems buggy to read square-bracket enclosed comments on PAUP blocks. I tried again and it worked but skipped both the characters and taxa blocks. Time to use one TNT's example files. So I chose the more evident _example.tnt_. I repeated the above command now using the tnt file as input. Everything works fine, data is read, stored and ready to go. Basically you have a number of commands that you can use to obtain your trees.  I used only **mult** which does multiple random addition sequences plus TBR (RAS+TBR) to find the most parsimonious tree(s). The program is fast for a morphology matrix of 84 characters and 112 taxa. In less than a second the tree is calculated.

But there is a major problem visualizing the tree(s): the so called PISH (Phylogenetic Inference SHell) does not allow scroll. So after obtaining the tree and using the **ne** command to visualize it you are left with a "tail" of the tree only. After some fidgeting I found a way to export trees to NEXUS format and could check the trees obtained. By using the command **export** with a dash and filenames as parameters.

tnt*>export -

**Conclusions**

TNT seems to be a powerful software and should be able to please anyone intending to employ parsimony as their phylogenetic method of choice. It is fast and, according to the documentation, is loaded.

On the other hand it is still (and probably will be for some time) limited and the CLI version for Linux is not the poster version of a user friendly application. There are many drawbacks and it is very difficult to learn the program without a deep study of the manual. Also the documentation is more focused to the GUI Windows version and the commands that can be used in Linux/OS X are not clear at first. In my opinion the worst feature of PISH is the lack of scroll (if there is scroll I wasn't able to turn it on) especially when the tree visualization is selected. 

Overall is TNT is a fair application, geared to its already known audience. Even being free, I don't see it occupying the place of PAUP, Phylip and MrBayes in the phyloege. Not without major changes.

**_Update: another review, of the GUI version is available [here](http://blindscientist.genedrift.org/2008/02/03/tnt-review-of-the-graphical-interface/).**_

