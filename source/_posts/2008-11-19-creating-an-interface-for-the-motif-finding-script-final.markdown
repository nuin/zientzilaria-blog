---
author: admin
date: '2008-11-19 16:57:24'
layout: post
slug: creating-an-interface-for-the-motif-finding-script-final
status: publish
title: Creating an interface for the motif finding script, final
wordpress_id: '201'
? ''
: - bioinformatics
  - GUI
  - motifs
  - motifs
  - python
  - wxPython
  - wxPython
---

We can say that this would be our final version of the script. There are
many nice wxPython programming resources, and one is a very good book
called [wxPython in Action](http://manning.com/rappin/), which is
co-written by Robin Dunn, the wxPython maintainer. Go check it out. 


So for the last entry in this series, we just need to add a couple of
changes to our interface and motif finding scripts. Basically on the
interface script we need to add a line that gets the value entered (or
the default one, if not changed) in the motif width input box. And we
can do that by including the line below in the `run_finder` function.

{% codeblock lang:python %}
width = self.motif\_width.GetValue()
{% endcodeblock %}

This line tells the script to
get the value of the box and assign to the variable width. This method
will get whatever is inside the input box and save as a string to the
variable assigned. Now, we need to create the structure to actually send
this value to the motif finder functions. Last version of our function
`calculate_motifs` received two parameters, we need to add an extra one,
and also change the lines that call the function that get the quorums.
Basically the first lines of the function will be 

{% codeblock lang:python %}
def calculate_motifs(input_seqs, input_seqs2, width):
 
    print input_seqs, input_seqs2
    input_seqs = fasta.read_seqs(open(input_seqs).readlines())
    input_seqs2 = fasta.read_seqs(open(input_seqs2).readlines())
 
    foreground = get_quorums(input_seqs, width)
    background = get_quorums(input_seqs2, width)
{% endcodeblock %}


And that's it. Our simple interface is ready to
primetime. OK, not prime primetime, we didn't add a series of features
that will make it useful by everyone. For instance, there is no error
control, so someone could enter 'ABC' in the width input box and that
value would be sent and an error will occur. Also you can click the run
button without any file selected. And we could go on and on. But this is
just a primer, and we can build from it. The code is on
[Github](http://github.com/nuin/beginning-python-for-bioinformatics/tree/master/scripts/motifs),
so get it there and have fun. Next time we will see ... no plans yet. We'll see ... 
