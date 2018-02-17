# NAME

mkfifo - make FIFOs (named pipes)

# SYNOPSIS

`mkfifo` \[ `options` \] file ...

# DESCRIPTION

`mkfifo` creates one or more FIFO's. By default, the mode of created
FIFO is `a=rw` minus the bits set in the
[`umask`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/umask.html)(1).

# OPTIONS

-`m`, --`mode`=`mode`
:   Set the mode of created FIFO to `mode`. `mode` is symbolic or octal
    mode as in
    [`chmod`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/chmod.html)(1).
    Relative modes assume an initial mode of `a=rw`.

# EXIT STATUS

`0`
: All FIFO's created successfully.

`&gt;0`
:   One or more FIFO's could not be created.

# SEE ALSO

[`chmod`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/chmod.html)(1),
[`umask`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/umask.html)(1)

# IMPLEMENTATION

`version`
:   mkfifo (AT&T Research) 2009-01-02

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030246/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030246/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030246/http://www.eclipse.org/org/documents/epl-v10.html)


