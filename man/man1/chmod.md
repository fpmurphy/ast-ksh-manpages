# NAME

chmod - change the access permissions of files

# SYNOPSIS

`chmod` \[ `options` \] mode file ...

# DESCRIPTION

`chmod` changes the permission of each file according to mode, which
can be either a symbolic representation of changes to make, or an octal
number representing the bit pattern for the new permissions.
Symbolic mode strings consist of one or more comma separated list of
operations that can be perfomed on the mode. Each operation is of the
form `user` `op` `perm` where `user` is zero or more of the following
letters:

`u`
: User permission bits.

`g`
: Group permission bits.

`o`
: Other permission bits.

`a`
: All permission bits. This is the default if none are specified.

The `perm` portion consists of zero or more of the following letters:

`r`
: Read permission.

`s`
: Setuid when `u` is selected for `who` and setgid when `g` is
    selected for `who`.

`w`
: Write permission.

`x`
: Execute permission for files, search permission for directories.

`X`
: Same as `x` except that it is ignored for files that do not
    already have at least one `x` bit set.

`l`
: Exclusive lock bit on systems that support it. Group execute must
    be off.

`t`
: Sticky bit on systems that support it.

The `op` portion consists of one or more of the following characters:

`+`
: Cause the permission selected to be added to the
    existing permissions. | is equivalent to +.

`-`
: Cause the permission selected to be removed to the
    existing permissions.

`=`
: Cause the permission to be set to the given permissions.

`&`
: Cause the permission selected to be `and`ed with the
    existing permissions.

`\^`
: Cause the permission selected to be propagated to more
    restrictive groups.

Symbolic modes with the `user` portion omitted are subject to
[`umask`](/web/20150530032021/http://www2.research.att.com:80/~astopen/man/man2/umask.html)(2)
settings unless the `=` `op` or the `--ignore-umask` option is
specified.
A numeric mode is from one to four octal digits (0-7), derived by adding
up the bits with values 4, 2, and 1. Any omitted digits are assumed to
be leading zeros. The first digit selects the set user ID (4) and set
group ID (2) and save text image (1) attributes. The second digit
selects permissions for the user who owns the file: read (4), write (2),
and execute (1); the third selects permissionsfor other users in the
file's group, with the same values; and the fourth for other users not
in the file's group, with the same values.

For symbolic links, by default, `chmod` changes the mode on the file
referenced by the symbolic link, not on the symbolic link itself. The
`-h` options can be specified to change the mode of the link. When
traversing directories with `-R`, `chmod` either follows symbolic
links or does not follow symbolic links, based on the options `-H`,
`-L`, and `-P`. The configuration parameter `PATH\_RESOLVE`
determines the default behavior if none of these options is specified.

When the `-c` or `-v` options are specified, change notifications
are written to standard output using the format, `%s: mode changed to
%0.4o (%s)`, with arguments of the pathname, the numeric mode, and the
resulting permission bits as would be displayed by the `ls` command.

For backwards compatibility, if an invalid option is given that is a
valid symbolic mode specification, `chmod` treats this as a mode
specification rather than as an option specification.

# OPTIONS

-`H`, --`metaphysical`
:   Follow symbolic links for command arguments; otherwise don't follow
    symbolic links when traversing directories.

-`L`, --`logical|follow`
:   Follow symbolic links when traversing directories.

-`P`, --`physical|nofollow`
:   Don't follow symbolic links when traversing directories.

-`R`, --`recursive`
:   Change the mode for files in subdirectories recursively.

-`c`, --`changes`
:   Describe only files whose permission actually change.

-`f`, --`quiet|silent`
:   Do not report files whose permissioins fail to change.

-`h|l`, --`symlink`
:   Change the mode of symbolic links on systems that support
    [`lchmod`](/web/20150530032021/http://www2.research.att.com:80/~astopen/man/man2/lchmod.html)(2).
    Implies `--physical`.

-`i`, --`ignore-umask`
:   Ignore the
    [`umask`](/web/20150530032021/http://www2.research.att.com:80/~astopen/man/man2/umask.html)(2)
    value in symbolic mode expressions. This is probably how you expect
    `chmod` to work.

-`n`, --`show`
:   Show actions but do not change any file modes.

-`F`, --`reference`=`file`
:   Omit the `mode` operand and use the mode of `file` instead.

-`v`, --`verbose`
:   Describe changed permissions of all files.

# EXIT STATUS

`0`
: All files changed successfully.

`&gt;0`
:   Unable to change mode of one or more files.

# SEE ALSO

[`chgrp`](/web/20150530032021/http://www2.research.att.com:80/~astopen/man/man1/chgrp.html)(1),
[`chown`](/web/20150530032021/http://www2.research.att.com:80/~astopen/man/man1/chown.html)(1),
[`lchmod`](/web/20150530032021/http://www2.research.att.com:80/~astopen/man/man1/lchmod.html)(1),
[`tw`](/web/20150530032021/http://www2.research.att.com:80/~astopen/man/man1/tw.html)(1),
[`getconf`](/web/20150530032021/http://www2.research.att.com:80/~astopen/man/man1/getconf.html)(1),
[`ls`](/web/20150530032021/http://www2.research.att.com:80/~astopen/man/man1/ls.html)(1),
[`umask`](/web/20150530032021/http://www2.research.att.com:80/~astopen/man/man2/umask.html)(2)

# IMPLEMENTATION

`version`
:   chmod (AT&T Research) 2012-04-20

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150530032021/http://www.eclipse.org/org/documents/epl-v10.html)


