# NAME

mkdir - make directories

# SYNOPSIS

`mkdir` \[ `options` \] directory ...

# DESCRIPTION

`mkdir` creates one or more directories. By default, the mode of
created directories is `a=rwx` minus the bits set in the
[`umask`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/umask.html)(1).

# OPTIONS

-`m`, --`mode`=`mode`
:   Set the mode of created directories to `mode`. `mode` is symbolic or
    octal mode as in
    [`chmod`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/chmod.html)(1).
    Relative modes assume an initial mode of `a=rwx`.

-`p`, --`parents`
:   Create any missing intermediate pathname components. For each dir
    operand that does not name an existing directory, effects equivalent
    to those caused by the following command shall occur:
    `mkdir -p -m $(umask -S),u+wx $(dirname dir) && mkdir [-m mode] dir`
    where the `-m` mode option represents that option supplied to the
    original invocation of `mkdir`, if any. Each dir operand that
    names an existing directory shall be ignored without error.

-`v`, --`verbose`
:   Print a message on the standard error for each created directory.

# EXIT STATUS

`0`
: All directories created successfully, or the `-p` option was
    specified and all the specified directories now exist.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`chmod`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/chmod.html)(1),
[`rmdir`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/rmdir.html)(1),
[`umask`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/umask.html)(1)

# IMPLEMENTATION

`version`
:   mkdir (AT&T Research) 2010-04-08

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


