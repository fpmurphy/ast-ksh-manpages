# NAME

delta2patch - generate patch script from pax delta+base archives

# SYNOPSIS

`delta2patch` \[ `options` \] delta base

# DESCRIPTION

`delta2patch` generates a
[`patch`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/patch.html)(1)
`diff -u` script given a
[`pax`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/pax.html)(1)
delta and base source archive to convert files extracted from the base
archive to be equivalent to files extracted from the delta archive with
respect to the base archive.

# SEE ALSO

[`package`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/package.html)(1),
[`pax`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/pax.html)(1)

# IMPLEMENTATION

`version`
:   delta2patch (AT&T Research) 2007-12-11

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1987-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030242/http://www.eclipse.org/org/documents/epl-v10.html)


