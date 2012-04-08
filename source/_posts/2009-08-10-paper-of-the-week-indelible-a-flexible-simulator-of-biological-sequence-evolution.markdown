---
date: '2009-08-10 10:09:40'
layout: post
slug: paper-of-the-week-indelible-a-flexible-simulator-of-biological-sequence-evolution
status: publish
title: 'Paper of the week: INDELible: A Flexible Simulator of Biological Sequence
  Evolution'
wordpress_id: '339'
categories:
- Science
tags:
- bioinformatics
- Computer simulation
---

[![ResearchBlogging.org](http://www.researchblogging.org/public/citation_icons/rb2_large_gray.png)](http://www.researchblogging.org)

The paper of this week touches a subject that I have been involved in the past: sequence simulation. INDELible, by Fletcher and Yang, is a program that is capable of simulating both DNA and amino acid sequences, and it seems to be the complete package to do so. It contains several substitution models and it can even simulate codon substitutions.

As the article mentions, the closest comparison to INDELible is DAWG, developed by Reed Cartwright, that seems to be faster. DAWG is a nice program and generates good simulations and has a very well designed code with strong models and quite reliable results. And that's what you want on a simulation program. You really want is a good implementation of the amino acid/nucleotide substitution pattern and a good model of indel simulation. It seems that INDELible has all of that, based on the publication (I haven't tested yet).

Sequence simulation is usually a fringe field (if there is such field) in bioinformatics and phylogenetics/evolution. We usually forget that the best alignment and [phylogenetic](http://en.wikipedia.org/wiki/Phylogenetics) reconstruction is basically the best estimate with the methods we have. There's no way to prove or test different alignment methods and programs without a solid _in silico_ simulation or a hand curated alignment. And I think the simulation is better and can generate much more input than meticulously curating a [sequence alignment](http://en.wikipedia.org/wiki/Sequence_alignment). Also, there is the need to test for phylogenetic reconstruction methods, and nothing better than good simulation packages that can mimic perfectly evolutionary phenomena.

I'm really looking forward to test INDELible and see what it is capable of. The only complaint that I have is that it uses yet another markup language as the control file. Why not use YAML or some other markup language? That would make usage more straightforward, but at least the authors provided a tutorial section on their website.


Fletcher, W., & Yang, Z. (2009). INDELible: A Flexible Simulator of Biological Sequence Evolution Molecular Biology and Evolution, 26 (8), 1879-1888 DOI: [10.1093/molbev/msp098](http://dx.doi.org/10.1093/molbev/msp098)







[![Reblog this post [with Zemanta]](http://img.zemanta.com/reblog_e.png?x-id=d1105486-b40d-4404-9c83-5461e9e2514c)](http://reblog.zemanta.com/zemified/d1105486-b40d-4404-9c83-5461e9e2514c/)
