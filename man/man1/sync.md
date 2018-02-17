# NAME

sync - schedule file system updates

# SYNOPSIS

`sync` \[ `options` \]

# DESCRIPTION

`sync` calls
[`sync`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man2/sync.html)(2),
which causes all information in memory that updates file systems to be
scheduled for writing out to all file systems. The writing, although
scheduled, is not necessarily complete upon return from `sync`.
Since
[`sync`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man2/sync.html)(2)
has no failure indication, `sync` only fails for option/operand syntax
errors, or when
[`sync`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man2/sync.html)(2)
does not return, in which case `sync` also does not return.

At minimum `sync` should be called before halting the system. Most
systems provide graceful shutdown procedures that include `sync` --
use them if possible.

# EXIT STATUS

`0`
: [`sync`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man2/sync.html)(2) returned.

`&gt;0`
:   Option/operand syntax error.

# SEE ALSO

[`sync`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man2/sync.html)(2),
[`shutdown`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man8/shutdown.html)(8)

# IMPLEMENTATION

`version`
:   sync (AT&T Research) 2006-10-04

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030251/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030251/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030251/http://www.eclipse.org/org/documents/epl-v10.html)


