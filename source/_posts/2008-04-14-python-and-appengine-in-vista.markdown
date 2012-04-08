---
date: '2008-04-14 08:55:54'
layout: post
slug: python-and-appengine-in-vista
status: publish
title: Python and AppEngine in Vista
wordpress_id: '124'
categories:
- Bioinformatics - opinion
tags:
- appengine
- msiexec
- python
- vista
---

I had problems installing Google's AppEngine in Vista. I had Python 2.5.1 installed in my machine but every time I tried to install the msi package it failed, claiming that Python was not present, even though C:\Python25 was in the path. AppEngine issues site did not help much either, the "solution" listed there was to make sure Python was in the path.

So, I decided to start over. I removed Python (and ActiveState Python, which I installed before to see if AppEngine would work) and re-installed it, or tried to. Strangely, Python's msi package was installing it in the C drive root, not under Python25. For half an hour I tested all possible combinations, versions and tricks to have it installed in the proper directory/folder. Then I remembered [msiexec](http://technet2.microsoft.com/windowsserver/en/library/9361d377-9011-4e21-8011-db371fa220ba1033.mspx?mfr=true), a command line tool that runs msi packages. Running msiexec with no parameters shows a window with options, but basically `/i` is the the only required. `/i` tells msiexec the input package, while 'code>/qb` make the installation quiet and with a basic interface. msiexec worked flawlessly and then Python was in its right place. 

`msiexec /i python-2.5.2.msi TARGETDIR="C:\Python25" /qb`

Then the same "trick" was used with AppEngine, but without a TARGETDIR. Bingo, it installed perfectly (I am assuming that). 

Now, I just have to wait for my AppEngine account.
