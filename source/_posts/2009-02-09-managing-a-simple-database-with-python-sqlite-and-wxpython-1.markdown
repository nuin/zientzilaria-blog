---
author: admin
date: '2009-02-09 15:11:57'
layout: post
slug: managing-a-simple-database-with-python-sqlite-and-wxpython-1
status: publish
title: Managing a simple database with Python, SQLite and wxPython, 1
wordpress_id: '238'
? ''
: - Graphical user interface
  - Phase 2
  - python
  - SQLite
---

[![The official wxPython
logo](http://upload.wikimedia.org/wikipedia/commons/thumb/c/c0/WxPython-logo.png/202px-WxPython-logo.png "The official wxPython logo")](http://commons.wikipedia.org/wiki/Image:WxPython-logo.png)
  ~ Image via
    [Wikipedia](http://commons.wikipedia.org/wiki/Image:WxPython-logo.png)

A little break from reviewing the book, let's check some database topics
in Python. I was asked to create a simple database to organize wet-lab
stuff. No relationships needs, no relational tables required. Just a
simple table with determined columns, and a nice GUI to go with it so
people can edit, search and use. My first idea was to use SQLite
database, and I stuck with it. After the initial phase of "interviews"
to check database requirements, I ended up with a list of tables and
decided to start working on the table that organizes the BACs used in
the lab. BAC is a DNA vector into which large DNA fragments can be
inserted and cloned in a bacterial host, and are used mainly in
cytogenetics around here. In the end the table had this structure
[sourcecode language='sql']CREATE TABLE bac (idbac INTEGER PRIMARY KEY,
clone Text, sdate Date, source Text, gene TEXT, chromosome Text,
startpos Integer, endpos Integer, antibiotic Text, location1 Text,
temperature Integer, tubes Integer, box Integer, cell Integer, dnaex
Boolean, validation Boolean, pcr Boolean, projects Text, comments Text,
genelink Text, refs Text);[/sourcecode] I won't explain in detail each
of the fields, but we can see that there is a mix of different types.
SQLite doesn't allow many different field types, so we stick to the
basics. And why SQLite? The module to access it comes with Python 2.5,
the whole database is stored in one file that can be moved around and it
allows a full SQL query language, which is perfect for these simple
cases. So we will going to use Python, SQLite and wxPython to create a
simple application to manage our simple database. I already created a
GitHub
[repository](http://github.com/nuin/python_sqlite_wxpython/tree/master)
for the upcoming code.

[![Reblog this post [with
Zemanta]](http://img.zemanta.com/reblog_e.png?x-id=1a2359cd-d9c7-4cee-a26b-c41b281ec3d2)](http://reblog.zemanta.com/zemified/1a2359cd-d9c7-4cee-a26b-c41b281ec3d2/ "Zemified by Zemanta")
