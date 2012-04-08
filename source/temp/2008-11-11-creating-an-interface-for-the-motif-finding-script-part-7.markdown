---
author: admin
date: '2008-11-11 13:53:09'
layout: post
slug: creating-an-interface-for-the-motif-finding-script-part-7
status: publish
title: Creating an interface for the motif finding script, part 7
wordpress_id: '197'
? ''
: - bioinformatics
  - GUI
  - motifs
  - motifs
  - python
  - wxPython
  - wxPython
---

Let's get back to the last post and check one line we entered\
\
[sourcecode language='python']self.motif\_width = wx.TextCtrl(panel, -1,
'10', (95, 50), (40,18))[/sourcecode]\
\
There is something in this line that I did not explain. The third
parameter in the test box declaration is `'10'`. How does this affect
our box? That's the default text that will be displayed inside the box
as soon as it is created. In our case, 10 is the motif width, and it's
the value we consider to be the most common search width.\
\
Another aspect not explained is the `run_finder`. We added a line \
\
[sourcecode language='python']wx.MessageBox('It should run,
eh?')[/sourcecode]\
\
where we declare a wx.MessageBox. What is it? A message box is the usual
error/information dialog that you see in most programs. In our case it
is very simple, just a warning/reminder that we need to include some
code there.\
\
Next time we will connect some Python source files and make our script
find some motifs.
