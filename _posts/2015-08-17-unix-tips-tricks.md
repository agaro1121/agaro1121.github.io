---
layout: post
title: Unix Command Line Tips & Tricks
date: '2015-08-17T15:51:00.000-07:00'
author: Anthony Garo
tags:
- Unix
- WhatILearnedToday
- Code
modified_time: '2016-02-28T16:05:41.673-08:00'
blogger_id: tag:blogger.com,1999:blog-4180298707082402742.post-5296071985668450680
blogger_orig_url: http://scarrediron.blogspot.com/2015/08/unix-tips-tricks.html
---

Below are some handy command line tips and tricks.You can read the rest with "Ubuntu Unleashed 2015 Edition"
!! - Run last command

For Example:

```bash
Hierro > echo "Saluton Mondo"
Saluton Mondo
Hierro > !!echo "Saluton Mondo"
Saluton Mondo
```

You can even combine it with other commands.
For example:

sudo !! will run sudo echo "Saluton Mondo"

!*(bang star) - This is a tricky one. This one will print out the last thing terminal spit out.
The below command will allow you nano the file from the ls command.

```bash
Hierro > ls testFile2.txt
testFile2.txt
Hierro > nano !*
nano testFile2.txt
```

Used alone, it will print out the last thing in the terminal and use it as a command like below

```bash
    Hierro > echo "echo"
    echo
    Hierro > !* "hello"
    "echo" "hello"
    hello
```


Ctrl+U  #erase the entire line
Ctrl+W  #erase word by word
Ctrl+A  #move your cursor to the beginning of the line
Ctrl+E  #move your cursor to the end of the line
Ctrl+K  #erase everything to the right of your cursor’s position
Ctrl+Y  #restore something you just deleted, but shouldn’t have

Chaining terminal commands:

```bash
command1 ; command2  # Runs commands consecutively
command1 && command2 # Runs command2 ONLY IF command1 runs successfully
command1 || command2 # Runs command2 ONLY IF command1 runs unsuccessfully
```

If your system crashes: REISUB
        to the rescuen hold PrtSc+Alt and press REISUB
        in that order slowly>nbsp;
        unRaw—Takes control of the keyboard back from the X server.

        tErminate
—Sends a SIGTERM command to all processes, which allows time for the processes to terminate gracefully.

        kIll
—Sends a SIGKILL to all processes, forcing any still running to terminate immediately.

        Sync—Flush data from memory to disk.

        Unmount—Unmount and remount all filesystems as read only.

        reBoot—Turn off and back on again, restarting the computer.