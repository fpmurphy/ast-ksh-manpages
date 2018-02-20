# NAME

mm2bb - convert mm/man subset to bb markups

# SYNOPSIS

`mm2bb` \[ `options` \] \[ file ... \]

# DESCRIPTION

`mm2bb` is a
[`sed`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/sed.html)(1)/[`ksh`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
script (yes!) that converts input
[`mm`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mm.html)(1)
or
[`man`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/man.html)(1)
documents to a `bb` markups document on the standard output. If `file`
is omitted then the standard input is read. `dir` operands and directory
components of `file` operands are added to the included file search
list. The default `bb` markup style is \[`op`\]`data`\[/ `op`\].

# OPTIONS

-`t`, --`texish`
:   `\\foo`{`data`} `bb` markup style

# SEE ALSO

[`mm2html`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mm2html.html)(1)

# IMPLEMENTATION

`version`
:   mm2bb (AT&T Research) 2010-05-28

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1996-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030246/http://www.eclipse.org/org/documents/epl-v10.html)


