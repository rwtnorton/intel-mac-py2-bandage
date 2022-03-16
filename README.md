# intel-mac-py2-bandage

A kludge for Intel Mac users who'd like their old Python 2 back.

## Why?

Along with version 12.3 of macOS, the built-in Python 2 is actually removed
(as it had been deprecated for years).  Those files lived under:
- /System/Library/Frameworks/Python.framework/

Unfortunately, some programs have not caught up with this change, and
after upgrading to 12.3+ those programs just fail.  (For example,
the Mac launcher client for FF XIV very much expects that system Python 2
to be present; without it, no game.)

## How?

This repo holds a tarball of a `Python.framework/` from an unupgraded
Intel Mac.  The idea is to unpack the tarball at a sister directory
(because things under `/System` are read-only by default for security).

```
$ cd /Library/Frameworks
$ mv {,.old.}Python.framework  # just in case, rename the old
$ bzip2 -cd $path_to_repo/py2.tar.bz2 | tar xvf -
### Or as root:
$ sudo bash -c 'bzip2 -cd $path_to_repo/py2.tar.bz2 | tar xvf -'
```

Now, there should be a Python 2 interpreter here:
```
$ /Library/Frameworks/Python.framework/Versions/2.7/bin/python2
```
(To exit, type Ctrl-d.)

## Really?

This is just a kludge.  Hopefully, these programs that have relied
on having a system Python 2 available will have updates to address
this problem.  Until then, better than nothing I guess.

## Caveat emptor

I take no responsibility for what this might do to your computer.
It works on *my* Intel Mac but you never know with these things.

### Will this work on an M1 Mac?

I seriously doubt it.  While the compiled Python files (.pyc) should
be portable, there are some native compiled files (.so) that I would
expect to be particular to an Intel architecture.
