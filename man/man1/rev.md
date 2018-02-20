# NAME

rev - reverse the characters or lines of one or more files

# SYNOPSIS

`rev` \[ `options` \] \[file ...\]

# DESCRIPTION

`rev` copies one or more files to standard output reversing the order
of characters on every line of the file or reversing the order of lines
of the file if `-l` is specified.
If no `file` is given, or if the `file` is `-`, `rev` copies from
standard input starting at the current offset.

# OPTIONS

-`l`, --`line`
:   Reverse the lines of the file.

# EXIT STATUS

`0`
: All files copied successfully.

`&gt;0`
:   One or more files did not copy.

# SEE ALSO

[`cat`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/cat.html)(1),
[`tail`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/tail.html)(1)

# IMPLEMENTATION

`version`
:   rev (AT&T Research) 2007-11-29

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030249/http://www.eclipse.org/org/documents/epl-v10.html)


