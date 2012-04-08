---
author: admin
date: '2009-02-18 11:06:58'
layout: post
slug: managing-a-simple-database-with-python-sqlite-and-wxpython-3
status: publish
title: Managing a simple database with Python, SQLite and wxPython, 3
wordpress_id: '244'
? ''
: - bioinformatics
  - Database
  - Phase 2
  - Programming
  - SQL
  - SQLite
---

In the last post we saw how to connect to a
[SQLite](http://sqlite.org/ "SQLite") database file and generate a
cursor that would allow us to actually interact with such database. Now
we need some functionality that will interact with the data, add, read,
delete and search. As was mentioned before the idea is to have a generic
database interaction class and have unique instantiated class objects
for each database of the project. In the `db_obj.py` file we have an
initial structure set, so let's check the `DB_Generic` class.
[sourcecode language='python']class DB\_Generic(): '''generic class to
add DB functionality''' def \_\_init\_\_(self, table\_name): \#par= name
of the table to be used self.table\_name = table\_name def
delete\_entry(self): pass def get\_data\_generic(self): '''gets the data
from the database generic so far, needs to be updated to include
range''' range = 1 (cursor, database) = link\_db() if range == 1:
cursor.execute("""SELECT \* from %s""" % self.table\_name) table\_data =
cursor.fetchall() raw\_data = [] for i in table\_data:
raw\_data.append(list(i)) self.table\_data = raw\_data database.close()
def insert\_data(self, values\_list, insert\_string): '''inserts data in
the database''' (cursor, database) = link\_db()
cursor.execute(insert\_string % self.table\_name, values\_list)
database.commit() database.close()[/sourcecode] There are different
functions in this class, we will take a look at each one individually.
We can see that the class is far from being complete, something that
we'll do in the next posts. We start with the class initialization:
[sourcecode language='python']def \_\_init\_\_(self, table\_name):
\#par= name of the table to be used self.table\_name =
table\_name[/sourcecode] Very simple and direct, it receives the table
name that is being used by the interface (in this case). The table name
is then stored in a object that can be accessed by other functions in
the class. The function to delete entries is not finished as we only
have a `pass` in it. We'll will do it soon. Next we have a function that
gets the data from the table. [sourcecode language='python'] def
get\_data\_generic(self): '''gets the data from the database generic so
far, needs to be updated to include range''' range = 1 (cursor,
database) = link\_db() if range == 1: cursor.execute("""SELECT \* from
%s""" % self.table\_name) table\_data = cursor.fetchall() raw\_data = []
for i in table\_data: raw\_data.append(list(i)) self.table\_data =
raw\_data database.close()[/sourcecode] So far it grabs everything,
there is no range selection based on any of the table fields, so it's a
generic SQL `SELECT`. Let's dissect it. The `range` object is a dummy
variable that at the moment is there only to remind us that we need to
include a range select. The next line is the most important in this
function: it will call the `link_db` function and start the connection.
Remember that `link_db` returns a tuple with the cursor and database
connection. Basically we will work with cursor methods to get the data,
and the first action is to execute a SQL `SELECT` stetement where we
select everything in the table [sourcecode
language='python']cursor.execute("""SELECT \* from %s""" %
self.table\_name)[/sourcecode] Notice that the statement is a regular
string and we use string formating `%` in ordert o add the table that we
are searching, which was defined when we initialized the class object in
the first place. Also, notice the triple quotes around the select
statement: this will avoid any problems in parsing it when sending to
the database, making it a [string
literal](http://en.wikipedia.org/wiki/String_literal "String literal").
So this line executes the statement we pass to the method, but it does
not actually get the data *per se*. We need to use another method and
fetch everything returned by the select. This is done by [sourcecode
language='python']table\_data = cursor.fetchall()[/sourcecode] A couple
of things here. The data fetched will be always (or in most cases) in
unicode, when it's a string field. And the data returned will be in a
list of tuples, with the actual number of fields from the table. We know
that it's easier to work with lists than tuples, so we code something to
convert types [sourcecode language='python']table\_data =
cursor.fetchall() raw\_data = [] for i in table\_data:
raw\_data.append(list(i)) self.table\_data = raw\_data[/sourcecode]
There are extra lines here that are not needed, and we will get rid of
them in a code refactoring soon. This short function is able to connect
to database, execute a SQL statement on a specified table and grab the
data selected, returning a list of lists with every field and value
available. We need to add a better selection statement later, and we
will do as soon as we have a good structure set. The last function in
this generic class is the one that inserts data into the table.
[sourcecode language='python']def insert\_data(self, values\_list,
insert\_string): '''inserts data in the database''' cursor, database) =
link\_db() cursor.execute(insert\_string % self.table\_name,
values\_list) database.commit() database.close()[/sourcecode] Identical
procedure: connect, get a cursor, execute a statement. But in this case
the extra step is not to get the data, but to commit the data to the
table, which is done by the commit method. We will explain later how the
execute method works here and what are the `insert_string` and
`values_list`. Notice at the end that we need to close the connection to
the database, so we know that the data has been inserted properly. Next,
we will instantiate a class from this generic one and see how easy is to
manipulate the data. Stay tuned. Previously in the series: [Part
1](http://python.genedrift.org/2009/02/09/managing-a-simple-database-with-python-sqlite-and-wxpython-1/)
[Part
2](http://python.genedrift.org/2009/02/17/managing-a-simple-database-with-python-sqlite-and-wxpython-2/)
[![Reblog this post [with
Zemanta]](http://img.zemanta.com/reblog_e.png?x-id=1663854e-5aba-4ff1-9a75-dffb8e6b7945)](http://reblog.zemanta.com/zemified/1663854e-5aba-4ff1-9a75-dffb8e6b7945/ "Zemified by Zemanta")
