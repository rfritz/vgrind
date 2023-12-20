vgrind and pprint
=================
The venerable BSD source code typesetter, which I am forking for my
own use on macOS, and perhaps for use in other projects.  The
**vgrind** command sends its results to a printer using **lp**; I have
added a **pprint** command which produces PDF files.

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

Makefile and vgrind.sh in the ATTIC are the BSD originals, kept for
reference.  RETEST contains a test program for regexp.c.

