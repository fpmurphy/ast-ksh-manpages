# NAME

ncsl - list the number of non-comment source lines for each C file

# SYNOPSIS

`ncsl` \[ `options` \] \[ file ... \]

# DESCRIPTION

`ncsl` lists the number of non-comment source lines for each C `file`
argument. If no `file` arguments are specified then the standard input
is read. /\`...\`/ and // style comments are recognized.

# OPTIONS

-`s`, --`summary`
:   If more than one `file` is specified then list a summary count for
    all files.

# SEE ALSO

[`wc`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/wc.html)(1)

# IMPLEMENTATION

`version`
:   ncsl (AT&T Research) 1996-10-11

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1994-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030247/http://www.eclipse.org/org/documents/epl-v10.html)


