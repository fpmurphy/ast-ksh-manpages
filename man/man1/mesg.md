# NAME

mesg - permit or deny messages to the terminal

# SYNOPSIS

`mesg` \[ `options` \] \[ y | n \]

# DESCRIPTION

`mesg` controls whether other users are allowed to send messages via
[`write`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/write.html)(1),
[`talk`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/talk.html)(1)
or other commands to the terminal device. The terminal device affected
is determined by searching for the first terminal in the sequence of
devices associated with standard input, standard output and standard
error, respectively. With no arguments, `mesg` reports the current
state without changing it. Processes with appropriate privileges may be
able to send messages to the terminal independent of the current state.

# OPERANDS

The following operands are supported:

`y`
: Grant permission to other users to send messages to the terminal.

`n`
: Deny permission to other users to send messages to the terminal.

# SEE ALSO

[`talk`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/talk.html)(1),
[`write`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/write.html)(1)

# IMPLEMENTATION

`version`
:   mesg (AT&T Research) 1999-04-28

`author`
:   David Korn

`copyright`
:   Copyright © 1995-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030246/http://www.eclipse.org/org/documents/epl-v10.html)


