---
author: admin
date: '2008-10-22 15:30:13'
layout: post
slug: creating-an-interface-for-the-motif-finding-script-part-3
status: publish
title: Creating an interface for the motif finding script, part 3
wordpress_id: '178'
? ''
: - bioinformatics
  - interface
  - motifs
  - motifs
  - python
  - Section 2
  - wxPython
  - wxPython
---

Today we will add some elements to our interface. Looking at the
previous screencap it is easy to conclude that our interface needs a lot
of work to be ready. First, it has a dark gray background that does not
resemble the usual window background (it looks more like a MDI frame).
We need to change that. Also, there are no menu bars or menus, or tool
bars. It's pretty bare bones, and not exactly good or useful. There many
ways of customizing the look of a window/frame in wxPython, and two of
these methods are adding a panel to the frame or adding the so-called
sizers. The latter is a difficult method to master, but powerful and
very good to customize objects, look and feels of a window. Addin a
panel and subsequently adding objects to it is a more laborious process,
but easier to understand. We will start by adding the
[panel](http://www.wxpython.org/docs/api/wx.Panel-class.html) to you
`__do_layout` function (where most of our changes will happen for now).
Basically, only one line is required: [sourcecode
language='python']\#adding the panel panel = wx.Panel(self)[/sourcecode]
That's it, the wx.Panel method only needs one parameter, where the panel
is being added to. The name `panel` is the one that we will be using to
access methods and properties associated with the wx.Panel derivation
that we just created. Adding the menu would require a little bit more
code. As its predecessor wxWidgets, wxPython divides the menu in
subcategories. The menubar is based on wx.Menubar method, the menu
itself (File, Edit, etc) is a wx.Menu wehre each of the entries is
added. At the end each menu derived from wx.Menu will be added to the
menubar. In order case we have to initialize a menubar [sourcecode
language='python']\#defines the menubar menubar =
wx.MenuBar()[/sourcecode] and then initialize a menu element, which we
will call filemenu and will be labeled File [sourcecode
language='python']\#file menu filemenu = wx.Menu()[/sourcecode] This
will only initialize a menu element with the name `filemenu`, it won't
add anything anywhere. In our case from the start, as we didn't do any
planning on how our interface would look like (no UML, no case studies,
nothing!), we need at least three menu items: one to open/set the
foreground sequence file, one to open/set the background sequence file
and one to quit the application. So what we are going to do is append
these items to the `filemenu` [sourcecode language='python']convertmenu
= filemenu.Append(-1, 'Select foreground file') seqmenu =
filemenu.Append(-1, 'Select background file') sep =
filemenu.AppendSeparator() treenooutmenu = filemenu.Append(-1,
'Quit')[/sourcecode] that simple. The first two lines and the last one
append the items that open/set files. The -1 parameter is an ID, as we
saw previously, when no ID is required for our code we use -1, and the
second parameter is the label of that menu item. The menu item `sep` is
a separator, keeping apart the file open/set items and the quit element.
One final thing is append the derived wx.Menu to the menubar and set it.
We accomplish that by [sourcecode language='python']\#appends the menu
to the menubar and creates it menubar.Append(filemenu, 'File')
self.SetMenuBar(menubar)[/sourcecode] Line 2 initializes menubar on
self, also known as pymotGUI, our main window. Putting everything
together our code would look like [sourcecode
language='python']\#!/usr/bin/env python import wx import pymot import
fasta class pymot(wx.App): def \_\_init\_\_(self, redirect=False):
wx.App.\_\_init\_\_(self, redirect) class pymotGUI(wx.Frame): def
\_\_init\_\_(self, parent, id): wx.Frame.\_\_init\_\_(self, parent, id,
'Python Motif Finder', style=wx.DEFAULT\_FRAME\_STYLE)
self.\_\_do\_layout() \# self.\_\_do\_binding() def
\_\_do\_layout(self): \#adding the panel panel = wx.Panel(self)
\#defines the menubar menubar = wx.MenuBar() \#file menu filemenu =
wx.Menu() foreground\_menu = filemenu.Append(-1, 'Select foreground
file') background\_menu = filemenu.Append(-1, 'Select background file')
sep = filemenu.AppendSeparator() quit\_menu = filemenu.Append(-1,
'Quit') \#appends the menu to the menubar and creates it
menubar.Append(filemenu, 'File') self.SetMenuBar(menubar) \#if
\_\_name\_\_ == '\_\_main\_\_': app = pymot() frame =
pymotGUI(parent=None, id = -1) \#frame.CentreOnScreen() frame.Show()
app.MainLoop()[/sourcecode] and this would look like the screencap below
(on Vista).
[![gui2](http://python.genedrift.org/wordpress/wp-content/uploads/2008/10/gui2-150x150.png "gui2")](http://python.genedrift.org/wordpress/wp-content/uploads/2008/10/gui2.png)
Next time we will work on more elements and activate the menu items.
