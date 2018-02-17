# NAME

execrate - wrapper for .exe challenged commands

# SYNOPSIS

`execrate` \[ `options` \] command \[ option ... \] file ...

# DESCRIPTION

`execrate` runs `command` after checking the `file` operands for
standard semantics with respect to `win32` `.exe` suffix
conventions. This command is only needed on `win32` systems that
inconsistently handle `.exe` across library and command interfaces.
`command` may be one of
[`cat`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/cat.html)(1),
[`chmod`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/chmod.html)(1),
[`cmp`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/cmp.html)(1),
[`cp`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/cp.html)(1),
[`ln`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/ln.html)(1),
[`mv`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/mv.html)(1),
or
[`rm`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/rm.html)(1).
Only the 2 argument forms of `cp`, `ln` and `mv` are handled.
Unsupported commands and commands requiring no change are silently
executed.
With no arguments `execrate` exits with status 0 if the current system
is `.exe` challenged, 1 if the current system is normal.

# OPTIONS

-`n`, --`show`
:   Show the underlying commands but do not execute.

# SEE ALSO

[`webster`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/webster.html)(1)

# IMPLEMENTATION

`version`
:   execrate (AT&T Labs Research) 2002-02-02

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030243/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 2002-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030243/http://www.eclipse.org/org/documents/epl-v10.html)


