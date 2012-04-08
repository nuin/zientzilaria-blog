---
author: admin
date: '2009-03-02 19:23:42'
layout: post
slug: managing-a-simple-database-with-python-sqlite-and-wxpython-5
status: publish
title: Managing a simple database with Python, SQLite and wxPython, 5
wordpress_id: '253'
? ''
: - bioinformatics
  - Database
  - Phase 2
  - python
  - SQLite
  - wxPython
  - wxPython
---

We have seen how to connect, get and insert data (at least
theoretically) in the database. Now, a little not about the SQL engine
of choice here: SQLite. SQLite databases have the main characteristic
that they are self-contained files. Also it does not require an
installation, works without a server and works pretty well in most
operating systems. Basically for the type of application we're
developing here, SQLite seems ideal. It eliminates a lot of
infrastructure that would be needed if we were working with MySQL or
postgresql. We don't need a server or know how to configure users or
manage the databases and tables. All we need is contained in a single
file that can be transported from system to system and can be accesed
from the computers used in the lab, mainly XP and OS X. Also some web
frameworks (Rails and
[Django](http://www.djangoproject.com "Django (web framework)"), for
instance) can use SQLite, so in the end we can have a desktop
application and a web application accessing the same file without extra
configuration. Now the database created for this application has 8
tables and almost no relationships among them. SQLite allows the
creation of relationships but in our case only a couple of cases were
required. For the table we are using at the moment (bac) there is no
need for relationships, although there are some fileds that can benefit
from a more relational structure. Also SQLite don't have the same data
types that are found on the bigger SQL engines. All values can be stored
as text, integer, real (floating point numbers), null and blob (verbose
type, what you store is what you get). As actual types, you can set
columns as Boolean and Data for instance and SQLite will understand
them. If you have no experience in creating databases, let's check again
the table we are using in this small project. First, I would recommend
the use of some SQLite database editor. You can find pretty good ones
for any computer system and there is even a Firefox extension that
allows you to edit some files. Editors make it easier to generate the
SQL table creation scripts and make easier to visualize what we are
doing. So, the table bac looks like [sourcecode language='sql']CREATE
TABLE bac (idbac INTEGER PRIMARY KEY, clone Text, sdate Date, source
Text, gene Text, chromosome Text, startpos Integer, endpos Integer,
antibiotic Text, location1 Text, temperature Integer, tubes Integer, box
Integer, cell Integer, dnaex Boolean, validation Boolean, pcr Boolean,
projects Text, comments Text, genelink Text, refs Text);[/sourcecode] If
you go back to our last post, you will see that in the insert statement
there is no mention of the `idbac` field. We don't actually insert ay
value there, the values that populate this field are created
automatically. And `idbac` is our primary key, meaning it's the unique
identifier of each bac we insert in this table. And in SQLite a integer
primary key is automatically incremented whenever values are inserted in
the table. So our first insertion will create `idbac` 1, the second will
create `idbac` 2 and so on. I'm not going to enter in details about
database development and administration, but it's usual and safe to
create tables with an auto-incremental integer primary keys. These
fields, apart from make it easier t identify records, make access to
such records faster and are great when relationships among tables are
set. Let's say that we had a column user in our bac table. And let's say
we had an user table with two columns: user\_id and name, user\_id being
a auto-increment primary key. The user column in back could be linked
with the user\_id column in the user table, in what we call a
one-to-many relationship (one user can insert as many bacs as he wants).
One day we want to know who is actually working in the lab and we want
to check how many bacs were catalogued by each user. We can easily
search the user table and extract information from bacs at the same time
thanks to the relationship between the tables. And the result should be
returned quite quickly, as we are only searching integers. All the other
fields/columns in our table are straightforward to understand. They are
basically related to the type of data they need to store. `validation`
is a boolean because the bac might have been validated or not, just as
`danex` (DNA extraction). At the same time, the number of tubes stored
in the freezer will always be an integer. So, why does temperature is an
integer? Because we can only store bacs in two type of freezers: -80
(ultra freezers) or -20 (regular freezer that we can have at home), and
we don't need to worry about fractional numbers. Well, this is a very
short and limited explanation of tables and SQLite. The web is full of
resources about it, so next time we will get back to Python. Previously
in the series: [Part
1](http://python.genedrift.org/2009/02/09/managing-a-simple-database-with-python-sqlite-and-wxpython-1/)
[Part
2](http://python.genedrift.org/2009/02/17/managing-a-simple-database-with-python-sqlite-and-wxpython-2/)
[Part
3](http://python.genedrift.org/2009/02/18/managing-a-simple-database-with-python-sqlite-and-wxpython-3/)
[Part
4](http://python.genedrift.org/2009/03/02/managing-a-simple-database-with-python-sqlite-and-wxpython-4/)
[![Reblog this post [with
Zemanta]](http://img.zemanta.com/reblog_e.png?x-id=4be1389f-5603-4b76-961b-b79d985066cc)](http://reblog.zemanta.com/zemified/4be1389f-5603-4b76-961b-b79d985066cc/ "Zemified by Zemanta")
