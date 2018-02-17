# NAME

pwd - write working directory name

# SYNOPSIS

`pwd` \[ `options` \]

# DESCRIPTION

`pwd` writes an absolute pathname of the current working directory to
standard output. An absolute pathname is a pathname that begins with
`/` that does not contains any `.` or `..` components.

If both `-L` and `-P` are specified, the last one specified will be
used. If neither `-P` or `-L` is specified then the behavior will be
determined by the `getconf` parameter `PATH\_RESOLVE`. If
`PATH\_RESOLVE` is `physical`, then the behavior will be as if
`-P` were specified. Otherwise, the behavior will be as if `-L` were
specified.

# OPTIONS

-`L`
: The absolute pathname may contains symbolic link components. This is
    the default.

-`P`
: The absolute pathname will not contain any symbolic link components.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
: An error occurred.

# SEE ALSO

[`cd`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/cd.html)(1),
[`getconf`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/getconf.html)(1)

# IMPLEMENTATION

`version`
: pwd (AT&T Research) 1999-06-07

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030249/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030249/http://www.opensource.org/licenses/cpl1.0.txt)


