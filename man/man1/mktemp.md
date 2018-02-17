# NAME

mktemp - make temporary file or directory

# SYNOPSIS

`mktemp` \[ `options` \] \[ prefix \]

# DESCRIPTION

`mktemp` creates a temporary file with optional base name prefix
`prefix`. If `prefix` is omitted then `tmp\_` is used and `--tmp` is
implied. If `prefix` contains a directory prefix then that directory
overrides any of the directories described below. A temporary file will
have mode `rw-------` and a temporary directory will have mode
`rwx------` , subject to
[`umask`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/umask.html)(1).
Generated paths have these attributes:

`\``
: Lower case to avoid clashes on case ignorant filesystems.

`\``
: Pseudo-random part to deter denial of service attacks.

`\``
: Default pseudo-random part (no specific `X...` template) formatted
    to accomodate 8.3 filesystems.

A consecutive trailing sequence of `X`'s in `prefix` is replaced by
the pseudo-random part. If there are no `X`'s then the pseudo-random
part is appended to the prefix.

# OPTIONS

-`d`, --`directory`
:   Create a directory instead of a regular file.

-`m`, --`mode`=`mode`
:   Set the mode of the created temporary to `mode`. `mode` is symbolic
    or octal mode as in
    [`chmod`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/chmod.html)(1).
    Relative modes assume an initial mode of `u=rwx`.

-`p`, --`default`=`directory`
:   Use `directory` if the `TMPDIR` environment variable is not
    defined. Implies `--tmp`.

-`q`, --`quiet`
:   Suppress file and directory error diagnostics.

-`R`, --`regress`=`seed`
:   The pseudo random generator is seeded with `seed` instead of
    process/system specific transient data. Use for testing only. A seed
    of `0` is silently changed to `1`.

-`t`, --`tmp|temporary-directory`
:   Create a path rooted in a temporary directory.

-`u`, --`unsafe|dry-run`
:   Check for file/directory existence but do not create. Use this for
    testing only.

# SEE ALSO

[`mkdir`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mkdir.html)(1),
[`pathtemp`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man3/pathtemp.html)(3),
[`mktemp`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man3/mktemp.html)(3)

# IMPLEMENTATION

`version`
:   mktemp (AT&T Research) 2010-03-05

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


