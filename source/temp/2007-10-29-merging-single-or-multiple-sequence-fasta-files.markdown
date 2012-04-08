---
author: admin
date: '2007-10-29 15:17:02'
layout: post
slug: merging-single-or-multiple-sequence-fasta-files
status: publish
title: Merging single (or multiple) sequence FASTA files
wordpress_id: '67'
? ''
: - Phase 2
---

Last couple of entries we saw how to split a multiple FASTA file. And
how can we achieve the opposite, merge single (or sometimes multiples)
sequence files in on larger multiple sequence file? In Python is very
simple, but we need to introduce a new module that would allow us to get
the desired result. In most scripts we have seen in previous posts, we
end up reading a single file from the input (in some cases two) and
that's not enough in the case of merging multiple files. Python has a
module called `glob` that is very powerful for reading contents of a
directory. We can use any type of pattern matching to find only the
files we want, wildcards allowed. Let's test glob and see what we can
get. We start with a simple script [sourcecode language='python']import
glob for i in glob.glob('\*.txt'): print i[/sourcecode] If we run this
script in a directory (Windows or Linux or Mac) we should see a list of
the filenames that match the patter passed to glob.glob. In this case
every file with a txt extension. This should be enough for us, for now.
Basically we need to create a list of all FASTA files, that match a
certain name pattern, and then take care of the sequences using our
already known FASTA module. To make things more flexible, we should ask
in the command line for a pattern to match, and maybe a output filename.
Our script would look like [sourcecode language='python']import sys
import glob import fasta filepattern = sys.argv[1] output =
open(sys.argv[2], 'w') \#initialize lists names = [] seqs = []
\#glob.glob returns a list of files that match the pattern for file in
glob.glob(filepattern): \#we read the contents and an instance of the
class is returned contents = fasta.read\_fasta(open(file).readlines())
\#a file can contain more than one sequence so we read them in a loop
for item in contents: names.append(item.name) seqs.append(item.sequence)
\#we print the output for i in range(len(names)): output.write(names[i]
+ '\\n' + seqs[i] + '\\n\\n') output.close()[/sourcecode] Except for the
glob part, we've already seen the rest in previous entries. Here, the
input `filepattern` should be enclosed in single or double quotes in
order to be transmitted properly (for instance when you include
wildcards). In the first `for` loop we access the list of files created
by `glob.glob` and extract the sequence name(s) and sequence(s) from
each file and parse them to a list which will serve to print the final
output. An example command line would look like
`python merge.py '*.fas' merged.fa` Of course, there are several ways of
merging FASTA files, but not everytime you have Linux's `cat` available.
Next time we will (try) to have fun with Python functional programming.
Stay tuned.
