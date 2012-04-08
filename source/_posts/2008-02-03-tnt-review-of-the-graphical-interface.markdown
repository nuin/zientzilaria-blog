---
date: '2008-02-03 12:27:27'
layout: post
slug: tnt-review-of-the-graphical-interface
status: publish
title: 'TNT: review of the graphical interface'
wordpress_id: '90'
categories:
- Bioinformatics - opinion
- Science
---

This time I am writing about the Windows version of TNT which is somewhat graphical. I am currently using Windows Vista Home Premium.

**Interface**

TNT's interface is far from being stylish, and it is quite simple and intuitive. Most of the options you would need to calculate trees and modify your analysis are on a toolbar and on menus at the top. 

[![Toolbar](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2008/01/tnt1.png)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2008/01/tnt1.png)

The main area is occupied by a log/text area where the current actions/selections are displayed from time to time. The default font is clear and large and there are ways to format it as you wish. You also have buttons that allow you to increase or decrease the font size.

**Running TNT**

Running the program with the interface was clearly more pleasant than using the cryptic command line version. TNT starts with an blank area, toolbar and menu, as an usual Windows application. I decided to open one of the three example files that come with it, zilla.tnt.

First thing would be to obtain the tree, and intuitively I ended up pressing the button the toolbar with the man running. Bingo, that's what I needed. TNT, then, showed me a options dialog.


[![tnt2.png](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2008/01/tnt2.thumbnail.png)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2008/01/tnt2.png)

This makes life much easier. All options for tree calculation were right in front of me, and I even had access to specific settings for each method. Then I could see the full range of features that TNT offers. I set to run with default parameters adding the ability to use the ratchet. The run went smoothly, quite fast and an informative progrss dialog displayed the status. (One thing though: TNT developers have created some of the dialogs without a frame or border, what makes impossible to move then around. Sometimes they got in the way of information displayed on the log that might have been important to set the runs).

After the calculation ended, TNT told me that 4 trees were retained from my run. So I wanted to check the trees, not that I was worried if my analysis was right or wrong. One fault was evident: tool bar buttons don't have a tooltip and this made a little bit difficult to understand some of the buttons' pictures. The one to create a consensus is pretty clear, as the one to trash all trees obtained. So I decided to check the menu.

As in any normal Windows program TNT's menu is richer in options than the tool bar for obvious reasons. I went to the Trees menu and selected View. All four trees were then displayed on the screen with a scrollbar on the side, much better than the command line version. There is an option that allows the user to collapse the branches, but in my opinion it still a little bit awkward. You have first to unlock the tree and then the program allows you to "shrink" nodes. One click at a node adds a red spot to it, another puts a green spot, and a double-click "shrinks" the node.

There are some errors on some tree display options. For instance, when the consensus button is clicked it brings up a dialog to change the calculation and after you click OK, TNT generates the consensus and automatically displays a tree. But the window containing the tree is larger than my desktop, has no scrollbar and cannot be dragged. I don't know if this an error, a bug or an incompatibility of TNT with Vista. The only way to exit is by using ESC. I will try on XP and update the review.


[TNT displaying a consensus tree (full screen capture)](http://blindscientist.genedrift.org/wordpress/wp-content/uploads/2008/02/tnt3.png)

**Conclusions**

TNT seems to be a powerful software for phylogenetic analysis if you are looking mainly for parsimony. Also, its algorithms seems to have inherited the best of Hennig86. The graphic interface, even though not groundbreaking by any means, makes its use very easy. The program is fast, has many different options for parsimony tree calculation and it is an excellent option for determination of trees to be used as input for slower methods, as pointed out in one of the comments of the CLI review. There are still some errors and bugs and some features I would change in its GUI, but that's true for most of the software available in any field. 


_**Update: another review is available [here](http://blindscientist.genedrift.org/2008/01/30/tnt-a-comprehensive-review/).**_
