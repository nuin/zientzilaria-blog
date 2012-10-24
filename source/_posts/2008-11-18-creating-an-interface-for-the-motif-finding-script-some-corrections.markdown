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

We need to pause a bit and do some corrections on our code. First the code I posted on the last entry for the pymotif.py module is wrong. Ok, not wrong, but some of the code I use to test ended up on the blog. Ths first two lines of the calculate_motifs function contained a link to the files I use for testing and should be replaced by 

{% codeblock lang:python %}
input_seqs = fasta.read_seqs(open(input_seqs).readlines())
input_seqs2 = fasta.read_seqs(open(input_seqs2).readlines())
{% endcodeblock %}

Also both variables that store the filenames and paths in pymoteGUI.py are declared in the wrong scope. The should have be declared at the pymotGUI class level, so it is accessible to all the functions in that class. This also means that every time we access the variable it should be preceded by the class name in order for the interpreter to know where the to get the value from. So both corrected files would be



{% codeblock lang:python %}
#!/usr/bin/env python
 
import wx
import pymot
import pymotif
import fasta
import os
 
class pymot(wx.App):
 
    def __init__(self, redirect=False):
        wx.App.__init__(self, redirect)
 
class pymotGUI(wx.Frame):
 
    fore_file = ''
    back_file = ''
 
    def __init__(self, parent, id):
        wx.Frame.__init__(self, parent, id,  'Python Motif Finder', style=wx.DEFAULT_FRAME_STYLE)
        self.__do_layout()
 
    def __do_layout(self):
 
        #adding the panel
        panel = wx.Panel(self)
 
        #defines the menubar
        menubar = wx.MenuBar()
 
        #file menu
        filemenu = wx.Menu()
        foreground_menu = filemenu.Append(-1, 'Select foreground file')
        background_menu = filemenu.Append(-1, 'Select background file')
        sep = filemenu.AppendSeparator()
        quitmenu = filemenu.Append(-1, 'Quit')
 
        #appends the menu to the menubar and creates it
        menubar.Append(filemenu, 'File')
        self.SetMenuBar(menubar)
 
        #input box for motif width, and label
        self.one_label = wx.StaticText(panel, -1, 'Motif width', (10,50))
        self.motif_width = wx.TextCtrl(panel, -1, '10', (95, 50), (40,18))
        #result textbox
        self.results = wx.TextCtrl(panel, -1, '', (150, 50), (200, 100), wx.TE_MULTILINE | wx.TE_AUTO_SCROLL | wx.HSCROLL)
 
        #run bbutton
        self.run_button = wx.Button(panel, -1, 'Run', (10, 80))
 
        #labels
        self.fore_label = wx.StaticText(panel, -1, 'Select the foreground file', (10, 10))
        self.back_label = wx.StaticText(panel, -1, 'Select the background file', (10, 30))
 
        #binding the menus to functions
        self.Bind(wx.EVT_MENU, self.on_foreground, foreground_menu)
        self.Bind(wx.EVT_MENU, self.on_background, background_menu)
        self.Bind(wx.EVT_BUTTON, self.run_finder, self.run_button)
 
    def on_foreground(self, event):
        dialog = wx.FileDialog(self, style=wx.OPEN)
        if dialog.ShowModal() == wx.ID_OK:
            pymotGUI.fore_file = dialog.GetPath()
            self.fore_label.SetLabel(pymotGUI.fore_file)
 
    def on_background(self, event):
        dialog = wx.FileDialog(self, style=wx.OPEN)
        if dialog.ShowModal() == wx.ID_OK:
            pymotGUI.back_file = dialog.GetPath()
            self.back_label.SetLabel(pymotGUI.back_file)
 
    def run_finder(self, event):
        print pymotGUI.fore_file
        result = pymotif.calculate_motifs(pymotGUI.fore_file, pymotGUI.back_file)
        for motif in result:
            self.results.WriteText(motif + 'n')
        #wx.MessageBox('It should run, eh?')
 
#if __name__ == '__main__':
app = pymot()
frame = pymotGUI(parent=None, id = -1)
#frame.CentreOnScreen()
frame.Show()
app.MainLoop()
{% endcodeblock %}

and

{% codeblock lang:python %}
#!/usr/bin/env python
 
import fasta
import sys
from collections import defaultdict
 
def choose(n, k):
    if 0 <= k <= n:
        ntok = 1
        ktok = 1
        for t in xrange(1, min(k, n - k) + 1):
            ntok *= n
            ktok *= t
            n -= 1
        return ntok // ktok
    else:
        return 0
 
def get_quorums(seqs, mlen):
    """
    add seq id_no to a set
    use explicit counter to create seq_no
    """
    quorum = defaultdict(int)
    for seq in seqs:
        for n in range(len(seq) - mlen):
            quorum[seq[n:n + mlen]] += 1
    return quorum
 
def calculate_motifs(input_seqs, input_seqs2):
 
    print input_seqs, input_seqs2
    input_seqs = fasta.read_seqs(open(input_seqs).readlines())
    input_seqs2 = fasta.read_seqs(open(input_seqs2).readlines())
 
    foreground = get_quorums(input_seqs, 10)
    background = get_quorums(input_seqs2, 10)
 
    N = len(input_seqs) + len(input_seqs2)
 
    res_motifs = []
    for i in foreground:
        term1 = choose(background[i], foreground[i])
        term2 = choose((N - background[i]), len(input_seqs) - 1)
        term3 = choose(N, len(input_seqs))
        p = (float(term1) * float(term2)) / term3
        if 0 < p <= 0.0001:
            res_motifs.append(i + 't' + str(foreground[i]) + 't' + str(background[i]) + 't' + str(p))
 
    res_motifs.sort()
    return res_motifs
{% endcodeblock %}

On the next post, the last in the series, we will just check how to get the value from the width input box and wrap-up everything.