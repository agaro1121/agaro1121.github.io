---
layout: post
title: Brief Sed & Awk
date: '2016-02-28T16:04:00.008-08:00'
author: Anthony Garo
tags:
- Unix
- Code
modified_time: '2016-02-28T16:04:46.681-08:00'
blogger_id: tag:blogger.com,1999:blog-4180298707082402742.post-330568664393824042
blogger_orig_url: http://scarrediron.blogspot.com/2016/02/brief-sed-awk.html
---

Sed 

sed,from Stream EDitor, is a command that is used to perform transformations on text. It works from the command line and processes text via standard in and standard out. It does not modify the original input and does not save the output unless you redirect that output to a file

Examples:


```bash
sed sedcommand inputfile
sed -e sedcommand inputfile #does the same thing as above, except that it specifically denotes the command to run
sed -e sedcommand -e anothersedcommand inputfile
```
Let’s say I want to change every instance of camel in the text file transportation.txt todune buggy.
Here is how to do that:

```bash
sed -e 's/camel/dune buggy/g' transportation.txt
```

s=substitute
g=global(everywhere in the file)

If I wanted to delete lines 4 through 17 in the file longtext.txt, I would do this:

```bash
sed -e '4,17d' longtext.txt
```

You can use other things in place of the line numbers such as regex

Awk
A small programming language for processing strings. It takes in text, transforms it in whatever way you tell it to, and then outputs the transformed text.
The most common use of awk is to manipulate files that consist of fields separated by delimiters, such as a comma separated values (CSV) or a configuration file.

What if we had a comma-delimited file containing names of things on my desk, a category for each, a color for each, and a date corresponding to the last time I picked that item up. 
That is 4 columns: name, category, color, and date. 
If I only really cared about the names and dates, then I could use awk to process the file quickly and list just these for me, like this:

```bash
awk -F',' '{print $1, "was last picked up on", $4}' deskstuff.txt
```

-F defines the delimeter(',')

You can define multiple delimiters:
-F'[;,-]'