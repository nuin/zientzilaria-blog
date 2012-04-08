---
author: admin
date: '2009-04-22 10:04:17'
layout: post
slug: managing-a-simple-database-with-python-sqlite-and-wxpython-8
status: publish
title: Managing a simple database with Python, SQLite and wxPython, 8
wordpress_id: '282'
? ''
: - bioinformatics
  - Phase 2
  - python
  - SQLite
  - wxPython
  - wxPython
---

[![Diagram of the location of introns and exons
w...](http://upload.wikimedia.org/wikipedia/commons/thumb/0/07/Gene.png/200px-Gene.png "Diagram of the location of introns and exons w...")](http://commons.wikipedia.org/wiki/Image:Gene.png)
  ~ Image via
    [Wikipedia](http://commons.wikipedia.org/wiki/Image:Gene.png)

Thanks to the comments and suggestions to the last post, it's possible
to make now a more pythonic and clearly generic database update class.
Let's check how the "generic" update/edit entry function is currently:
[sourcecode language='python']def update\_data(self, values\_list):
'''edits and updates fields''' if sys.platform == 'darwin': (cursor,
database) = link\_db(self.db\_path) else: (cursor, database) =
link\_db() cursor.execute("UPDATE bac SET projects = ?, comments = ?,
temperature = ?, cell = ?, box = ?, tubes = ?, chromosome = ?, sdate =
?, clone = ?, source = ?, location1 = ?, startpos = ?, endpos = ?, gene
= ?, genelink = ?, dnaex = ?, validation = ?, pcr = ?, refs = ?,
antibiotic = ? WHERE idbac = ?", values\_list['projects'],
values\_list['comments'], values\_list['temperature'],
values\_list['cell'], values\_list['box'], values\_list['tubes'],
values\_list['chromo'], values\_list['date'], values\_list['clone'],
values\_list['source'], values\_list['location'], values\_list['start']
values\_list['end'], values\_list['gene'], values\_list['genelink'],
values\_list['dna'], values\_list['validation'], values\_list['pcr'],
values\_list['refs'], values\_list['antibiotic'],
values\_list['idbac'])) database.commit() database.close()[/sourcecode]
which is really ugly and, although it works, is not really useful
outside this small project. Based on the comments the best option was to
use placeholders and a dictionary, similar to the approach used on the
insert data function. Pre-formatting a string to have both the field
name to be updated and a placeholder (for instance `:idbac`) that will
receive the values [sourcecode language='python']update =
','.join(['%s=:%s' % (y, y) for y in values\_list])[/sourcecode] where
update is the string we want and values\_list is the dictionary with all
the key-value pairs. I tried this approach, using this structure in the
generic function, but then I decided that the best alternative was to
put this `join` in the derived class function and pre-populate the
string with the values and then send this string directly to the update
function. In the end I opted to use this [sourcecode
language='python']update = ','.join(['%s=\\"%s\\"' % (y,
values\_list[y]) for y in values\_list])[/sourcecode] The latter is
slightly different to what was suggested. The original one would create
a tuple with the keys from the dictionary, making for instance
`sdate:sdate`. With all these place holders just pass the dictionary and
you have all the values inserted. This would be handy if the insert
string was being created on the "generic" function. If we move this to
the derived class, we can use the the alternative, keeping in mind that
the values parsed should be surrounded by quotes, otherwise the SQL
UPDATE statement will have problems with spaces and other foreign
characters that should not be there. So instead of placeholders we will
have `gene:"PTEN"` and we can attache this joined string to the actual
commands. We then can move all the machinery from the "generic" function
that can be written as [sourcecode language='python']def
update\_data(self, update\_string): '''edits and updates fields''' if
sys.platform == 'darwin': (cursor, database) = link\_db(self.db\_path)
else: (cursor, database) = link\_db() cursor.execute(update\_string)
database.commit() database.close()[/sourcecode] That's it, very elegant
(we will see the derived class in the next post). And finishing our
generic class, we would need a delete function, so the user can
eliminate entries that he/she doesn't want anymore. It's also a very
simple function [sourcecode language='python']def delete\_data(self,
delete\_string): '''deletes one field''' if sys.platform == 'darwin':
(cursor, database) = link\_db(self.db\_path) else: (cursor, database) =
link\_db() cursor.execute(delete\_string) database.commit()
database.close()[/sourcecode] We will check the delete string next time.
Again, I would like to thank for all the comments, it has been really
helpful for me. Previously in the series: [Part
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
[Part
7](http://python.genedrift.org/2009/04/20/managing-a-simple-database-with-python-sqlite-and-wxpython-7-includes-a-question/)

[![Reblog this post [with
Zemanta]](http://img.zemanta.com/reblog_a.png?x-id=e8dc77f5-e3de-4d4f-8ec1-8c0006225743)](http://reblog.zemanta.com/zemified/e8dc77f5-e3de-4d4f-8ec1-8c0006225743/ "Reblog this post [with Zemanta]")
