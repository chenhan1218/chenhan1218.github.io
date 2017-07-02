---
title: 'PuDB Python Debugging Tool. A full-screen, console-based Python debugger'
date: "2016-03-31 02:51:00"
comments: true
categories: 
---
I highly recommened pudb, which is a full-screen, console-based visual debugger for Python. The user-interface is nicely designed for python developers.

Here is an example debugging a simple python script:
[Introduction to the PuDB Python Debugging Tool
](http://heather.cs.ucdavis.edu/~matloff/pudb.html)

Also, another great tutorial is from Jordi Gutiérrez Hermoso. 
[Montreal, QC, September 14, 2015 - Jordi Gutiérrez Hermoso presents PuDB, a full-screen, console-based visual debugger for Python.](https://www.youtube.com/watch?v=IEXx-AQLOBk)
An interesting comment from the speaker:
> Everyone should use a debugger
> ...
>
> But If pdb is the only debugger you've every seen, I won't blame you not using a debugger
> 
> ...
> because the debugger is ugly, not because the source code is ugly

To install pudb on Debian/Ubuntu, you can use apt-get to install the package 
``` bash
# for python 2
sudo apt-get -y python-pudb
# for python 3
sudo apt-get -y python3-pudb

# pudb is even better when debugging with ipython
# so that's install ipython
sudo apt-get install ipython
```