---
author: Paulo Nuin
date: '2008-10-20 16:31:50'
layout: post
slug: creating-an-interface-for-the-motif-finding-script
status: publish
title: Creating an interface for the motif finding script, part 1
wordpress_id: '171'
? ''
: - bioinformatics
  - interface
  - motifs
  - wxPython
---

And we are back. After much ado about real life, I am able to "restart"
this blog and probably with a good frequency of posts. Last time we saw
the final product of our motif finding series. We ended up creating a
very elegant script in Python that efficiently counts words in FASTA
sequences and then using a basic statistical method, calculates the
significance of each word and output the overrepresented ones. Our
script used a little bit less than 50 lines, and if you include the
imported fasta module, it won't top 100. But the number of lines is not
important. The efficiency, clarity and speed are key here. At the same
time, running a script from the command line is not something everyone
is used to do. In order to add more visibility to our simple script, why
not including a GUI? With a visual interface, more people can use our
script, in different systems. Sounds great. Python has many options of
GUI frameworks, some more cross-platform that others. In the end finding
the right framework is more a matter of taste, or availability. My
personal experience with [wxWidgets](http://www.wxwidgets.org) lead me
to start developing in [wxPython](http://www.wxpython.org), and for me
this was a natural choice. But there are many other GUI frameworks for
Python, each one providing more or less integration and portability (you
can "choose" you own [here](http://www.awaretek.com/toolkits.html)). So,
let's create a skeleton for our GUI. First step is to install wxPython.
Packages for Windows are available from their website, RPMs for Linux
and DMG for Macs (I'm quite sure OS X Leopard comes with wxPython by
default, just test importing it). After installing it, start Python and
check if everything is in place 

{% codeblock lang:python %}import wx
wx.__version__{% endcodeblock %} 

On my machine, I get no errors and the
version is 2.8.9.1 (you don't need the latest version to create the
GUI). Everything seems to be fine. A wxPython script has the same format
as any Python script, the only difference is that its output is not
directed to the prompt or a file. The script's product will be the
screen, so in most cases the output and program usage will depend on the
user's interaction with objects on the screen. Like any other graphical
interface. A very simple script would look like 


{% codeblock lang:python %}\#!/usr/bin/env python 
import wx 
class pymot(wx.App):
	def __init__(self, redirect=False): 
		wx.App.__init__(self, redirect) 
class pymotGUI(wx.Frame):
	def __init__(self, parent, id):
	wx.Frame.__init__(self, parent, id, 'Python Motif Finder', style=wx.DEFAULT_FRAME_STYLE) 
	self.__do_layout() 
	
def __do_layout(self): 
	pass 
		
app = pymot() 
frame = pymotGUI(parent=None, id = -1) 
frame.Show() 
app.MainLoop(){% endcodeblock %} 

Usually a wxPython
interface has three parts in its script: a class for the
window/frame/dialog, a class for the application and a initialization
routine. All wxPython applications, and scripts, need to derive an
wx.App class and initialize it (on OnInit or on `__init__` functions),
i.e. create the window, begin the program, etc. Another class, derived
from wx.Frame in this case, will build the window/frame/dialog *per se*
and will also contain initialization for the window, objects, events,
etc. The last part is the main script where the application is started,
by calling the derived class, the window is also called and shown. The
last line is the `MainLoop`, present in every wxPython script, and it is
the main line of the script, the heart of the application. MainLoop
processes all the events and manages how the objects interact by
receiving and dispatching such events. The script above could have been
created differently, some lines of it omitted and there is also no need
to derive an specific class for the frame. But this way it is easier to
get a grasp of the script as it will need to be enlarged so accommodates
the objects and maybe a couple of extra windows and dialogs. Running the
above script will generate the window 
very simple and barebones. Next will explore the script above, include
some extra elements and learn a little bit more of wxPython.