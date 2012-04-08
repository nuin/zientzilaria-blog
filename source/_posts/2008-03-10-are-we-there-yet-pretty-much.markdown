---
date: '2008-03-10 15:22:56'
layout: post
slug: are-we-there-yet-pretty-much
status: publish
title: Are we there yet? Pretty much.
wordpress_id: '114'
categories:
- Bioinformatics - opinion
---

[![ResearchBlogging.org](http://www.researchblogging.org/images/rbicons/ResearchBlogging-Medium-White.png)](http://www.researchblogging.org)

Are We There Yet it is a simple web application to explore graphically convergence in Markov Chain Monte Carlo in Bayesian phylogenetic inference. The website name comes from one of the most important factors in Bayesian phylogenetic inference, that is the convergence of branch lengths and splits. Usually a linear plot of likelihood scores is used to define convergence (a plateau in the graph) where supposedly the variables in the estimation reached a "convergent" status. But as pointed in AWTY original article this method can incur in assessment errors of such convergence and because of this they developed the web application. 

AWTY is pretty simple interface, the simple here being a compliment. No frills and easy to use. Basically the whole process can be summarized by:

upload tree file(s) -> select analysis type -> click Plot -> check result

The application is nothing more than a wrapper to [GnuPlot](http://www.gnuplot.info/) and in some cases [PAUP](http://paup.csit.fsu.edu). A nice touch is that everything created in the site is logged and all commands used on the background GnuPlot are also output and linked, so if you don't like the graph created by AWTY you can run your own. No complete help is available but the simplicity of the interface makes it very user friendly. Each of the nine methods have short explanatory texts in order to guide the user on parameter selection and/or the number of required file(s) for the analysis.

One change that I would make is to include the possibility of uploading more than one file at once. But apart of that AWTY is a very nice application and should be very useful for exploratory Bayesian phylogenetic inference.

_Tested on Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.8.1.12) Gecko/20080201 Firefox/2.0.0.12_




Nylander, J.A., Wilgenbusch, J.C., Warren, D.L., Swofford, D.L. (2007). AWTY (are we there yet?): a system for graphical exploration of MCMC convergence in Bayesian phylogenetics. Bioinformatics, 24(4), 581-583. DOI: [10.1093/bioinformatics/btm388](http://dx.doi.org/10.1093/bioinformatics/btm388)
