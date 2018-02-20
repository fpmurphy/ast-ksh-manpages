# NAME

tee - duplicate standard input

# SYNOPSIS

`tee` \[ `options` \] \[file ...\]

# DESCRIPTION

`tee` copies standard input to standard output and to zero or more
files. The options determine whether the specified files are overwritten
or appended to. The `tee` utility does not buffer output. If writes to
any `file` fail, writes to other files continue although `tee` will
exit with a non-zero exit status.
The number of `file` operands that can be specified is limited by the
underlying operating system.

# OPTIONS

-`a`, --`append`
:   Append the standard input to the given files rather than
    overwriting them.

-`i`, --`ignore-interrupts`
:   Ignore SIGINT signal.

-`l`, --`linebuffer`
:   Set the standard output to be line buffered.

# EXIT STATUS

`0`
: All files copies successfully.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`cat`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/cat.html)(1),
[`signal`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man3/signal.html)(3)

# IMPLEMENTATION

`version`
:   tee (AT&T Research) 2012-05-31

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030251/http://www.eclipse.org/org/documents/epl-v10.html)


