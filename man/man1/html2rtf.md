# NAME

html2rtf - html to rtf filter

# SYNOPSIS

`html2rtf` \[ `options` \] \[ file ... \]

# DESCRIPTION

`html2rtf` converts input `html` documents to an `RTF` document on
the standard output. `html2rtf` expects properly nested begin/end tags
in the input `html` and warns about imbalance.

# OPTIONS

-`d`, --`debug`=`level`
:   Set the debug trace level to `level`. Higher levels produce
    more output.

-`f`, --`font-size`=`size`
:   Set the initial font size to `size` points. The default value is
    `12`.

-`p`, --`project-file`=`file`
:   Appends MS HELP project information to the help project file `file`.
    This file combines individual RTF files into a
    hyper-linked collection. Note that MS expects `file` to have a
    `.hlp` extension.

-`v`, --`verbose`
:   Enable verbose error and warning messages. Some `html` source
    can't stand the heat.

# SEE ALSO

[`man`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/man.html)(1),
[`mm`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/mm.html)(1),
[`mm2html`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/mm2html.html)(1),
[`troff`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/troff.html)(1),
[`troff2html`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/troff2html.html)(1)

# IMPLEMENTATION

`version`
:   html2rtf (AT&T Research) 1999-01-01

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1996-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030244/http://www.eclipse.org/org/documents/epl-v10.html)


