---
date: '2007-10-24 22:25:26'
layout: post
slug: using-subversion-and-svn-time-lapse-to-edit-a-manuscript-take-2-a-short-tutorial
status: publish
title: Using subversion and svn-time-lapse to edit a manuscript, take 2, a short tutorial
  - PART I
wordpress_id: '53'
categories:
- Misc
- Science
---

Last post I introduced svn-time-lapse, which is already in [version 1.3](http://svn-time-lapse-view.googlecode.com/files/svn-time-lapse-view-1.3.zip). Jon included the option to view only the changes what I think might be an extra advantage when you are editing a manuscript. I outline here a small tutorial on how to edit a manuscript with subversion and svn-time-lapse. This is based on a Windows system, but it can be used with small changes for Linux, which has the advantage of having (most of the time) subversion installed.

(Be aware that this won't work for Word files, you need to be using a text based, ie Latex, document)

First you need to [download ](http://tortoisesvn.net/downloads)and install the TortoiseSVN interface for Windows. After installing it, the Windows Explorer right-click menu will have some extra options, as can be seen on the figure below.

[![svn1.png](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn1.png)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn1.png)

Checkout allows you to get the source from a repository, while TortoiseSVN gives a list of features to use with subversion. Now, we need to create a directory where the manuscript repository is going to reside. You can create the repository in any place, online, locally, etc. But if you don't have an online place to create it, I suggest to create underneath a Documents type of location. On Windows you can create a new folder inside the (My) Documents directory. So, make the new folder **manuscript**. [![svn2.png](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn2.png)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn2.png)

and the right-click on it and navigate to **TortoiseSVN>>Create repository here**. You can select either format. Done, your repository is set.

**SVN**[![svn3.png](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn3.png)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn3.png)

If you open the manuscript directory you will see different files, but of course it is empty of actual content. You need to add some content to it and the ideal way is to check out (create a copy for edition) the repository in another location, drop files into this copy and add them to the version control. 

[![svn4.png](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn4.png)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn4.png)

You created the repository in your "Documents" directory, so you can check out it to your Desktop (or to any location). This will be your "local" copy of the manuscript, the one that you will work on. Close all open windows and right click on your desktop and select **SVN Checkout** from the popup menu.

[![svn5.png](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn5.png)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn5.png)


In the dialog that appear enter the location of the repository (in your "Documents" dir) and the location where you want to checkout to (your "Desktop" location), just like the figure below.

[![svn6.png](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn6.png)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn6.png)

Click OK and a "local" copy of the repository will be created.

[![svn7.png](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn7.png)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2007/10/svn7.png)

To be continued.
