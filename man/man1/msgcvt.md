# NAME

msgcvt - convert message file to/from html

# SYNOPSIS

`msgcvt` \[ `options` \]

# DESCRIPTION

`msgcvt` reads a
[`gencat`](/web/20150528150110/http://www2.research.att.com/~astopen/man/man1/gencat.html)(1)
format file on the standard input and converts it to `html` on the
standard output. The input file must contain the control statement
`\$quote "` and use the " character to quote message text. The output
is in a form suitable for automatic translation by web sites like
`http://babelfish.altavista.com/` or filters like
[`translate`](/web/20150528150110/http://www2.research.att.com/~astopen/man/man1/translate.html)(1).

# OPTIONS

-`h`, --`html`
:   Generate `html` from
    [`gencat`](/web/20150528150110/http://www2.research.att.com/~astopen/man/man1/gencat.html)(1)
    input. This is the default.

-`m`, --`msg`
:   Generate a
    [`gencat`](/web/20150528150110/http://www2.research.att.com/~astopen/man/man1/gencat.html)(1)
    message file from (presumably translated) `html`. Wide characters
    are UTF-8 encoded.

-`r`, --`raw`
:   The message file is raw message text, one message per line, with no
    quoting or line numbering.

# SEE ALSO

[`gencat`](/web/20150528150110/http://www2.research.att.com/~astopen/man/man1/gencat.html)(1),
[`msgcc`](/web/20150528150110/http://www2.research.att.com/~astopen/man/man1/msgcc.html)(1),
[`msggen`](/web/20150528150110/http://www2.research.att.com/~astopen/man/man1/msggen.html)(1),
[`translate`](/web/20150528150110/http://www2.research.att.com/~astopen/man/man1/translate.html)(1)

# IMPLEMENTATION

`version`
:   msgcvt (AT&T Research) 2000-05-01

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 2000-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150528150110/http://www.eclipse.org/org/documents/epl-v10.html)


