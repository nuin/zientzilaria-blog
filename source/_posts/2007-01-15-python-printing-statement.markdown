---
author: admin
date: '2007-01-15 18:40:41'
layout: post
slug: python-printing-statement
status: publish
title: Python printing statement
wordpress_id: '7'
? ''
: - print
  - python
  - Section 1
---

Just an apart from the bioinformatics aspect of programming: Python's
`print` statement. As in most computer languages Python allows an easy
way to write to the standard output. Python's `print` only accepts
output of strings, and if the variable sent to it is not a string it is
first converted and then output. The `print` always put a linebreak
(`'\n'` or `"\n"`) at the end of the expression to be output, except
when the `print` statement ends with a comma. For example: 

{% codeblock lang:python %}
print "This is a" 
print "test"
{% endcodeblock %}

will print

**This is a**
**test** 

while 


{% codeblock lang:python %}
print "This is a",
print "test"
{% endcodeblock %}




will print 

**This is a test** 

Of course Python's `print` statement allows any programming escape character, such
as `'\n'` and `'\t'`. 


**Concatenating strings on output** 

To concatenate two strings on output there are two possible ways in Python. You can
either separate the strings with a comma, like we did here 

{% codeblock lang:python %}
print myDNA, myDNA2
{% endcodeblock %}


 or you can use the "+" sign in roder to obtain almost the same result. This is similar to
what was used here 

{% codeblock lang:python %}
myDNA3 = myDNA + myDNA2
{% endcodeblock %}


but instead we would use the `print` command as


{% codeblock lang:python %}print myDNA3 + myDNA{% endcodeblock %}

In the latter case, both strings will not be separated by a space and will be
merged. To get the same result you would have to concatenate an extra
space between the strings like 

{% codeblock lang:python %}
print myDNA3 + " " + myDNA{% endcodeblock %}
