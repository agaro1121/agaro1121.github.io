---
layout: post
title: The tar Command
date: '2015-08-12T08:17:00.003-07:00'
author: Anthony Garo
tags:
- Unix
- WhatILearnedToday
- Code
modified_time: '2015-08-17T04:53:59.439-07:00'
blogger_id: tag:blogger.com,1999:blog-4180298707082402742.post-2829987774162831427
blogger_orig_url: http://scarrediron.blogspot.com/2015/08/learning-unix.html
---

Every day I like to learn something new, whether it's big or small. Sometimes I take time to "relearn"
something and understand it in different, simpler ways so I don't have to remember the small details. You'd be
surprised how much faster those small details come back when you know how everything fits together.
    
On to what I learned !
Lately I've been experimenting with Linux(again). I installed an Ubunto Distro onto my rig and have been
learning the command line bit by bit.        


The tar command
I've been using this command for years but had to google the syntax every single time.
That ends today !!!
What is tar?

* It basically zips/unzips files.

How to use it?

**CODE EXAMPLE**

```bash
tar [putflags here] [newZipFileName.tgz] [directory to zip up]
tar [put flags here] [newZipFileName.tgz]
```

Small things to know
tar has a few flags you always use

<ul class="mdlist">
    <li>x => extract files</li>
    <li>c => create archive</li>
    <li>t => list files</li>
    <li>v => verbose (list files as it processes them)...shows you what's happening live</li>
    <li>j => use bz2 compression</li>
    <li>z => use gz compression</li>
    <li>f => read or write files to disk.</li>
</ul>

How to remember the small things?
- You always use the same flags to zip/unzip files except for one flag.

Look at your keyboard. You have z,x,c,v,f in a nice L shape for you. Why did I have you do this?
    Because your tar command looks like this:

**Zip**

```bash
tar czvf ...
```


**Unzip**

```bash
-tar xzvf ...
```

As I promised same exact command except for the first flag z/x or create/extract LOL
The ```z``` flag is interchangeable with the ```j``` flag depending on the type of compression you're working with.

**Zip**

```bash
tar cjvf ...
```

**Unzip**

```bash
tar xjvf ...
```

**Code Samples**

```bash
tar czvf testZipFile.tar.gz myDir/
tar xzvf testZipFile.tar.gz
tar cjvf testZipFile.tar.bz2 myDir/
tar xjvf testZipFile.tar.bz2
```

BTW: To simply view what's in your compressed file

```bash
tar tzvf testZipFile.tar.gz
tar tjvf testZipFile.tar.bz2
```