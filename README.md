vgrind
======

The venerable BSD prettyprinter, which I am forking for my own use on
macOS, and perhaps for use in other projects.

Source
------
This source was gathered from NetBSD.org, using the following
commands:

    export CVSROOT="anoncvs@anoncvs.NetBSD.org:/cvsroot"
    export CVS_RSH="ssh"
    cvs checkout -P -d vgrind src/usr.bin/vgrind
	
No effort is currently being make to track the original, which is
decades-old.

### Notes

Makefile and vgrind.sh in the project rootdir are the BSD originals,
kept for reference.  RETEST contains a test program for refexp.c.

