# NAME

fds - list open file descriptor status

# SYNOPSIS

`fds` \[ `options` \]

# DESCRIPTION

`fds` lists the status for each open file descriptor. When invoked as
a shell builtin it accesses the file descriptors of the calling shell,
otherwise it lists the file descriptors passed across
[`exec`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man2/exec.html)(2).

# OPTIONS

-`l`, --`long`
:   List file descriptor details.

-`u`, --`unit`=`fd`
:   Write output to `fd`.

# SEE ALSO

[`logname`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/logname.html)(1),
[`who`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/who.html)(1),
[`getgroups`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man2/getgroups.html)(2),
[`getsockname`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man2/getsockname.html)(2),
[`getsockopts`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man2/getsockopts.html)(2)

# IMPLEMENTATION

`version`
:   fds (AT&T Research) 2009-09-09

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030243/http://www.eclipse.org/org/documents/epl-v10.html)


