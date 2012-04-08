---
author: admin
date: '2008-11-04 17:39:01'
layout: post
slug: creating-an-interface-for-the-motif-finding-script-part-6
status: publish
title: ' Creating an interface for the motif finding script, part 6'
wordpress_id: '193'
? ''
: - bioinformatics
  - motifs
  - motifs
  - python
  - wxPython
  - wxPython
---

Last entry we saw how to allow the user to open a file. Now we need to
work on this file and store its path so the script can process it later
on. After the file is selected on the file menu, the filename is printed
on the label. Let's think for a second ... If we get only the filename
from the dialog, the program won't work, because the file might be
located in another directory, partition, you name it. So we need tp get
the file's full path. We need to change the lines [sourcecode
language='python']back\_file = dialog.GetFilename()
self.fore\_label.SetLabel(dialog.GetFilename())[/sourcecode] by
[sourcecode language='python']back\_file = dialog.GetPath()
self.fore\_label.SetLabel(back\_file)[/sourcecode] (do not forget to do
the same to the fore\_file!). Let's run the script and check what
happens. The frame should look like the one below (with a little
stretching for me). [![new
gui](http://python.genedrift.org/wordpress/wp-content/uploads/2008/11/gui4.png "new gui")](http://python.genedrift.org/wordpress/wp-content/uploads/2008/11/gui4.png)
OK, so this is part is solved. As we haven't planned our application
from the start, we will spend sometime thinking of the basic
functionality that we migth need. So far, we need one input box, where
the user can enter the motif width to be searched, and a button to start
the process. Fine, let's add the input box. For this we also need an
extra label to tell the user what the box is for. Always working on our
\_\_do\_layout function we add two lines [sourcecode
language='python']self.one\_label = wx.StaticText(panel, -1, 'Motif
width', (10,50)) self.motif\_width = wx.TextCtrl(panel, -1, '10', (95,
50), (40,18))[/sourcecode] Simple as that we have a input box. For the
button, one line will suffice [sourcecode
language='python']self.run\_button = wx.Button(panel, -1, 'Run', (10,
80))[/sourcecode] As we can see there is not much difference in any of
the declarations, they follow a similar process and the parameters are
more or less identical in some of them. Now, we need to bind the button
to a function, that we will call `run_finder`. Remember that binding
needs an event type, a target function and an object. This time the
event is a button event, but the other two parameters are similar.
[sourcecode language='python']self.Bind(wx.EVT\_BUTTON,
self.run\_finder, self.run\_button)[/sourcecode] and the function, for
now will look like [sourcecode language='python']def run\_finder(self,
event): wx.MessageBox('It should run, eh?')[/sourcecode] That's all for
today. Our script is growing and the full code is below [sourcecode
language='python']\#!/usr/bin/env python import wx import pymot import
fasta import os class pymot(wx.App): def \_\_init\_\_(self,
redirect=False): wx.App.\_\_init\_\_(self, redirect) class
pymotGUI(wx.Frame): def \_\_init\_\_(self, parent, id):
wx.Frame.\_\_init\_\_(self, parent, id, 'Python Motif Finder',
style=wx.DEFAULT\_FRAME\_STYLE) self.\_\_do\_layout() self.fore\_file =
'' self.back\_file = '' def \_\_do\_layout(self): \#adding the panel
panel = wx.Panel(self) \#defines the menubar menubar = wx.MenuBar()
\#file menu filemenu = wx.Menu() foreground\_menu = filemenu.Append(-1,
'Select foreground file') background\_menu = filemenu.Append(-1, 'Select
background file') sep = filemenu.AppendSeparator() quitmenu =
filemenu.Append(-1, 'Quit') \#appends the menu to the menubar and
creates it menubar.Append(filemenu, 'File') self.SetMenuBar(menubar)
\#input box for motif width, and label self.one\_label =
wx.StaticText(panel, -1, 'Motif width', (10,50)) self.motif\_width =
wx.TextCtrl(panel, -1, '10', (95, 50), (40,18)) \#run bbutton
self.run\_button = wx.Button(panel, -1, 'Run', (10, 80)) \#labels
self.fore\_label = wx.StaticText(panel, -1, 'Select the foreground
file', (10, 10)) self.back\_label = wx.StaticText(panel, -1, 'Select the
background file', (10, 30)) \#binding the menus to functions
self.Bind(wx.EVT\_MENU, self.on\_foreground, foreground\_menu)
self.Bind(wx.EVT\_MENU, self.on\_background, background\_menu)
self.Bind(wx.EVT\_BUTTON, self.run\_finder, self.run\_button) def
on\_foreground(self, event): dialog = wx.FileDialog(self, style=wx.OPEN)
if dialog.ShowModal() == wx.ID\_OK: fore\_file = dialog.GetPath()
self.fore\_label.SetLabel(fore\_file) def on\_background(self, event):
dialog = wx.FileDialog(self, style=wx.OPEN) if dialog.ShowModal() ==
wx.ID\_OK: back\_file = dialog.GetPath()
self.back\_label.SetLabel(back\_file) def run\_finder(self, event):
wx.MessageBox('It should run, eh?') \#if \_\_name\_\_ == '\_\_main\_\_':
app = pymot() frame = pymotGUI(parent=None, id = -1)
\#frame.CentreOnScreen() frame.Show() app.MainLoop()[/sourcecode]
