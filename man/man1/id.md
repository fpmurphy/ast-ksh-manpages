# NAME

id - return user identity

# SYNOPSIS

`id` \[ `options` \] \[user\]

# DESCRIPTION

If no `user` operand is specified `id` writes user and group IDs and
the corresponding user and group names of the invoking process to
standard output. If the effective and real IDs do not match, both are
written. Any supplementary groups the current process belongs to will
also be written.
If a `user` operand is specified and the process has permission, the
user and group IDs and any supplementary group IDs of the selected user
will be written to standard output.

If any options are specified, then only a portion of the information is
written.

# OPTIONS

-`n`, --`name`
:   Write the name instead of the numeric ID.

-`r`, --`real`
:   Writes real ID instead of the effective ID.

-`a`
: This option is ignored.

-`g`, --`group`
:   Writes only the group ID.

-`u`, --`user`
:   Writes only the user ID.

-`G`, --`groups`
:   Writes only the supplementary group IDs.

-`s`, --`fair-share`
:   Writes fair share scheduler IDs and groups on systems that support
    fair share scheduling.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`logname`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/logname.html)(1),
[`who`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/who.html)(1),
[`getgroups`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man2/getgroups.html)(2)

# IMPLEMENTATION

`version`
:   id (AT&T Research) 2004-06-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030244/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030244/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030244/http://www.eclipse.org/org/documents/epl-v10.html)


