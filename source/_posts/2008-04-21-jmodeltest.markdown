---
date: '2008-04-21 14:26:03'
layout: post
slug: jmodeltest
status: publish
title: jModelTest
wordpress_id: '135'
categories:
- Bioinformatics - opinion
tags:
- Akaike Information Criterion
- Bayesian Information Criterion
- Java
- jModelTest
---

[![ResearchBlogging.org](http://www.researchblogging.org/images/rbicons/ResearchBlogging-Medium-White.png)](http://www.researchblogging.org)

_tested on a Pentium 4, 3 Ghz running Fedora Core 8_

David Posada released sometime ago [jModelTest](http://darwin.uvigo.es), a program that tries to be the ultimate maximum likelihood model selector for phylogenies. Written in Java, jModelTest is cross-platform, but differently from the latest available Java-based programs that are executables, the program is distributed as a jar file. Other programs like [TreeStat](http://tree.bio.ed.ac.uk/software/treestat/) have "compiled" versions for Macs and Windows, so why not jModelTest? 


The manual mentions that it was created using Xcode under OS X and even though Xcode provides a great environment for interface design, jModelTest interface is very simple, poor. It is basically a non-shrinkable window with a text editor/log occupying its entirety. All actions are provided with menus, no buttons or other widgets at first. Some example files are bundled with the package, and they show the versatility of jModelTest that allows input of different file types, phylip, nexus among others. This is an excellent aspect of the application that should be followed by other packages and programs.

After firing up jModelTest, I decided to load one of the files, example.phy, composed of 10 sequences of 1000 nucleotides. After using the File menu, it was easy to notice a major problem with the menu items. All of them have menu accelerators, simple key combinations to easy access menu items from the keyboard, but they are noted as Meta + _letter_ (I am having trouble uploading images on Wordpress, I will find a solution later). OK, the Meta (option) key on a Mac is easy to get, and Windows and Linux? The file loaded fine but so my next guess (yes, I don't read manuals upfront) was to use the Analysis menu. Luckily only one item was enabled, the one to calculate the likelihood scores.

ModelTest, that can be called a predecessor of jModelTest, used PAUP externally to calculate the likelihood scores for different methods. Now, [Phyml](http://atgc.lirmm.fr/phyml/) is used on the background, hence the average to good speed of jModelTest calculations. After selecting _Analysis->Compute likelihood scores_ the program presented a simple dialog with some options to set the likelihood calculation parameters. I tested the ML optimized topology with 11 substitution schemes (default). It took roughly 4 minutes to calculate the 88 available models for the example.phy file, with a good amount of log information output to the main screen. After that, there were three other items enabled in the _Analysis_ menu, allowing for different statistical calculations of the best ML model. It was possible to generate AIC (Akaike Information Criterion), BIC (Bayesian Information Criterion) and DT (Decision Theory) to determine the best (or ideal) ML evolutionary model while hLRT calculation was not enabled. All three were performed with default parameters, with AIC and BIC being very fast and DT very slow and memory hungry.

The results from the statistical analysis were displayed in the same log text box and in some places very confusing 



> 
There are 88 models in the 100% confidence interval: [ HKY+G TPM2uf+G TrN+G TIM2+G TPM1uf+G TIM1+G TIM3+G TPM3uf+G GTR+G TVM+G TVM+I+G GTR+I+G TPM3uf+I+G TIM3+I+G TPM2uf+I+G TIM2+I+G HKY+I+G TrN+I+G TPM1uf+I+G TIM1+I+G TPM1+I+G K80+I+G TPM2+I+G TPM3+I+G TrNef+I+G TIM1ef+I+G TVMef+I+G TIM3ef+I+G TIM2ef+I+G SYM+I+G K80+G TPM1+G TrNef+G TIM1ef+G TPM3+G TPM2+G TIM3ef+G TPM1uf+I TPM2uf+I TVMef+G TIM2ef+G HKY+I TIM2+I TPM3uf+I TrN+I TVM+I TIM1+I SYM+G GTR+I TIM3+I K80+I TPM1+I TPM3+I TrNef+I TPM2+I TIM1ef+I TIM3ef+I TVMef+I TIM2ef+I SYM+I F81+I+G F81+G JC+I+G JC+G F81+I JC+I TIM1 TIM3 TrN TPM3uf TPM1uf TVM TIM2 HKY GTR TPM2uf TIM1ef TrNef TPM1 K80 TIM3ef TPM3 F81 TIM2ef TPM2 SYM TVMef JC ] 



and in other places misleading



> Model selection results also available at the "Model > Show model table" menu



as there is no such menu entry. Maybe the developer was referring to _Results->Show Results table_ menu, but you never know. This results table presented all the values calculated for all test models, pointing out the suggested model in red. It was clearer to check the values in a grid than the main log window/text interface. There were some other tools in jModelTest to calculate the likelihood ratio test and model-averaged phylogeny. Also most calculations allowed the generation of a PAUP block, which in still widely used.

As a package, jModelTest is somewhat solid, even though the interface is bland and buggy (menu accelerators, wrong information in logs, it does not access help in Linux), computation of certain tasks is time consuming (Java?) and the manual contains some wrong terms (Operative (sic) Systems). It is easy to use and should be a good replacement for ModelTest (and PAUP). 

Apart from the ease of use and the analytical capabilities, there are some issues with the jModelTest: 




	
  * the program is distributed under the GPL, but there is no source code in the package and no information on how to get the source in the manual or the webpage. Should I write the author?

	
  * indeed is great the jModelTest makes possible to break free from the PAUP relationship, but at the same time is a double standard to use other applications under-the-hood and not allowing ModelTest to be distributed the same way in the past. As an excuse to control all possible copies and downloads of ModelTest, Posada didn't allow me to distribute the ModelTest executable with [MrMTgui](http://genedrift.org/mtgui.php). So much for GPL'ing your programs

	
  * the download process is very '95ish, where you have to enter name, email and institution in order to get the link. Someone should invent access logs ...



Posada, D. (2008). jModelTest: Phylogenetic Model Averaging. Molecular Biology and Evolution DOI: [10.1093/molbev/msn083](http://dx.doi.org/10.1093/molbev/msn083)

[![](http://img.zemanta.com/pixie.png?x-id=abf013e6-fd32-47a5-ae50-afad381cbdfb)](http://www.zemanta.com/)
