# NAME

uuencode - encode a binary file

# SYNOPSIS

`uuencode` \[ `options` \]

# DESCRIPTION

`uuencode` writes an encoded version of the named input `file`, or the
standard input if no file is specified, to the standard output.
`decode-file` is the name stored in the encoded output header. This is
the default name that will be used by `uudecode` when decoding.

# OPTIONS

-`h`, --`header`
:   Write header and trailer sequences to the encoded output. The header
    for some encoding formats may contain file name and
    access infomation. On by default; -`h` means --`noheader`.

-`l`, --`list`
:   List the encoding method names on the standard output.

-`o`, --`output`=`file`
:   Write the output data into `file` instead of the standard output.

-`t`, --`text`
:   The input file is a text file that requires \\n =&gt; \\r\\n
    translation on encoding.

-`x`, --`method`=`method`
:   Specifies the encoding `method`: [`posix|uuencode`]()
    [`ucb|bsd`]() [`mime|base64`]() [`quoted-printable|qp`]()
    [`binhex|mac-binhex`]() [`sevenbit|7bit`]()

# IMPLEMENTATION

`version`
:   uuencode (AT&T Research) 2002-03-24

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030253/http://www.eclipse.org/org/documents/epl-v10.html)


