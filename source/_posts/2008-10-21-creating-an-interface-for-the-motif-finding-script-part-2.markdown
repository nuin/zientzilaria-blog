---
author: Paulo Nuin
date: '2008-10-21 11:40:33'
layout: post
slug: creating-an-interface-for-the-motif-finding-script-part-2
status: publish
title: Creating an interface for the motif finding script, part 2
wordpress_id: '176'
? ''
: - bioinformatics
  - interface
  - motifs
  - motifs
  - python
  - wxPython
  - wxPython
---

Let's take a deeper look on the code we started yesterday, piece by
piece 

{% codeblock lang:python %}
class pymot(wx.App):
    def __init__(self, redirect=False):
        wx.App.__init__(self, redirect, filename)
{% endcodeblock %}

This is the class `pymot` we derived from wx.App,
and this will be the main class for your application. As any other class
derived it needs a OnInit or a __init__ function that will take care
of initializing things. As usual, we pass `self` and a `redirect`
parameter, that will tell the application to redirect some output to the
command line. We actually don't need a `redirect`, but it can be useful
in the future to track errors. It's set to false as we don't need it
now. 

{% codeblock lang:python %}
class pymotGUI(wx.Frame):
    def __init__(self, parent, id):
        wx.Frame.__init__(self, parent, id,  'Python Motif Finder', style=wx.DEFAULT_FRAME_STYLE)
        self.__do_layout()
 
    def __do_layout(self):
        pass

{% endcodeblock %}


This is the pymotGUI class derived, in this case, from wx.Frame. a wx.Frame
is the common window you see in most OS. As above, it needs a OnInit or
__init__ function, and here it initializes the window (but does not show it). In the first line of __init__ we have a call to format the
window we want to display. The frame method would need these
[paramaters](http://www.wxpython.org/docs/api/wx.Frame-class.html) to
customize the window 


{% codeblock lang:python %}__init__(self, parent, id, title, pos, size, style, name){% endcodeblock %} 

Both title and
style are set by default (not that they cannot be changed) in the frame
definition, and whe this is called and properly initialized, other
parameters can be passed and/or changed. There is a second defined
function in the `pymotGUI` class, `__do_layout`. This is a personal
preference of having all the layout methods for the window grouped in
one function. It helps organizing a bit the code and easier to browse
and correct it if needed. Most of the main part of the script could be
moved to the wx.App class derivation, but for now, we can keep it there.


{% codeblock lang:python %}
app = pymot()
frame = pymotGUI(parent=None, id = -1)
frame.Show()
app.MainLoop()

{% endcodeblock %} 


The first line initializes the application, the second calls and
initializes the frame. The method Show makes the window to be displayed.
MainLoop we saw last time. The skeleton of a wxPython script and
application is very simple. Now we need to populate our window, create
menus, buttons, and specially events. Next time we will include a menu
on the form and check how events are linked to elements.
