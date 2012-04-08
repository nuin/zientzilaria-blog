---
author: admin
date: '2008-11-18 14:45:31'
layout: post
slug: creating-an-interface-for-the-motif-finding-script-some-corrections
status: publish
title: Creating an interface for the motif finding script, some corrections
wordpress_id: '200'
? ''
: - bioinformatics
  - GUI
  - motifs
  - motifs
  - python
  - wxPython
  - wxPython
---

We need to pause a bit and do some corrections on our code. First the
code I posted on the last entry for the pymotif.py module is wrong. Ok,
not wrong, but some of the code I use to test ended up on the blog. Ths
first two lines of the calculate\_motifs function contained a link to
the files I use for testing and should be replaced by [sourcecode
language='python']input\_seqs =
fasta.read\_seqs(open(input\_seqs).readlines()) input\_seqs2 =
fasta.read\_seqs(open(input\_seqs2).readlines())[/sourcecode] Also both
variables that store the filenames and paths in pymoteGUI.py are
declared in the wrong scope. The should have be declared at the pymotGUI
class level, so it is accessible to all the functions in that class.
This also means that every time we access the variable it should be
preceded by the class name in order for the interpreter to know where
the to get the value from. So both corrected files would be [sourcecode
language='python']\#!/usr/bin/env python import wx import pymot import
pymotif import fasta import os class pymot(wx.App): def
\_\_init\_\_(self, redirect=False): wx.App.\_\_init\_\_(self, redirect)
class pymotGUI(wx.Frame): fore\_file = '' back\_file = '' def
\_\_init\_\_(self, parent, id): wx.Frame.\_\_init\_\_(self, parent, id,
'Python Motif Finder', style=wx.DEFAULT\_FRAME\_STYLE)
self.\_\_do\_layout() def \_\_do\_layout(self): \#adding the panel panel
= wx.Panel(self) \#defines the menubar menubar = wx.MenuBar() \#file
menu filemenu = wx.Menu() foreground\_menu = filemenu.Append(-1, 'Select
foreground file') background\_menu = filemenu.Append(-1, 'Select
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
if dialog.ShowModal() == wx.ID\_OK: pymotGUI.fore\_file =
dialog.GetPath() self.fore\_label.SetLabel(pymotGUI.fore\_file) def
on\_background(self, event): dialog = wx.FileDialog(self, style=wx.OPEN)
if dialog.ShowModal() == wx.ID\_OK: pymotGUI.back\_file =
dialog.GetPath() self.back\_label.SetLabel(pymotGUI.back\_file) def
run\_finder(self, event): print pymotGUI.fore\_file result =
pymotif.calculate\_motifs(pymotGUI.fore\_file, pymotGUI.back\_file) for
motif in result: self.results.WriteText(motif + 'n') \#wx.MessageBox('It
should run, eh?') \#if \_\_name\_\_ == '\_\_main\_\_': app = pymot()
frame = pymotGUI(parent=None, id = -1) \#frame.CentreOnScreen()
frame.Show() app.MainLoop()[/sourcecode] and [sourcecode
language='python']\#!/usr/bin/env python import fasta import sys from
collections import defaultdict def choose(n, k): if 0 <= k <= n: ntok =
1 ktok = 1 for t in xrange(1, min(k, n - k) + 1): ntok \*= n ktok \*= t
n -= 1 return ntok // ktok else: return 0 def get\_quorums(seqs, mlen):
""" add seq id\_no to a set use explicit counter to create seq\_no """
quorum = defaultdict(int) for seq in seqs: for n in range(len(seq) -
mlen): quorum[seq[n:n + mlen]] += 1 return quorum def
calculate\_motifs(input\_seqs, input\_seqs2): print input\_seqs,
input\_seqs2 input\_seqs =
fasta.read\_seqs(open(input\_seqs).readlines()) input\_seqs2 =
fasta.read\_seqs(open(input\_seqs2).readlines()) foreground =
get\_quorums(input\_seqs, 10) background = get\_quorums(input\_seqs2,
10) N = len(input\_seqs) + len(input\_seqs2) res\_motifs = [] for i in
foreground: term1 = choose(background[i], foreground[i]) term2 =
choose((N - background[i]), len(input\_seqs) - 1) term3 = choose(N,
len(input\_seqs)) p = (float(term1) \* float(term2)) / term3 if 0 < p <=
0.0001: res\_motifs.append(i + 't' + str(foreground[i]) + 't' +
str(background[i]) + 't' + str(p)) res\_motifs.sort() return
res\_motifs[/sourcecode] On the next post, the last in the series, we
will just check how to get the value from the width input box and
wrap-up everything. Technorati Tags:
[wxPython](http://technorati.com/tag/wxPython),
[python](http://technorati.com/tag/python),
[motifs](http://technorati.com/tag/motifs),
[GUI](http://technorati.com/tag/GUI)
