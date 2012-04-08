---
date: '2007-03-15 14:39:15'
layout: post
slug: interfaces
status: publish
title: Bioinformatics and interfaces
wordpress_id: '12'
categories:
- Bioinformatics - opinion
---

On the reply to my second Geneious review, an interesting point was raised: building interfaces, "which is one of the biggest workloads in writing software".

My first programming language was the old [Visual Basic 3.0](http://www.webdevelopersjournal.com/archive/vbasic.html) which has a visual driven user interface and programming approach. To create windows and dialogs in VB is an extremely easy process, dragging and dropping objects in a window, easily setting properties, menus and features. The interface design is straightforward, and the burden of a user-friendly program lies on the programmer and his/her ability to set the objects on the screen, manipulate their function and add programming elements to operate them.

But Visual Basic has it drawbacks, first by not being a powerful language and restrictions of only running resulting programs on Windows machines, etc. In Bioinformatics, Visual Basic is great for simple applications where the processing speed, heavy number crunching, portability, intense I/O operations and other high-performance issues are not a requirement. Applications like [WinPop](http://www.genedrift.org/winpop.php) (I will focus on my personal experience), that had version 1.0 released late 1998 ("compiled" with VB3.0) and version 2.5 which was released in 2004 and was "compiled" with the more advanced VB 6.0. WinPop is the perfect example of a good project for VB: simulates and represents simple Population Genetics phenomena with limited input and outputs nice looking graphs to help the user understands what is going on in each one of the models. WinPop is also geared to undergrad and grad students that need to learn Population Genetics, and can be used in any Windows machine (Windows 95 and up) and does not require a state-of-the-art box to run nor it will allow you to discover a major breakthrough in science.

VB programming is focused on the visual part. Your whole approach to develop the software has to consider the objects you see (and sometimes not) on the screen, how to link them if needed, which event will trigger what and so on. It is different than writing your script in Python, or your number crunching application in C++ or Java. In VB, there is the possibility of generating command line applications, but this is more difficult than creating one with a window. In Java you can opt to make a command line application or to create a GUI for it with Swing. In C++, everything is command line, unless you use one the GUI frameworks available, like [Qt](http://www.trolltech.com) or [wxWidgets](http://www.wxwidgets.org), which in some case is like learning a new language by itself. Some of these frameworks were ported to other languages too, like wxPython, wxPerl, PyQt.

Until recently, advanced Bioinformatics applications were command-line only. Examples can be found everywhere: alignment packages (Clustal has), Blast (web-interface, not very powerful), TFBS determination, HMM, phylogenetics (PAUP for Mac and Mega are most recognizable exceptions), etc, etc. Nowadays it is becoming easier to find good programs with nice interfaces, like [Geneious](http://www.genedrift.org/sugg.php), which are portable and powerful. But still, in my opinion researchers don't give much attention to the interface development.
