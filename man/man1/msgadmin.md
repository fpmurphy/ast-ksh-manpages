# NAME

msgadmin - message catalog file administration

# SYNOPSIS

`msgadmin` \[ `options` \] \[ file ... \]

# DESCRIPTION

`msgadmin` administers message catalog files. If no `file` operands
are specified then all message files in the local `\$INSTALLROOT`
source tree are operated on. Exactly one of `--generate`,
`--remove`, `--translate` , or `--verify` must be specified.

# OPTIONS

-`D`, --`debug`
:   Passed to
    [`translate`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/translate.html)(1).

-`a`, --`all`
:   Passed to
    [`translate`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/translate.html)(1).

-`c`, --`cache`
:   Passed to
    [`translate`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/translate.html)(1).

-`d`, --`dialect`=`dialect`
:   Operate on the dialects in the `,` separated `dialect` list. `-`
    means all dialects supported by
    [`translate`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/translate.html)(1).
    The default value is `-`.

-`f`, --`force`
:   Force binary catalog generation even when the current binary is
    newer than the source.

-`g`, --`generate`
:   Generate and install
    [`gencat`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/gencat.html)(1)
    binary message catalogs.

-`l`, --`list`
:   List each installed message catalog name paired with its
    input source.

-`n`, --`show`
:   Show commands but do not execute.

-`o`, --`omit`=`pattern`
:   Omit
    [`translate`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/translate.html)(1)
    methods matching the
    [`ksh`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
    `pattern`.

-`r`, --`remove`
:   Remove all translated message files and work directories.

-`s`, --`share`
:   Generate and install
    [`msggen`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/msggen.html)(1)
    machine independent binary message catalogs.

-`t`, --`translate`
:   Translate using
    [`translate`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/translate.html)(1).

-`v`, --`verify`
:   Verify that translated message files satisfy
    [`gencat`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/gencat.html)(1) syntax.

# SEE ALSO

[`gencat`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/gencat.html)(1),
[`ksh`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1),
[`msggen`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/msggen.html)(1),
[`translate`](/web/20150527180649/http://www2.research.att.com/~astopen/man/man1/translate.html)(1)

# IMPLEMENTATION

`version`
:   msgadmin (AT&T Labs Research) 2001-06-08

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 2000-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150527180649/http://www.eclipse.org/org/documents/epl-v10.html)


