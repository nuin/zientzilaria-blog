---
author: admin
date: '2009-03-31 12:06:08'
layout: post
slug: managing-a-simple-database-with-python-sqlite-and-wxpython-6
status: publish
title: Managing a simple database with Python, SQLite and wxPython, 6
wordpress_id: '276'
? ''
: - bioinformatics
  - Phase 2
  - python
  - SQLite
  - wxPython
  - wxPython
---

[![The :en:SQLite logo as of
2007-12-15](http://upload.wikimedia.org/wikipedia/commons/thumb/1/19/SQLite_Logo_4.png/202px-SQLite_Logo_4.png "The :en:SQLite logo as of 2007-12-15")](http://commons.wikipedia.org/wiki/Image:SQLite_Logo_4.png)
  ~ Image via
    [Wikipedia](http://commons.wikipedia.org/wiki/Image:SQLite_Logo_4.png)

Let's get back to our SQLite and wxPython project. We haven't seen
anything on wxPython yet, and we will check the interface only on the
next post. For now, let's see some extra code added to the SQLite access
class. Remember that we have a generic class and one class derived from
it that would work on accessing specific tables in our database file.
When we last covered the db access routines, there was no search for an
entry (the function returned everything in the table no matter what),
there was no update function in case someone would want to modify an
entry and there was no delete method if you wanted to delete something.
In the meantime, I added all of this functionality (and some other) to
the generic class and extended it to the class derived from it. Let's
check how the generic class is now (you will notice that there is an
issue in one of the methods, if someone can help me I'd appreciate. More
details later.) [sourcecode language='python']class DB\_Generic():
'''generic class to add DB functionality''' def \_\_init\_\_(self,
table\_name, db\_path = ''): \#par= name of the table to be used
self.table\_name = table\_name if len(db\_path) \> 0: self.db\_path =
db\_path print db\_path def get\_data\_generic(self, range = 1,
bac\_to\_get = 0): '''gets the data from the database''' if sys.platform
== 'darwin': (cursor, database) = link\_db(self.db\_path) else: (cursor,
database) = link\_db() if range == 1: cursor.execute("""SELECT \* FROM
%s""" % self.table\_name) elif range == 2: cursor.execute("""SELECT \*
FROM %s where idbac = %d""" % (self.table\_name, bac\_to\_get))
table\_data = cursor.fetchall() raw\_data = [] for i in table\_data:
raw\_data.append(list(i)) self.table\_data = raw\_data database.close()
def insert\_data(self, values\_list, insert\_string): '''inserts data in
the database''' if sys.platform == 'darwin': (cursor, database) =
link\_db(self.db\_path) else: (cursor, database) = link\_db()
cursor.execute(insert\_string % self.table\_name, values\_list)
database.commit() database.close() def update\_data(self, values\_list):
'''edits and updates fields''' if sys.platform == 'darwin': (cursor,
database) = link\_db(self.db\_path) else: (cursor, database) =
link\_db() \#change this to generic!!!!!!!!!!!! cursor.execute("UPDATE
bac SET projects = ?, comments = ?, temperature = ?, cell = ?, box = ?,
tubes = ?, chromosome = ?, sdate = ?, clone = ?, source = ?, location1 =
?, startpos = ?, endpos = ?, gene = ?, genelink = ?, dnaex = ?,
validation = ?, pcr = ?, refs = ?, antibiotic = ? WHERE idbac = ?",
(values\_list['projects'], values\_list['comments'],
values\_list['temperature'], values\_list['cell'], values\_list['box'],
values\_list['tubes'], values\_list['chromo'], values\_list['date'],
values\_list['clone'], values\_list['source'], values\_list['location'],
values\_list['start'], values\_list['end'], values\_list['gene'],
values\_list['genelink'], values\_list['dna'],
values\_list['validation'], values\_list['pcr'], values\_list['refs'],
values\_list['antibiotic'], values\_list['idbac'])) database.commit()
database.close() def delete\_data(self, delete\_string): '''deletes one
field''' if sys.platform == 'darwin': (cursor, database) =
link\_db(self.db\_path) else: (cursor, database) = link\_db()
cursor.execute(delete\_string) database.commit()
database.close()[/sourcecode] In the next couple of posts we'll dissect
each function and see what's going on. The class definition wasn't
changed, so we start with `get_data_generic` [sourcecode
language='python']def get\_data\_generic(self, range = 1, bac\_to\_get =
0): '''gets the data from the database''' if sys.platform == 'darwin':
(cursor, database) = link\_db(self.db\_path) else: (cursor, database) =
link\_db() if range == 1: cursor.execute("""SELECT \* FROM %s""" %
self.table\_name) elif range == 2: cursor.execute("""SELECT \* FROM %s
where idbac = %d""" % (self.table\_name, bac\_to\_get)) table\_data =
cursor.fetchall() raw\_data = [] for i in table\_data:
raw\_data.append(list(i)) self.table\_data = raw\_data
database.close()[/sourcecode] The first difference we notice here is the
`sys.platform` usage. This is required if we intend to package our
application as an OS X app, using py2app. When a Python/wxPython
application is packaged in OS X, the actual application executable is
inside the a directory named after the application (or whatever you set
up). In our case here we don't provide a way for the Python script to
receive the path and name for the database on a command line, as we
expect it to be in the executable's current directory. Because of that
we need to provide a "config" file (in our case here a one-line text
file with the database path) inside the application wrapper, something
we will see in the end of the series. Another modification here is the
`range` parameter and the addition of the `bac_to_get` parameter. Notice
that both parameters have a value assigned to it. This means that they
are optional, the function's call can pass them or not. If it doesn't
pass, their value will be the one assigned on the function declaration.
So, here if we are interested in getting all bacs, `range` will have the
value of 1 and we don't need to worry about it. If we want an specific
bac we will pass `range` as 2 and then pass the `bac_to_get` ID to be
returned. A final change/addition is that we added a new select
statement for the cases when `range` equals 2. This time we are adding
the bac ID to be returned. Previously in the series: [Part
1](http://python.genedrift.org/2009/02/09/managing-a-simple-database-with-python-sqlite-and-wxpython-1/)
[Part
2](http://python.genedrift.org/2009/02/17/managing-a-simple-database-with-python-sqlite-and-wxpython-2/)
[Part
3](http://python.genedrift.org/2009/02/18/managing-a-simple-database-with-python-sqlite-and-wxpython-3/)
[Part
4](http://python.genedrift.org/2009/03/02/managing-a-simple-database-with-python-sqlite-and-wxpython-4/)
[Part
5](http://python.genedrift.org/2009/03/02/managing-a-simple-database-with-python-sqlite-and-wxpython-5/)

[![Reblog this post [with
Zemanta]](http://img.zemanta.com/reblog_a.png?x-id=ea53b728-33c6-47db-aabf-0c695dcfabd8)](http://reblog.zemanta.com/zemified/ea53b728-33c6-47db-aabf-0c695dcfabd8/ "Zemified by Zemanta")
