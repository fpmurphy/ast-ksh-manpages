# NAME

changes - list changed \$PACKAGEROOT package source files

# SYNOPSIS

`changes` \[ `options` \] \[ from-date \[ to-date \] \] \[ -- ls-option ... \]

# DESCRIPTION

`changes` lists \$PACKAGEROOT relative package source files that
changed between `from-date` between `to-date` . The default `from-date`
is the modify time of `\$PACKAGEROOT/README`. The default `to-date` is
`now` . The changed files are listed by
[`ls`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/ls.html)(1)
with the optional `ls-option` operands.

# OPTIONS

-`p`, --`package`=`package`
:   List source files for `package` only. Multiple `--package` options
    may be specified. By default source files for all packages in
    `\$PACKAGEROOT/lib/package` are checked.

# SEE ALSO

[`tw`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/tw.html)(1),
[`ls`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/ls.html)(1)

# IMPLEMENTATION

`version`
:   changes (AT&T Research) 2010-01-20

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 2005-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030239/http://www.eclipse.org/org/documents/epl-v10.html)


