# NAME

tsort - topological sort

# SYNOPSIS

`tsort` \[ `options` \] \[ file \]

# DESCRIPTION

`tsort` writes to the standard output a totally ordered list of items
consistent with a partial ordering of items contained in the input
`file`. If `file` is omitted then the standard input is read.
The input consists of pairs of items (non-empty strings) separated by
blanks. Pairs of different items indicate ordering. Pairs of identical
items indicate presence, but not ordering.

# SEE ALSO

[`comm`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/comm.html)(1),
[`sort`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/sort.html)(1),
[`uniq`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/uniq.html)(1)

# IMPLEMENTATION

`version`
:   tsort (AT&T Research) 2000-03-23

`author`
:   David Korn

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1995-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030252/http://www.eclipse.org/org/documents/epl-v10.html)


