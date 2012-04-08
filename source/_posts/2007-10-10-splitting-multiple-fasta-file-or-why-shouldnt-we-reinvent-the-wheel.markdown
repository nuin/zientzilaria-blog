---
author: admin
date: '2007-10-10 12:04:59'
layout: post
slug: splitting-multiple-fasta-file-or-why-shouldnt-we-reinvent-the-wheel
status: publish
title: Splitting multiple FASTA file, or why shouldn't we reinvent the wheel?
wordpress_id: '62'
? ''
: - fasta
  - Phase 2
  - split
---

[Daniel Swan](eridanus.net/blog) posted a comment on the previous entry
regarding that splitting multiple sequence FASTA files is "one of those
‘bioinformatics’ tasks where people are seriously guilty of reinventing
the wheel". 

Biologically, let's dissect his comment. As there are not
many comments in this blog, we take advantage of the few ones posted. I
don't disagree with the fact that many applications in Bioinformatics
are reinventing the wheel, but at the same time this blog is not to
teach anyone advanced bioinformatics development. Here, we deal with
Python and I try to use real life examples to show how powerful (or not,
depends on your point of view) Python is.The splitting FASTA example is
not the first one that "reinvents the wheel".

Who needs a new GenBank parser? Or a restriction site finder? Or a new class to read FASTA file?
Basically who needs Python if we can do everything else with Perl, C++?
What the heck, let's just learn Assembler. Diversity, that's the first
rule here. Perl mongers usually say that are many ways to do the same
thing, and that's very close to the truth. What would be of blue if
everyone liked green? At the same time he presents us with an
alternative for the job which is "‘csplit’" and this "should probably be
your first port of call for context based splitting of files!". Yes, I
know csplit. 

I also know dozens of other methods (see next post) to do
same thing. But maybe he didn't notice the title of the site: Beginning
**Python** for Bioinformatics. If the main reason of the blog was to
show \*nix commands I would have titled it Beginning \*nix Commands for
Bioinformatics. We also learn from his comment that csplit is "far more
widely applicable than for just this example." 

I know in bioinformatics
we are in a microuniverse with its own idiosyncrasies. Because we live
in this bioinfo universe we might think that every other person in the
world has immediate access to a \*nix terminal. Biologists *don't use*
Windows. Because of that, I cannot disagree more that csplit is far more
widely applicable than any other method. Again, diversity. Not every
system is equal, not every solution is widely applicable. And lastly, he
tells us "Remember - if it seems like a logical operation and you are in
the ‘why hasn’t anyone made a utility to do this?’ frame of mind - look
around because they probably have!". Oh, I look around. And I see the
diversity of systems, applications, programming languages. I even see
diversity among biologists and bioinformaticians. 

Again, what I try to
emphasize with this post is diversity. Since the beginning my main focus
was to show a Pythonistic view of basic bioinformatics development. I am
probably reinventing the wheel every week, in every post. For the ones
that are learning Python or bioinformatics, it is a seed. For those that
are already established bioinformaticians, it might be a new option on
how to accomplish things. Diversity is the key. Out there is evolve or
perish. In (bio)informatics that's also true.
