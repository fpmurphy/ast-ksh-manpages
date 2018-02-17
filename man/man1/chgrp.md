# NAME

chgrp - change the group ownership of files

# SYNOPSIS

`chgrp` \[ `options` \] \[\[owner:\]group\] file ...

# DESCRIPTION

`chgrp` changes the group ownership of each file to `group`, which can
be either a group name or a numeric group id. The user ownership of each
file may also be changed to `user` by prepending `user``:` to the
group name.

# OPTIONS

-`b`, --`before`=`file`
:   Only change files with `ctime` before (less than) the `mtime` of
    `file`.

-`c`, --`changes`
:   Describe only files whose ownership actually changes.

-`f`, --`quiet|silent`
:   Do not report files whose ownership fails to change.

-`h|l`, --`symlink`
:   Change the ownership of symbolic links on systems that support
    [`lchown`](/web/20150530235459/http://www2.research.att.com:80/~astopen/man/man2/lchown.html)(2).
    Implies `--physical`.

-`m`, --`map`
:   The first operand is interpreted as a file that contains a map of
    space separated `from\_uid:from\_gid to\_uid:to\_gid` pairs. The
    `uid` or `gid` part of each pair may be omitted to mean any `uid` or
    `gid`. Ownership of files matching the `from` part of any pair is
    changed to the corresponding `to` part of the pair. The matching for
    each file operand is in the order `uid`:`gid`, `uid`:, :`gid`. For a
    given file, once a `uid` or `gid` mapping is determined it is not
    overridden by any subsequent match. Unmatched files are
    silently ignored.

-`n`, --`show`
:   Show actions but don't execute.

-`N`, --`numeric`
:   By default numeric user and group id operands are first interpreted
    as names; if no name exists then they are interpreted as explicit
    numeric ids. `--numeric` interprets numeric id operands as
    numeric ids.

-`r`, --`reference`=`file`
:   Omit the explicit ownership operand and use the ownership of
    `file` instead.

-`u`, --`unmapped`
:   Print a diagnostic for each file for which either the `uid` or `gid`
    or both were not mapped.

-`v`, --`verbose`
:   Describe changed permissions of all files.

-`H`, --`metaphysical`
:   Follow symbolic links for command arguments; otherwise don't follow
    symbolic links when traversing directories.

-`L`, --`logical|follow`
:   Follow symbolic links when traversing directories.

-`P`, --`physical|nofollow`
:   Don't follow symbolic links when traversing directories.

-`R`, --`recursive`
:   Recursively change ownership of directories and their contents.

-`X`, --`test`
:   Canonicalize output for testing.

# EXIT STATUS

`0`
: All files changed successfully.

`&gt;0`
:   Unable to change ownership of one or more files.

# SEE ALSO

[`chmod`](/web/20150530235459/http://www2.research.att.com:80/~astopen/man/man1/chmod.html)(1),
[`chown`](/web/20150530235459/http://www2.research.att.com:80/~astopen/man/man2/chown.html)(2),
[`tw`](/web/20150530235459/http://www2.research.att.com:80/~astopen/man/man1/tw.html)(1),
[`getconf`](/web/20150530235459/http://www2.research.att.com:80/~astopen/man/man1/getconf.html)(1),
[`ls`](/web/20150530235459/http://www2.research.att.com:80/~astopen/man/man1/ls.html)(1)

# IMPLEMENTATION

`version`
:   chgrp (AT&T Research) 2012-04-20

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150530235459/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20150530235459/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150530235459/http://www.eclipse.org/org/documents/epl-v10.html)


