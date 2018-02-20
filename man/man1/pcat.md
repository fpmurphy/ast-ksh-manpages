# NAME

pcat - unpack and concatenate files created by pack

# SYNOPSIS

`pcat` \[ `options` \] file ...

# DESCRIPTION

`pcat` does for packed files what
[`cat`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/cat.html)(1)
does for ordinary files, except that `pcat` cannot be used as filter.
For each `file` specified, a search is made for a file named
`file``.z` (or just `file`, if `file` ends in `.z`). If this file
appears to be a packed file, `pcat` unpacks the file and writes it to
standard output.

# EXIT STATUS

`0`
: All files unpacked successfully.

`n`
: `n` files failed to unpack, where `n` is less than 125.

`125`
: 125 or more files failed to unpack.

# SEE ALSO

pack(1), unpack(1), cat(1), zcat(1), gzcat(1)

# IMPLEMENTATION

`version`
:   unpack (AT&T Research) 2003-04-28

`author`
:   David Korn

`copyright`
:   Copyright © 1993-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030248/http://www.eclipse.org/org/documents/epl-v10.html)


