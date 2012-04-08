---
author: admin
date: '2010-04-08 20:59:54'
layout: post
slug: the-sickest-python-code-ive-ever-created-1
status: publish
title: The "sickest" Python code I've ever created 1
wordpress_id: '357'
? ''
: - Phase 2
---

But, I guess, it can be easily refactored/enhanced/despised by the
audience that read or have access to this blog via Planet Python.
Anyway, for someone like me, whose main task now is not to generate tons
of code and lines, I think the code (or part of it) that I will present
below is quite good. Feel free to comment, criticize and say bad and
good things about it. We needed a script that would take files coming
out from protein search engines that would be able to compare the
peptides and protein sequences, their abundance and some other
characteristics. We had a combination of protein and peptide files, with
a list of proteins (one protein per line in a tab delimited file) that
was related to a list of peptides in another file (one peptide per line,
with multiple peptides/lines related to one protein in the original
list). Also each line in both files had more than 50 columns, and 8 or
16 of them were the values we wanted to extract. I say 8 or 16 of them
because we didn't know how many will output each time, as it would
depend on the number of samples per run (4 to 8 samples) . So, we had a
couple of issues: we didn't know how many proteins would be output
(actually found) in each file, we wouldn't know how many peptides for
each protein would be found and we didn't know before hand how many
samples would be run at once. One good thing is that the 8-16 columns of
values were fixed, always in the same position and with empty cells if
no value was registered there. And we had a fourth problem: usually the
samples attributions would be random, meaning a control could come in
the first value column or could come in the last. And a fifth as we
didn't know before hand (the tech knew) how many treatments would be run
each time. A treatment could be a different experimental condition, a
sample grouping or some other extraneous factor. An extra issue is that
we would need to compare multiple files, and get protein and peptide
abundances in all of them at the same time and finally compare each
treatment. Basically, in order to create an universal script we needed
something flexible enough that whatever the experiments threw at use we
would be able to handle. First step we decided to use a YAML file that
could be filled by the experimental researchers with sample assignments,
treatments, etc. The YAML would look like this B0: - 114: A - 115: D -
116: B - 117: C B1: - 114: C - 115: A - 116: D - 117: B In this file B0
and B1 would be the result file names, 114 is the column/channel where
the sample was run and and A, B, C and D the treatment. With this set,
out objective was to get all proteins and their peptides for treatment A
in files B0 and B1, do some calculation and them compare to all proteins
and peptides from treatment B, C and D extracted also from files B0 and
B1. First step was to get the names of the treatments from the YAML file
[sourcecode language='python']]def get\_treatments(mapping): treats =
set([]) for entry in mapping: [treats.add(list(t.values())[0]) for t in
mapping[entry]] return treats[/sourcecode] where [code]mapping[/code] is
the YAML file name. We used a set to store and sets have unique items,
and treatment names can vary from file to file. In the code above we
basically read the YAML and the value for each entry. We then needed a
class to store protein information, and there was the story got hairy.
With all my (lack of ) experience, I decided to use [code]exec[/code]
statements to fix all the uncertainty of the experimental data details.
I didn't have the treatment names before hand (or in a fixed immutable
list), and didn't have the columns (channels) that were being used at
the time and I have to correctly assign each protein abundance (area) to
its place. In the end our class look like this [sourcecode
language='python']class Protein(): """Class Protein, stores all the
information about channels and areas, name and accession""" def
\_\_init\_\_(self, accession, name, treatments): self.accession =
accession self.name = name \#ratio channels are called based on their
name for i in treatments: exec('self.%s = []' %i) exec('self.area%s =
[]' %i) def add\_to\_channel(self, channel, peptide):
exec('self.%s.append(peptide)' % channel) def add\_to\_area(self,
channel, area): exec('self.area%s.append(area)' % channel)[/sourcecode]
In order to be faithful to this blog's name, I will explain how the code
above is supposed to work. First, [code]exec[/code] is a Python
statement that support dynamic execution of code. In our case above it
was used to name the objects, so we would be able to access them by name
in subsequent functions. Let's take this for example [sourcecode
language='python']for i in treatments: exec('self.%s = []' %i)
exec('self.area%s = []' %i)[/sourcecode] In this snippet we were trying
to create lists called (for the YAML file above) A, B, C and D, and
another set of lists called areaA, areaB, areaC and areaD. Let's say for
another experiment we would have treatments "Control", "Low" and "High"
and so on. The next two functions use the same approach, with exec, this
time appending to the freshly created lists. This way it's easy to
control what the user is throwing at us. I don'f know if this the best
approach possible, or if it is or not harmful. Maybe experts reading
this might have better ideas, and I appreciate them. We check the rest
of the script next time.
