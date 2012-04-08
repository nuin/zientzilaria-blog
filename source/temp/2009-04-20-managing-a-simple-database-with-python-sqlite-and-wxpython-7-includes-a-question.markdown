---
author: admin
date: '2009-04-20 12:21:59'
layout: post
slug: managing-a-simple-database-with-python-sqlite-and-wxpython-7-includes-a-question
status: publish
title: Managing a simple database with Python, SQLite and wxPython, 7 (includes a
  question)
wordpress_id: '279'
? ''
: - bioinformatics
  - Phase 2
  - python
  - SQLite
  - wxPython
  - wxPython
---

And we're back. After a couple of weeks of inactivity we will get back
to our small soap-opera pf Python, wxPython and SQLite. Continuing in
our database management code let's check two other functions that
changed since our first inception of the code. The first one is the
`insert_data` function that looks like this now [sourcecode
language='python']def insert\_data(self, values\_list, insert\_string):
'''inserts data in the database''' if sys.platform == 'darwin': (cursor,
database) = link\_db(self.db\_path) else: (cursor, database) =
link\_db() cursor.execute(insert\_string % self.table\_name,
values\_list) database.commit() database.close()[/sourcecode] Basically
no changes, apart from the obvious check for the current running
operating system, which was explained in the last post. The other
function to check is the `update_data`. This function is new and it
wasn't in the first version, but as it can be seen it has a problem
being a "generic" function, because it contains information pertained to
the table and database being used in the interface. This function
basically received information that needs to be updated in the table's
fields and by using the SQL `UPDATE ... SET` edits and updates data in
the changed fields. I have tried several different syntaxes to make the
execute generic, mainly trying to pre-format the string without success.
IF anyone reading this can help, I'd appreciate. [sourcecode
language='python']def update\_data(self, values\_list): '''edits and
updates fields''' if sys.platform == 'darwin': (cursor, database) =
link\_db(self.db\_path) else: (cursor, database) = link\_db()
cursor.execute("UPDATE bac SET projects = ?, comments = ?, temperature =
?, cell = ?, box = ?, tubes = ?, chromosome = ?, sdate = ?, clone = ?,
source = ?, location1 = ?, startpos = ?, endpos = ?, gene = ?, genelink
= ?, dnaex = ?, validation = ?, pcr = ?, refs = ?, antibiotic = ? WHERE
idbac = ?", values\_list['projects'], values\_list['comments'],
values\_list['temperature'], values\_list['cell'], values\_list['box'],
values\_list['tubes'], values\_list['chromo'], values\_list['date'],
values\_list['clone'], values\_list['source'], values\_list['location'],
values\_list['start'], values\_list['end'], values\_list['gene'],
values\_list['genelink'], values\_list['dna'],
values\_list['validation'], values\_list['pcr'], values\_list['refs'],
values\_list['antibiotic'], values\_list['idbac'])) database.commit()
database.close()[/sourcecode] Anyway, I will explain the logic of the
command (OK for a stop gap, but not as a definite solution).
`values_list` is a dictionary that is passed to the function and
contains the field names as keys and the new/changed information as
values. The execute method simply parses the values from each key in the
update string which is then sent to the database and table to be
changed. Everything is committed and the database is closed. As this is
a "generic" function from a "generic" class the ideal scenario would be
to the function to receive a pre-formatted string with all the
information, as in the insert data function, and update the information
in the database. I would like to thank in advance anyone that can
comment on this. Next time we will continue checking the generic class
and finalize this part in order to start with the interface build
process.\
\
 Previously in the series: [Part
1](http://python.genedrift.org/2009/02/09/managing-a-simple-database-with-python-sqlite-and-wxpython-1/)
[Part
2](http://python.genedrift.org/2009/02/17/managing-a-simple-database-with-python-sqlite-and-wxpython-2/)
[Part
3](http://python.genedrift.org/2009/02/18/managing-a-simple-database-with-python-sqlite-and-wxpython-3/)
[Part
4](http://python.genedrift.org/2009/03/02/managing-a-simple-database-with-python-sqlite-and-wxpython-4/)
[Part
5](http://python.genedrift.org/2009/03/02/managing-a-simple-database-with-python-sqlite-and-wxpython-5/)
[Part
6](http://python.genedrift.org/2009/03/31/managing-a-simple-database-with-python-sqlite-and-wxpython-6/)
[![Reblog this post [with
Zemanta]](http://img.zemanta.com/reblog_a.png?x-id=d0bb5d11-6f9d-8521-9a2f-6cd30868e375)](http://reblog.zemanta.com/zemified/d0bb5d11-6f9d-8521-9a2f-6cd30868e375/ "Reblog this post [with Zemanta]")
