---
author: admin
date: '2009-03-02 11:58:09'
layout: post
slug: managing-a-simple-database-with-python-sqlite-and-wxpython-4
status: publish
title: Managing a simple database with Python, SQLite and wxPython, 4
wordpress_id: '250'
? ''
: - bioinformatics
  - Phase 2
  - Programming
  - python
  - SQL
  - SQLite
  - wxPython
---

[![The :en:SQLite logo as of
2007-12-15](http://upload.wikimedia.org/wikipedia/commons/thumb/1/19/SQLite_Logo_4.png/202px-SQLite_Logo_4.png "The :en:SQLite logo as of 2007-12-15")](http://commons.wikipedia.org/wiki/Image:SQLite_Logo_4.png)
  ~ Image via
    [Wikipedia](http://commons.wikipedia.org/wiki/Image:SQLite_Logo_4.png)

Let's continue building our small db app. As mentioned in the previous
post we need now to instantiate a specific class from our generic
[SQLite](http://sqlite.org/ "SQLite") access class. In order to do this
we just have to declare a new class and its type will be `DB_Generic`.
[sourcecode language='python']class Bac(DB\_Generic)[/sourcecode] This
new class is called Bac because it's linked to the bac table in our
database file. A side note, bacs are Bacterial Artificial Chromosomes
and are used in different molecular biology techniques. Mainly in our
case bacs have incorporated human DNA segments and are used as probes
for deletion, duplication, etc studies. Now, back to our Python code, as
soon as we instantiate our generic class, the object (class) we create
has access to all methods and functions from the parent class (by using
`self`), but we still need to create functionality and expose other
methods that can be accessed from a class object derived from `Bac`. Our
instantiated class will be [sourcecode language='python']class
Bac(DB\_Generic): def \_\_init\_(self): self.bac\_data = []
DB\_Generic.\_\_init\_\_(self, 'bac') def get\_data(self): return
self.get\_data\_generic() def load\_data(self): pass def add\_data(self,
values\_list): insert\_string = """INSERT INTO %s (projects, comments,
temperature, cell, box, tubes, chromosome, sdate, clone, source,
location1, startpos, endpos, gene, genelink, dnaex, validation, pcr,
refs, antibiotic) VALUES (:projects, :comments, :temperature, :cell,
:box, :tubes, :chromo, :date, :clone, :source, :location, :start, :end,
:gene, :genelink, :dna, :validation, :pcr, :refs, :antibiotic)"""
self.insert\_data(values\_list, insert\_string)[/sourcecode] Pretty
simple so far, as we don't have a lot of declared methods. Let's check
one by one [sourcecode language='python']def \_\_init\_(self):
DB\_Generic.\_\_init\_\_(self, 'bac')[/sourcecode] The only line is the
initialization required by the parent class, and we're passing the value
that is the table to be accessed. [sourcecode language='python']def
get\_data(self): self.get\_data\_generic() return
self.table\_data[/sourcecode] The `get_data` function returns the all
elements in our table (So far, we still don't have an elegant range
option) and has one too many lines in it. We will get rid of some
useless code here in the future, but it's OK the way it is. Basically
this code access the `get_data_generic` from the parent class and gets
all the values stored in the table. There is a function not yet complete
that will load data, and will be used in the future. And the last one is
the function that actually adds the data to the table with a SQL insert
statement [sourcecode language='python']def add\_data(self,
values\_list): insert\_string = """INSERT INTO %s (projects, comments,
temperature, cell, box, tubes, chromosome, sdate, clone, source,
location1, startpos, endpos, gene, genelink, dnaex, validation, pcr,
refs, antibiotic) VALUES (:projects, :comments, :temperature, :cell,
:box, :tubes, :chromo, :date, :clone, :source, :location, :start, :end,
:gene, :genelink, :dna, :validation, :pcr, :refs, :antibiotic)"""
self.insert\_data(values\_list, insert\_string)[/sourcecode] In this
function, we have a large string with all the SQL insert options. A SQL
insert statement is divided into two parts, one where you point where to
insert the values and another where you input the values. Usually simple
insert statements will have this structure [sourcecode
language='sql']INSERT INTO my\_table\_name (table\_column1,
table\_column2) VALUES (value1, value2);[/sourcecode] So, we have the
table we want to insert values into, its columns and the values we set
for each column. After executed this will put value1 into table\_column1
and value2 into table\_column2. The actual syntax can vary a bit for
different SQL engines but the structure is identical in most cases.
Pretty simple. For our insert string above, there are some aspects to
call for attention. Again note the triple quote around the statement.
This make sure that it's not changed and parsed correctly. We also have
a `%s` for the table name, which will be parsed by the parent class
function that insert values, then a list of all the tables in the
database and then a list of values to insert. And why the values to be
inserted have this `:value` syntax? Because we are previously storing
the values in a dictionary, and the ":" indicates that we need to get
the dictionary value for the correspondent key. The insert string, and
the list of values (actually a dictionary, not the best variable/object
name I must admit) is then sent to the parent class to be inserted.
Storing the values to be inserted in a dictionary is OK for a one time
insert case, where the values are obtained from a form. If you are
parsing a large CSV or TSV file, ideally it's better to put it in a
list, and dump them at the same time. We're progressing. Next we will
take a look on some simple SQL table structure and then move to create
the form to insert the values and check the table. Previously in the
series: [Part
1](http://python.genedrift.org/2009/02/09/managing-a-simple-database-with-python-sqlite-and-wxpython-1/)
[Part
2](http://python.genedrift.org/2009/02/17/managing-a-simple-database-with-python-sqlite-and-wxpython-2/)
[Part
3](http://python.genedrift.org/2009/02/18/managing-a-simple-database-with-python-sqlite-and-wxpython-3/)

[![Reblog this post [with
Zemanta]](http://img.zemanta.com/reblog_e.png?x-id=4c2737a4-f1de-46bf-ae53-c5de040daf97)](http://reblog.zemanta.com/zemified/4c2737a4-f1de-46bf-ae53-c5de040daf97/ "Zemified by Zemanta")

evi
