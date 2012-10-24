---
author: admin
date: '2008-10-30 14:45:19'
layout: post
slug: creating-an-interface-for-the-motif-finding-script-part-5
status: publish
title: ' Creating an interface for the motif finding script, part 5'
wordpress_id: '186'
? ''
: - bioinformatics
  - motifs
  - motifs
  - python
  - wxPython
  - wxPython
---

Last time we saw how to bind an interface element to a function. Now we
need to make good use of it, and make the script have some actual
functionality. First thing we are going to do is to include a label (or
static text) on the interface. Remember that initially we added a panel
to the frame, so the label should go on the panel. For a label we use a
[wx.StaticText](http://wxpython.org/docs/api/wx.StaticText-class.htm)
and has these parameters 



[sourcecode language='python'](self, parent,
id=-1, label=EmptyString, pos=DefaultPosition, size=DefaultSize,
style=0, name=StaticTextNameStr)[/sourcecode] 



We don't need all of them, just a couple would be enough. Basically, parent, id, label and pos will
do it, as the size would be default and based on the text length we
input. We are going to work on our __do_layout function and add two
labels to the panel on the frame, one for each the fore and background
files 


[sourcecode language='python']self.fore\_label =
wx.StaticText(panel, -1, 'Select the foreground file', (10, 10))
self.back\_label = wx.StaticText(panel, -1, 'Select the background
file', (10, 30))[/sourcecode] 


These two lines are very similar, only the
label, position and name change. panel is the name of the panel we
created previously, -1 is the ID, the string is the actual text that
will appear on the label and the values between parentheses are the X, Y
coordinates to display them on the frame. In the beginning (or when a
size needs to be set) we can add `pos=` to the label declaration in
order to make clearer what the values are setting 

[sourcecode language='python']self.fore_label = wx.StaticText(panel, -1, 'Select
the foreground file', pos=(10, 10))[/sourcecode]

If we add these two
lines and run our script, both labels will be there on the frame, as can
be seen in the screencap below. [![GUI with
labels](http://python.genedrift.org/wordpress/wp-content/uploads/2008/10/gui3-300x187.png "GUI with labels")](http://python.genedrift.org/wordpress/wp-content/uploads/2008/10/gui3.png)
Now, we need to add some functionality to the menus. The menu items set
previously, basically should work by presenting a file open dialog to
the user, where he/she can select a file that will be processed later
(or immediately). wxPython provides an option of automatically creating
a file dialog, by using the [wx.FileDialog
method](http://wxpython.org/docs/api/wx.FileDialog-class.html). This
method requires only one parameter, which is the style of the dialog.
The dialog can be of many types, i.e. for opening (single and multiple
files) and saving. the dialog call would look like [sourcecode
language='python']dialog = wx.FileDialog(self,
style=wx.OPEN)[/sourcecode] very simple and objective. But just
declaring won't make it show up on the screen. We need to actually call
the dialog's show method. Usually, most dialogs are
[modal](http://en.wikipedia.org/wiki/Modal_window), requiring some kind
of interaction between the user and the dialog before returning to the
application that called the dialog. Because of this behaviour we need to
use an if clause when showing the dialog, to check what type of result
returns from the user/dialog interaction. [sourcecode
language='python']if dialog.ShowModal() == wx.ID\_OK:[/sourcecode]
wx.ID\_OK is a internal method of wxPython that checks if the user
pressed the OK button on the file open dialog. If so, the program will
process the code, otherwise it will destroy the dialog and return to the
main application (or do something else if we set an elif clause). So,
all we need is set, we just need to put things together and add some
code when the user selects a file [sourcecode language='python']def
on\_foreground(self, event): dialog = wx.FileDialog(self, style=wx.OPEN)
if dialog.ShowModal() == wx.ID\_OK: fore\_file = dialog.GetFilename()
self.fore\_label.SetLabel(forefile)[/sourcecode] After the if clause,
the script will get the name of the selected file from the dialog and
then set the label of our StaticText (label!) with it. Straightforward.
We do the same thing for the background file and we have some code
going. One last thing, the objects `fore_file` and `back_file` are
declared on the \_\_init\_\_ function of the frame class, so they are
available to the whole frame scope. Our script will look like
[sourcecode language='python']\#!/usr/bin/env python import wx import
pymot import fasta import os class pymot(wx.App): def \_\_init\_\_(self,
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
self.fore\_label = wx.StaticText(panel, -1, 'Select the foreground
file', (10, 10)) self.back\_label = wx.StaticText(panel, -1, 'Select the
background file', (10, 30)) self.Bind(wx.EVT\_MENU, self.on\_foreground,
foreground\_menu) self.Bind(wx.EVT\_MENU, self.on\_background,
background\_menu) def on\_foreground(self, event): dialog =
wx.FileDialog(self, style=wx.OPEN) if dialog.ShowModal() == wx.ID\_OK:
fore\_file = dialog.GetFilename()
self.fore\_label.SetLabel(dialog.GetFilename()) def on\_background(self,
event): dialog = wx.FileDialog(self, style=wx.OPEN) if
dialog.ShowModal() == wx.ID\_OK: back\_file = dialog.GetFilename()
self.back\_label.SetLabel(dialog.GetFilename()) \#if \_\_name\_\_ ==
'\_\_main\_\_': app = pymot() frame = pymotGUI(parent=None, id = -1)
\#frame.CentreOnScreen() frame.Show() app.MainLoop()[/sourcecode] Next
we will keep adding elements on the screen and functionality.
