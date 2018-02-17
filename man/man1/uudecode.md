# NAME

uudecode - decode a uuencoded binary file

# SYNOPSIS

`uudecode` \[ `options` \]

# DESCRIPTION

`uudecode` decodes the named input `file` or the standard input if no
file is specified, to the file name encoded in `file` by `uuencode`.
If `decode-file` is specified then the output is written there. `-` is
equivalent to the standard output.

# OPTIONS

-`c`, --`local`
:   Convert pathnames to file names in the local directory.

-`h`, --`header`
:   The input file contains header and trailer sequences. The header for
    some encoding formats may contain file name and access infomation.
    On by default; -`h` means --`noheader`.

-`l`, --`list`
:   List the encoding method names on the standard output.

-`o`, --`output`=`file`
:   Write the output data into `file` instead of the standard output.
    `decode-file` if specified overrides `--output`.

-`t`, --`text`
:   The input file is a text file that requires \\n =&gt; \\r\\n
    translation on encoding.

-`x`, --`method`=`method`
:   Specifies the encoding `method`. Some encoding methods self identify
    and for those `--method` is optional. [`posix|uuencode`]()
    [`ucb|bsd`]() [`mime|base64`]() [`quoted-printable|qp`]()
    [`binhex|mac-binhex`]() [`sevenbit|7bit`]()

# IMPLEMENTATION

`version`
:   uudecode (AT&T Research) 2002-03-24

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030253/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030253/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030253/http://www.eclipse.org/org/documents/epl-v10.html)


