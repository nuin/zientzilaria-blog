---
author: admin
date: '2008-11-13 17:28:35'
layout: post
slug: creating-an-interface-for-the-motif-finding-script-part-8
status: publish
title: Creating an interface for the motif finding script, part 8
wordpress_id: '199'
? ''
: - bioinformatics
  - GUI
  - motifs
  - motifs
  - python
  - wxPython
  - wxPython
---

Let's see now how do we connect our GUI to the the pymotif file (I
changed the name because of some conflicts with the app name [my bad!],
the git repo was updated accordingly). And also how to display the
results, in a simpler manner. Ok, first to connecting the script to the
function file, pymotif.py. The file is already imported in our script
and we have used it before. We need to find the exact point and which
parameters to pass. pytmotif.py is a slightly modified version of your
command line script, and the code is below. [sourcecode
language='python']\#!/usr/bin/env python import fasta import sys from
collections import defaultdict def choose(n, k): if 0 <= k <= n: ntok =
1 ktok = 1 for t in xrange(1, min(k, n - k) + 1): ntok \*= n ktok \*= t
n -= 1 return ntok // ktok else: return 0 def get\_quorums(seqs, mlen):
""" add seq id\_no to a set use explicit counter to create seq\_no """
quorum = defaultdict(int) for seq in seqs: for n in range(len(seq) -
mlen): quorum[seq[n:n + mlen]] += 1 return quorum def
calculate\_motifs(input\_seqs, input\_seqs2): input\_seqs =
fasta.read\_seqs(open('celladhesion1000.fa').readlines()) input\_seqs2 =
fasta.read\_seqs(open('celladhesion1000C.fa').readlines()) foreground =
get\_quorums(input\_seqs, 10) background = get\_quorums(input\_seqs2,
10) N = len(input\_seqs) + len(input\_seqs2) res\_motifs = [] for i in
foreground: term1 = choose(background[i], foreground[i]) term2 =
choose((N - background[i]), len(input\_seqs) - 1) term3 = choose(N,
len(input\_seqs)) p = (float(term1) \* float(term2)) / term3 if 0 < p <=
0.0001: res\_motifs.append(i + 't' + str(foreground[i]) + 't' +
str(background[i]) + 't' + str(p)) res\_motifs.sort() return
res\_motifs[/sourcecode] So, basically the line we are interested is
this one [sourcecode language='python']def
calculate\_motifs(input\_seqs, input\_seqs2):[/sourcecode] We replace
the wx.MessageBox line in our run\_finder function and use the input
files selected by the user as parameters for calculate\_motifs, and we
are done [sourcecode language='python']def run\_finder(self, event):
result = pymotif.calculate\_motifs(self.fore\_file,
self.back\_file)[/sourcecode] Very simple and direct. This should take
care of everything except the motif width, what we will see in the next
post. We still need a place to write the overrepresented motifs. We can
add a text box to the frame, and we do that by adding an extra
declaration in our \_\_do\_layout function. This time we need to add
some extra style to the box, so it can show multiple lines and has a
scroll bar. [sourcecode language='python']self.results =
wx.TextCtrl(panel, -1, '', (150, 50), (200, 100), wx.TE\_MULTILINE |
wx.TE\_AUTO\_SCROLL | wx.HSCROLL)[/sourcecode] Notice the wx. flags
added. MULTILINE allows the box to have multiple lines and the other two
turn on the auto scroll and horizontal scroll. Great. And how do we
write the results. Notice above that the function that calculates the
motifs, returns a list where each item has the motif sequence and the p
value, sorted. So the only thing we need to do is to iterate over the
list and print each line to the result box. That simple, and we
accomplish it by using the WriteText method, that receives as a
parameter a string, either literal or a string object. Our run\_finder
function will have a couple of extra lines [sourcecode
language='python']def run\_finder(self, event): result =
pymotif.calculate\_motifs(self.fore\_file, self.back\_file) for motif in
result: self.results.WriteText(motif + 'n')[/sourcecode] That will
present in a very simplistic way the resulting overrepresented motifs,
but it's enough for now. Our GUI script will be [sourcecode
language='python']\#!/usr/bin/env python import wx import pymot import
pymotif import fasta import os class pymot(wx.App): def
\_\_init\_\_(self, redirect=False): wx.App.\_\_init\_\_(self, redirect)
class pymotGUI(wx.Frame): def \_\_init\_\_(self, parent, id):
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
wx.TextCtrl(panel, -1, '10', (95, 50), (40,18)) \#result textbox
self.results = wx.TextCtrl(panel, -1, '', (150, 50), (200, 100),
wx.TE\_MULTILINE | wx.TE\_AUTO\_SCROLL | wx.HSCROLL) \#run bbutton
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
result = pymotif.calculate\_motifs(self.fore\_file, self.back\_file) for
motif in result: self.results.WriteText(motif + 'n') \#wx.MessageBox('It
should run, eh?') \#if \_\_name\_\_ == '\_\_main\_\_': app = pymot()
frame = pymotGUI(parent=None, id = -1) \#frame.CentreOnScreen()
frame.Show() app.MainLoop()[/sourcecode]
