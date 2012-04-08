---
author: admin
date: '2009-02-17 11:04:18'
layout: post
slug: managing-a-simple-database-with-python-sqlite-and-wxpython-2
status: publish
title: Managing a simple database with Python, SQLite and wxPython, 2
wordpress_id: '242'
? ''
: - bioinformatics
  - Database
  - Phase 2
  - Programming
  - python
  - SQL
  - SQLite
---

Let's continue coding our small Python + SQLite application. The initial
idea was to have a file for the interface and another file for the DB
access. We will start with the later. If you have access to the
repository you will see two Python files, `bac_form.py` and `db_obj.py`.
At the moment they are not well commented and have some junk lines at
the bottom, legacy from older versions. Take a look on `db_obj.py`. It
has two class declarations, one called `DB_Generic` and another one
called `Bac`. Remember in the last post where I mentioned that the idea
was to have different simple tables in the same SQLite database and each
table would have a simple input/output interface (If I didn't mention
that, I just did!). So, we can create a generic DB access class and we
can subtype from it for every table that we will be using. In the
`db_obj.py` file we have at the moment the generic database management
class, a class derived from the generic to access the Bac database and
an initialization function, that opens the access to the SQLite file.
Let's take a look at it: [sourcecode language='python']def link\_db():
'''initializes the database file''' try: db =
sqlite3.connect("samples.db") except sqlite3.Error, errmsg: print 'DB
not available ' + str(errmsg) sys.exit() db\_cursor = db.cursor() return
db\_cursor, db[/sourcecode] In order to access a SQLite database file we
need initially the name of the file. After importing sqlite3 (we're
using the latest version of SQLite here) Python has everything it needs
to access, change and manipulate data in a SQLite database. Just to be
sure the database file is there and we don't get an error, we have the
initialization code inside an exception. We have seen exceptions before
and in this case we use it to be sure the database file has been
accessed with no problems. The exception structure looks like
[sourcecode language='python']try: \#here we try to do something \#the
code placed here would be executed \#if no error reported it will go
until the end and exit \#if not, some error (exception) raised except:
\#the code under except will be executed[/sourcecode] So, the first step
is to connect to the database file [sourcecode language='python']db =
sqlite3.connect("samples.db")[/sourcecode] In our case it's a fixed
file, but the connect method receives any kind of string. It could have
been some parameter obtained from the command line or a string from a
configuration file. If the connect is successful, no error will be
raised and we are safe to continue. We connected to database, now what?
We need a cursor, an object that will actually access the data and allow
us to execute [SQL](http://en.wikipedia.org/wiki/SQL "SQL") commands on
it. [sourcecode language='python']db\_cursor = db.cursor()[/sourcecode]
`cursor` method works on the database connection object that we created
previously. We're set. This function returns the cursor and database
connection objects that we created, in a tuple and this function can be
called from the classes we are going to work. The classes will then have
connection to the database and a cursor that would manage, select,
delete and add data to it. Next time we'll see how our generic table
class works. Previously in the series: [Part
1](http://python.genedrift.org/2009/02/09/managing-a-simple-database-with-python-sqlite-and-wxpython-1/)
[![Reblog this post [with
Zemanta]](http://img.zemanta.com/reblog_e.png?x-id=cbbab23e-338a-4756-8f4c-25cc0a5239dc)](http://reblog.zemanta.com/zemified/cbbab23e-338a-4756-8f4c-25cc0a5239dc/ "Zemified by Zemanta")
