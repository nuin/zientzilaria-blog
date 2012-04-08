---
date: '2007-10-20 00:41:26'
layout: post
slug: using-subversion-and-svn-time-lapse-to-edit-a-manuscript
status: publish
title: Using subversion and svn-time-lapse to edit a manuscript, take 1
wordpress_id: '50'
categories:
- Misc
---

Neil Saunders started the thread [here ](http://nsaunders.wordpress.com/2007/10/03/organise-your-bioinformatics-projects-using-subversion-and-trac-part-1/)and [here](http://nsaunders.wordpress.com/2007/10/05/organise-your-bioinformatics-projects-using-subversion-and-trac-part-2/) of using subversion to maintain your files, projects and general stuff. Myself, I find trac a little bit clumsy to check differences between two versions. It is easy to see what has been changed but if the modifications are large it gets a little bit tedious to scroll down and search everything. An example is below.

[![Example of file comparison in trac (2 versions, Python)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/trac_example.thumbnail.png)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/trac_example.png) 

Enters [svn-time-lapse](http://jonaquino.blogspot.com/2007/10/svn-time-lapse-view.html), which seems to be a very interesting tool to compare two versions of a file. I decided to test it on a manuscript edition. I first created a a repository on my Desktop and added an old LaTex file. I replaced this file with a different version of the article (1 or 2 revisions ahead) and opened the repository with svn-time-lapse. The program instantly highlights the portions of the article that are different and display both side by side. One advantage is that svn-time-lapse already gets a certain number of revisions from the repository that can be compared to the current file. A scroll on the top gives an extra help moving from one revision to another.

[![svn-time-lapse example](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn_time_lapse_example.thumbnail.png)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn_time_lapse_example.png)

The program is available from the developer's website, Jon Aquino, and from Google Code. The release still needs some polishing but it is stable enough to be used extensively.





