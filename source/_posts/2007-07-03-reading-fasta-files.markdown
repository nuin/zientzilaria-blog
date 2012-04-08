---
author: Paulo Nuin
date: '2007-07-03 16:39:37'
layout: post
slug: reading-fasta-files
status: publish
title: 'Reading FASTA files: introduction'
wordpress_id: '39'
? ''
: - Section 5
---

Again after a long period we are back. We already have most of the
knowledge to create very useful scripts and small programs in Python.
And in this post we will create a routine that will make the biologist's
life even easier (when programming Python). A great part of
bioinformatics is to store data, how to store it and which format to
use. Anyone working in a wetlab or on a pure bioinformatics lab had had
problems with file formats one day or another. In fact, you don't have
to be in a bioinformatics environment to have such problems, but in
biology people tend to create a file format for everyt program they
write. We can call it a lack of standards, sometimes. But one very well
established format is the FASTA (pronounced FAST-Aye, according to the
EMBl-EBI page for the software with identical name. This format is
really simple and easy to manipulate with most computer languages and
being text-based adds an extra advantage of portability for the files.
Usually a FASTA file has a structure like this 

    >title/name/extra information about the sequence  
    sequence in one or many lines

There is
no limit on the number of sequences that can be stored in a file,
neither on the size of each sequence. Usually sequences that are larger
than 70-80 nucleotides/amino acids are displayed in multiple lines.

`>Q15465|SHH_HUMAN Sonic hedgehog protein - Homo sapiens (Human).
MLLLARCLLLVLVSSLLVCSGLACGPGRGFGKRRHPKKLTPLAYKQFIPNVAEKTLGASG
RYEGKISRNSERFKELTPNYNPDIIFKDEENTGADRLMTQRCKDKLNALAISVMNQWPGV
KLRVTEGWDEDGHHSEESLHYEGRAVDITTSDRDRSKYGMLARLAVEAGFDWVYYESKAH
IHCSVKAENSVAAKSGGCFPGSATVHLEQGGTKLVKDLSPGDRVLAADDQGRLLYSDFLT
FLDRDDGAKKVFYVIETREPRERLLLTAAHLLFVAPHNDSATGEPEASSGSGPPSGGALG
PRALFASRVRPGQRVYVVAERDGDRRLLPAAVHSVTLSEEAAGAYAPLTAQGTILINRVL
ASCYAVIEEHSWAHRAFAPFRLAHALLAALAPARTDRGGDSGGGDRGGGGGRVALTAPGA
ADAPGAGATAGIHWYSQLLYQIGTWLLDSEALHPLGMAVKSS `


So, let's write a function
and a small script to read a typical FASTA file and display the output.
Later we will see how to manipulate the file and in the end we will have
created a list of scripts that will be useful for the everyday
laboratory life. But before we get to our final goal, we need to learn
some new features of Python. In our case **Classes**. Classes in Python
are very similar to classes in C++, and they are the building blocks of
Object Oriented Programming (OOP). This guide will only scratch the
surface of OOP, as it is a very complex subject, requiring a guide of
its own. There are plenty of good introductory material online and any
Google search will return dozens of links. Let's focus on some basic
concepts, what will be exactly what we will need here. Classes are
basically objects with associated properties (attributes) and methods. A
traditional introductory example of classes is the employee list. In a
company all employees are registered and they basic information are
stored in the human resources file system. Let's call the main class
`Employee` with three attributes: `name`, `room_number` and
`favourite_colour`. This defines a class. Let's see how to do that in
Python: 

{% codeblock lang:python %}class Employee: 
    def __init__(self, name, room, colour): 
        self.name = name 
        self.room = room 
        self.colour = colour{% endcodeblock %} 

Let's dissect this piece of code.
First we declare a class and give a name to it `Employee`. The next
thing we need to do is to define the initiation (constructor) method of
the class and give it the attributes we need, that's the `__init__`
method. Every time we create a copy of the main class object the copy
will be initialized with the values we are passing to the method.
According to Dive into Python "The first argument of every class method,
including `__init__`, is always a reference to the current instance of
the class". That's the `self` on the method definition, which is
followed by what we want to store in the object: name, room and
favourite colour. The lines in the method are the ones assigning the
received values to the different class' attributes. 

Again from Dive into
Python we have "To reference this attribute from code outside the class,
you qualify it with the instance name, instance.data, in the same way
that you qualify a function with its module name. To reference a data
attribute from within the class, you use self as the qualifier". In
other words the attributes of the class are seen internally by it by the
use of `self` while from the outside (another part of the script) it is
seen by the name given to the instance of the class. It is a little bit
confusing, so let's see an example below. 

{% codeblock lang:python %}class Employee: 
    def __init__(self, name, room, colour): 
        self.name = name 
        self.room = room 
        self.colour = colour


employeename = "Paulo" 
roomnumber = "21" 
colour = "blue" 
newemployee = Employee(employeename, roomnumber, colour) 
print newemployee{% endcodeblock %} 


If we run this simple code we will get
something like this 


{% codeblock lang:python %}<__main__.Employee instance at 0x7379cc>{% endcodeblock %} 

And that's exactly what we need here: that's a class instance that was created by 

{% codeblock lang:python %}newemployee = Employee(employeename, roomnumber, colour){% endcodeblock %} 

Printing this information is not very useful. We
don't want to know the memory address of the object, we want to get the
attributes of it, so we need to change `print newemployee` by these
lines: 

{% codeblock lang:python %}
print newemployee.name 
print newemployee.room 
print newemployee.colour{% endcodeblock %} 

There they are,
run it and see what is being printed to the screen. Of course, as is
this script does not accomplish anything useful, but imagine that you
need to read a file with 1000 new employees everyt month. That's what we
need to do with FASTA files everyday and we will see how to do that on
the next post.
