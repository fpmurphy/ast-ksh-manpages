# NAME

pathchk - check pathnames for portability

# SYNOPSIS

`pathchk` \[ `options` \] pathname ...

# DESCRIPTION

`pathchk` checks each `pathname` to see if it is valid and/or
portable. A `pathname` is valid if it can be used to access or create a
file without causing syntax errors. A file is portable if no truncation
will result on any conforming POSIX.1 implementation.
By default `pathchk` checks each component of each `pathname` based on
the underlying file system. A diagnostic is written to standard error
for each pathname that:

`-`
: Is longer than `\$(getconf PATH\_MAX)` bytes.

`-`
: Contains any component longer than `\$(getconf NAME\_MAX)` bytes.

`-`
: Contains any directory component in a directory that is
    not searchable.

`-`
: Contains any character in any component that is not valid in its
    containing directory.

`-`
: Is empty.

# OPTIONS

-`p`, --`components`
:   Instead of performing length checks on the underlying file system,
    write a diagnostic for each pathname operand that:

    [`-`]()
    : Is longer than `\$(getconf \_POSIX\_PATH\_MAX)` bytes.

    [`-`]()
    : Contains any component longer than
        `\$(getconf \_POSIX\_NAME\_MAX)` bytes.

    [`-`]()
    : Contains any character in any component that is not in the
        portable filename character set.

-`P`, --`path`
:   Write a diagnostic for each pathname operand that:

    [`-`]()
    : Contains any component with `-` as the first character.

    [`-`]()
    : Is empty.

-`a`, --`all|portability`
:   Equivalent to `--components` `--path`.

# EXIT STATUS

`0`
: All `pathname` operands passed all of the checks.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`getconf`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/getconf.html)(1),
[`creat`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man2/creat.html)(2),
[`pathchk`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man2/pathchk.html)(2)

# IMPLEMENTATION

`version`
:   pathchk (AT&T Research) 2009-07-24

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030248/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030248/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030248/http://www.eclipse.org/org/documents/epl-v10.html)


