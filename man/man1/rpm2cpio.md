# NAME

rpm2cpio - convert rpm file to cpio file

# SYNOPSIS

`rpm2cpio` \[ `options` \] \[ file \]

# DESCRIPTION

`rpm2cpio` converts the input
[`rpm`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/rpm.html)(1)
`file`, or the standard input if `file` is omitted, to a
[`cpio`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/cpio.html)(1)
file on the standard output.
This command is provided for interface compatibility; use
[`pax`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/pax.html)(1)
to read `rpm` files directly.

# OPTIONS

-`n`, --`show`
:   Show the underlying
    [`pax`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/pax.html)(1)
    command but do not execute.

-`v`, --`verbose`
:   List the package file members as they are converted.

# SEE ALSO

[`cpio`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/cpio.html)(1),
[`pax`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/pax.html)(1),
[`rpm`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/rpm.html)(1)

# IMPLEMENTATION

`version`
:   rpm2cpio (AT&T Labs Research) 1999-12-25

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030249/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1987-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030249/http://www.eclipse.org/org/documents/epl-v10.html)


