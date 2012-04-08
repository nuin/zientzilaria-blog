---
author: admin
date: '2007-03-15 09:43:10'
layout: post
slug: debugging-in-python
status: publish
title: Debugging in Python
wordpress_id: '28'
? ''
: - Section 3
---

Beginning the third section in our tutorial/guide, we are going to see
the chapter six of BPB. This chapter discusses the topics of creating
subroutines (in Python's case functions) and debugging the code. We are
going to start by the end. In Python, code debugging can be done as in
any other programming language: Perl has pdb, C/C++ has gdb, etc. Python
also has a pdb module that can be imported and run to check for errors
in your code. Using this command line: `python -m pdb myscript` will
start the debug module and this will run your script. If you are an
experienced programmer, who is just starting Python, pdb usage might
look simple and straightforward. On the other hand, if you don't have a
lot of experience in programming I would suggest a different approach,
as you become more comfortable with the language. Python has a great
advantage over some other interpreted languages, allowing you to
interactively code using the interpreter. So if your code is not working
properly, maybe a wrong output or a value that is not being correctly
calculated you have the options of coding the part of your script that
is not working using the interpreter or use the first rule of debugging:
include `print` statements that output the value of variables/objects.
Another option is to use a Python code editor, what will also help you
with highlight your code. I have little experience with Python code
editors, as I normally code in Linux and use
[Kate](http://kate-editor.org/). Lately I have been trying [Komodo
edit](http://www.activestate.com/products/komodo_edit/) which is a
cross-platform freeware from Active State. It looks pretty good but I
never tried debugging my code with it. So, these are my advices if you
are just starting to program. Maybe because of the age of Beginning Perl
for Bioinformatics (published in 2001), Perl's pdb was the only option
back then. Thanks to major advances on open-source and free software
there are many other options nowadays to debug your code.
`python -m pdb myscript`
