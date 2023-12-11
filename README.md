vgrind
======

The venerable BSD prettyprinter, which I am forking so that I can build it for my own use on macOS, and perhaps reference the repository in other projects.

Source
------
This source was gathered from NetBSD.org, using the following
commands:

    export CVSROOT="anoncvs@anoncvs.NetBSD.org:/cvsroot"
    export CVS_RSH="ssh"
    cvs checkout -P -d vgrind src/usr.bin/vgrind
	
No effort is currently being make to track the original, which is decades-old.
